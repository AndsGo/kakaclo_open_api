---
description: xulin
---

# 一个可被 CI 约束的 FastAPI 后端模板：从分层规范到团队协作

最近整理了一个可复用的 FastAPI 后端模板，目标不是简单搭一个能运行的 API 项目， 而是把我们在后端项目里经常反复讨论的工程规范固化下来，并尽量交给自动化工具检查。

项目地址：

```
https://github.com/AndsGo/fastapi-backend-template
```

### 为什么需要这个模板

很多后端项目一开始都会经历类似流程：

* 搭 FastAPI 工程结构。
* 接 SQLAlchemy 和 Alembic。
* 补配置管理、日志、测试、lint、类型检查。
* 再讨论 API、Service、Repository 应该怎么分层。
* 后面 review 时继续争论 endpoint 能不能直接查数据库、service 能不能互相调用。

这些问题本身都不复杂，但每个项目重新做一遍，会消耗很多团队注意力。更麻烦的是， 如果规范只写在文档里，最后还是要靠 review 人工拦截。人会漏，标准也容易因为项目压力被放松。

所以这个模板的核心目标是：

> 把基础后端结构、分层规范、验证命令和 CI gate 放进同一个项目基线里。

换句话说，这不是一个“代码生成器”，而是一个团队协作基线。

### 这个模板包含什么

当前模板包含这些基础能力：

* FastAPI API v1 路由结构。
* SQLAlchemy 模型、会话、仓储和 Alembic 迁移。
* PostgreSQL 和 MySQL 支持，通过 `DATABASE_URL` 切换。
* Redis 客户端和统一 Redis key 模板。
* 定时任务定义、调度器、worker、任务注册和执行记录。
* JSON Lines 日志，默认输出到 stdout。
* `pytest` 测试。
* `ruff` 代码检查。
* `mypy` 类型检查。
* `import-linter` 架构边界检查。
* 英文 README、中文 README 和项目文档。

模板里还保留了一个 `examples` 示例模块，用来展示新增业务模块时推荐的文件组织方式。

### 核心分层设计

这个项目采用模块化单体结构，核心依赖方向是：

```
api -> application -> services -> repositories -> models -> database
```

每层职责如下：

* `api`：只处理 HTTP 协议、请求解析、响应模型和依赖注入。
* `application`：用例编排层，负责跨模块协调、事务边界和非 HTTP DTO。
* `services`：原子业务能力层，负责单一模块内的业务行为。
* `repositories`：数据库访问层，封装 SQLAlchemy 查询。
* `models`：数据库表定义。
* `schemas`：Pydantic 请求和响应结构。
* `jobs/handlers`：后台任务入口，本质上也是 delivery adapter。

几个关键规则：

* Endpoint 不写业务逻辑。
* Endpoint 不直接查数据库。
* API 不直接调用 Repository。
* Service 不能互相调用。
* 跨模块编排必须放在 Application。
* Job handler 只能调用 Application use case。

这套规则的目的不是为了“分层而分层”，而是让代码在项目变大后仍然能保持边界清晰。 如果 endpoint 可以随便调用 repository，或者 service 之间互相调用，短期看起来很快， 长期会让业务流程散落在多个地方，测试和修改都会变困难。

### Application 为什么是唯一编排层

模板里刻意引入了 `app/application`，它不是简单的目录分类，而是一个明确的架构边界。

Application 层负责这些事情：

* 把 API schema 转成 use case 所需的 DTO 或命令对象。
* 组织一个业务用例需要调用的 service 或 repository。
* 承担跨模块流程。
* 以后承接权限、幂等、事务边界等用例级逻辑。

Service 层则保持原子能力。例如 `ExampleItemService` 只处理 example item 的创建、更新、 查询等能力，不应该去调用另一个 service 完成跨模块流程。

这样做的好处是：当一个业务动作需要协调多个模块时，我们可以直接去 application use case 找入口，而不是在 endpoint、job handler 或多个 service 之间追调用链。

### 团队规范如何被 CI 卡住

文档里的规范很重要，但只靠文档不够。这个模板把关键检查放进了 CI：

```
python -m pytest
python -m ruff check .
lint-imports
python -m mypy app
```

每个命令负责不同层面的质量约束：

* `pytest`：防止行为回归。
* `ruff`：检查 import 顺序、未使用变量、基础 bug pattern 和代码风格。
* `mypy`：检查类型一致性。
* `lint-imports`：检查架构依赖方向。

其中 `lint-imports` 是这次模板里比较关键的一步。它读取 `.importlinter`，会拒绝违反分层规则的 import。

当前配置会卡住这些情况：

* API 直接 import `services`、`repositories`、`models` 或 `app.db`。
* Job handler 直接 import `services`、`repositories`、`models`、`app.db` 或 `api`。
* Service 之间互相 import。
* Repository 依赖 API、Application、Service 或 Jobs。
* Model 依赖上层模块。

例如，如果有人在 API 层直接写：

```
from app.repositories.example_repository import ExampleItemRepository
```

`lint-imports` 会失败，并指出类似这样的错误：

```
app.api is not allowed to import app.repositories:
​
- app.api.v1.dependencies -> app.repositories.example_repository
```

这就把“规范争议”从口头讨论变成了自动化检查。不是某个人不让这么写，而是项目规则不允许。

### 新增模块的标准流程

新增业务模块时，可以参考现有 `examples` 模块，推荐流程是：

1. 在 `app/models` 新增数据库模型。
2. 在 `app/schemas` 新增请求和响应 schema。
3. 在 `app/repositories` 新增 repository。
4. 在 `app/services` 新增原子 service。
5. 在 `app/application` 新增 DTO 和 use case。
6. 在 `app/api/v1/endpoints` 新增 endpoint。
7. 在 `app/api/v1/router.py` 注册路由。
8. 如果需要后台执行，在 `app/jobs/handlers` 新增 job handler。
9. 新增 Alembic migration。
10. 新增或更新测试。
11. 更新相关文档。

这个顺序不是强制仪式，而是为了让每个模块都有稳定的落点。后来的人看到目录结构， 就能大致判断某段代码应该在哪里，而不是每个模块都长成不同形状。

### 定时任务也是同一套架构

模板内置了一个通用 job 系统：

* `scheduled_jobs` 保存任务定义。
* `scheduled_job_runs` 保存触发和执行记录。
* scheduler 只负责扫描到期任务并创建 pending run。
* worker 只负责 claim run 并调用 handler。
* handler 只作为适配器，把任务执行转发到 application use case。

也就是说，后台任务不会绕过分层规则。HTTP endpoint 和 job handler 都是入口层， 它们都不应该直接编排复杂业务，也不应该直接访问数据库。

### 当前没有内置什么

这个模板也刻意没有把所有东西都放进去：

* 没有默认前端代码。
* 没有默认 `docker-compose.yml`。
* 没有完整认证和权限实现。
* 没有绑定具体业务领域。

认证和权限目前是占位设计。后续项目真正落地时，需要根据团队实际情况选择 SSO、OAuth2、 OIDC、API key 或 RBAC 方案。

这些能力没有默认加入，是为了避免模板一开始就变得过重。模板应该提供稳定基线，而不是提前替业务项目做太多决定。

### 使用建议

如果新项目需要一个 FastAPI 后端基线，可以直接基于这个模板开始。

建议团队使用时遵守几个原则：

* 新模块优先参考 `examples` 的结构。
* 行为变更必须补测试。
* 新配置必须同步 `.env.example`。
* 模型变更必须补 migration。
* 规范变更必须同时更新文档和 `.importlinter`。
* 不要绕过 CI gate 合并代码。

如果某条架构规则确实不适合某个项目，也可以调整。但调整方式应该是显式修改规则和文档， 而不是在业务代码里默默破例。

### 总结

这个 FastAPI 后端模板的重点不是“用了哪些库”，而是把团队协作中的基础约定沉淀成可执行的项目结构。

它解决的核心问题有三个：

1. 减少新项目重复搭基础工程的成本。
2. 让分层规范有明确代码位置和文档说明。
3. 用 CI 自动检查关键边界，降低 review 中的规范争议。

后续如果团队继续使用这个模板，可以逐步补充更贴近实际项目的认证方案、部署方案、 业务模块示例和更细的测试规范。但基础方向应该保持不变：规范不只写在文档里，也要能被工具执行。
