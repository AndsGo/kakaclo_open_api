---
description: xulin
---

# Claude Code 团队入门指南

> 从安装到团队级配置，帮助你在日常开发中高效使用 Claude Code。

### 目录

* 第 1 章：什么是 Claude Code
* 第 2 章：安装与首次使用
* 第 3 章：日常提效指南
* 第 4 章：理解陌生代码库
* 第 5 章：项目级配置
* 第 6 章：使用 Superpowers 规范化开发流程
* 第 7 章：推荐 Plugin 与 Skill
* 第 8 章：进阶技巧
* 第 9 章：常见问题与避坑

***

### 第 1 章：什么是 Claude Code

Claude Code 是一个运行在终端里的 **AI 编程代理**。它不是聊天机器人，也不是代码补全工具——它能直接读写你的项目文件、运行命令、自主完成开发任务。

你描述意图，Claude 负责探索代码、制定方案、实现功能、运行验证。你可以随时介入纠正方向。

#### 与其他 AI 工具的区别

|          | ChatGPT / 网页对话 | GitHub Copilot | Claude Code          |
| -------- | -------------- | -------------- | -------------------- |
| **工作方式** | 你复制代码过去问       | 在编辑器内补全代码      | 直接在你的项目里读、写、运行       |
| **上下文**  | 你手动提供          | 当前文件           | 整个项目 + 终端            |
| **自主性**  | 无              | 低（补全级）         | 高（探索 → 规划 → 实现 → 验证） |

#### 核心工作模式

```
你描述意图 → Claude 探索代码库 → 制定方案 → 实现代码 → 运行验证
                    ↑                                      |
                    └───── 你随时可以介入纠正方向 ──────────┘
```

这种"代理式"工作方式意味着：你不需要逐行指导 Claude 怎么写，而是告诉它你想要什么结果，它会自己想办法实现。

***

### 第 2 章：安装与首次使用

#### 前置条件

* 一个终端或命令行工具
* 一个 Claude 订阅（Pro、Max、Teams 或 Enterprise）、Claude Console 账号（API 预付费）、或支持的云服务商（Amazon Bedrock / Google Vertex AI）
* Windows 用户需要安装 [Git for Windows](https://git-scm.com/downloads/win)

#### 安装

根据你的操作系统选择安装方式：

**macOS / Linux / WSL（推荐）：**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell：**

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Windows CMD：**

```batch
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

**其他方式：**

```bash
# macOS Homebrew
brew install --cask claude-code

# Windows WinGet
winget install Anthropic.ClaudeCode
```

> 通过原生安装脚本安装的版本会自动后台更新。Homebrew / WinGet 安装的版本需要手动更新。

#### 认证

首次运行 `claude` 命令后，会引导你完成登录：

```bash
# 进入你的项目目录
cd /path/to/your-project

# 启动 Claude Code
claude
```

支持的账号类型：

* **Claude Pro / Max / Teams / Enterprise**（推荐）
* **Claude Console**（API 预付费额度）
* **Amazon Bedrock / Google Vertex AI**（企业云服务商）

登录完成后凭证会被保存，后续无需重复登录。如需切换账号，运行 `/login`。

#### 第一次对话

以我们的 LegoFlow 项目为例，进入项目目录后启动 `claude`，尝试以下几个指令感受能力边界：

**让 Claude 了解项目全貌：**

```
这个项目是做什么的？
```

Claude 会自动探索项目的文件结构、README、配置文件等，然后给你一份项目概述。

**让 Claude 执行命令：**

```
运行测试并告诉我结果
```

Claude 会找到测试命令（如 `pytest`），执行它，并分析测试结果。

**让 Claude 解读代码：**

```
解释一下 lego_flow/activities/base.py 的核心逻辑
```

Claude 会读取文件内容，然后用你能理解的方式讲解代码结构和设计意图。

#### 基本交互

| 操作          | 按键/命令                          |
| ----------- | ------------------------------ |
| 发送消息        | `Enter`                        |
| 中途停止 Claude | `Esc`                          |
| 查看帮助        | `/help`                        |
| 清空上下文       | `/clear`                       |
| 引用文件        | `@文件路径`（如 `@lego_flow/api.py`） |

#### IDE 集成

除了 CLI 终端使用，Claude Code 也提供 VS Code 和 JetBrains 的编辑器扩展。安装后可以在编辑器内直接与 Claude 对话，适合习惯图形界面的同事。详见 [官方 IDE 集成文档](https://code.claude.com/docs/zh-CN/ide-integrations)。

***

### 第 3 章：日常提效指南

这是本文档的核心章节。掌握这 4 个场景，你的日常开发效率会有显著提升。

**贯穿原则：**

* **给 Claude 验证手段**是你能做的最高杠杆的事——每次都要求 Claude 运行测试、lint 或其他检查来确认结果
* **具体 > 模糊**——好的提示能让 Claude 一次完成任务，省去多轮纠正

#### 3.1 写功能代码

**模糊提示（容易返工）：**

```
写一个函数处理数据
```

**具体提示（一次到位）：**

```
在 lego_flow/activities/data/ 下新建一个 Activity，参考 @lego_flow/activities/data/sql_query.py
的模式，功能是将 CSV 文本转为 JSON。输入是 csv_content: str，输出是
parsed_rows: list[dict]。写完后运行 /test 验证。
```

**技巧：** 用 `@文件路径` 指向一个参考文件，Claude 会自动对齐风格和模式。这比在提示里写"遵循项目规范"有效得多。

#### 3.2 调试

**模糊提示（浪费时间）：**

```
报错了
```

**具体提示（直达根因）：**

```
pytest tests/workflows/test_research.py 失败了，错误信息是：

  AssertionError: expected 3 results, got 0

分析根因并修复，修复后重新运行测试确认通过。
```

**技巧：** 可以直接把错误信息管道输入给 Claude：

```bash
pytest tests/ 2>&1 | claude -p "分析这些测试失败的原因并修复"
```

#### 3.3 写测试

**模糊提示（覆盖不全）：**

```
加测试
```

**具体提示（覆盖到位）：**

```
为 lego_flow/activities/llm/completion.py 编写单元测试，覆盖以下场景：
1. 正常响应
2. API 超时
3. 空输入

使用 AsyncMock 模拟 OpenAI 调用，不要 mock 其他东西。
参考 @tests/activities/llm/test_completion.py 的现有模式。
写完后运行 pytest 验证全部通过。
```

**技巧：** 始终要求 Claude 写完测试后自己运行验证，这样它能立即发现并修复问题，而不是把一堆不能跑的测试交给你。

#### 3.4 做 PR

```
查看当前分支相对于 master 的所有变更，写一个描述清晰的 commit message 并提交，
然后创建 PR。PR 描述要包含变更摘要和测试情况。
```

Claude 会自动使用 `gh` CLI 来创建 PR。确保你的环境已安装并认证 `gh`：

```bash
# 安装（如果没有）
# macOS: brew install gh
# Windows: winget install GitHub.cli

# 认证
gh auth login
```

***

### 第 4 章：理解陌生代码库

Claude Code 最被低估的用法之一：**当作一位随时可问的资深同事**。这对新人 onboarding 和跨项目协作尤其有价值。

#### 4.1 快速了解项目全貌

进入一个陌生项目后，直接问：

```
这个项目的架构是怎样的？核心模块有哪些？数据是怎么流转的？
```

以 LegoFlow 为例，你还可以更有针对性：

```
解释 LegoFlow 的 Activity → Workflow → Worker 这条链路是怎么工作的，
从一个 API 请求到最终执行经过了哪些步骤？
```

Claude 会自动读取相关源码文件，然后给你一份清晰的架构说明。

#### 4.2 深入理解特定代码

像问同事一样直接提问：

```
为什么 BaseActivity 要用泛型 InputT, OutputT？这样设计的好处是什么？
```

```
@lego_flow/workflows/utils.py 里的 run_parallel 是怎么实现并行的？
```

```
@lego_flow/activities/registry.py 第 45 行这个装饰器做了什么？
```

**技巧：** 用 `@文件路径` 让 Claude 先读文件再回答，能大幅减少"编造"的可能。

#### 4.3 追溯变更历史

Claude 可以结合 git 历史回答"为什么"的问题：

```
查看 git log，这个模块最近一个月有哪些重要变更？
```

```
用 git blame 看看 api.py 中的输入校验逻辑是谁在什么时候加的，当时的 commit message 是什么？
```

#### 4.4 用 Subagent 做大范围调查

当你需要跨多个模块做调查时，用 subagent 避免主对话的上下文膨胀：

```
用 subagent 调查项目中所有的错误处理模式，总结成一份清单
```

Subagent 会在独立的上下文中工作，只把调查结果的摘要返回给你，你的主对话保持干净。关于 subagent 的更多细节见第 8 章。

#### 核心价值

这种用法显著缩短了新人的上手时间——不用反复打扰忙碌的同事，Claude 可以解答大部分"这段代码是怎么回事"的问题。Claude Code 官方也将代码库探索列为其核心使用场景之一。

***

### 第 5 章：项目级配置

这一章是**标准化团队工作流**的核心。通过以下配置，你可以让 Claude Code"懂"你们的项目规范，让每个团队成员获得一致的开发体验。

#### 5.1 CLAUDE.md — 项目规则文件

CLAUDE.md 是 Claude Code 在**每次对话开始时自动读取**的指令文件，相当于给 Claude 的"员工手册"。

**放在哪里：**

| 位置                    | 作用域          | 是否提交 git |
| --------------------- | ------------ | -------- |
| `~/.claude/CLAUDE.md` | 个人全局（所有项目生效） | 否        |
| `项目根目录/CLAUDE.md`     | 团队共享         | 是        |
| `子目录/CLAUDE.md`       | 处理该目录文件时自动加载 | 是        |

**该写什么 vs 不该写什么：**

| 该写                 | 不该写                        |
| ------------------ | -------------------------- |
| Claude 猜不到的构建/测试命令 | 读代码就能推断的东西                 |
| 与默认值不同的代码风格规则      | 标准语言约定（如"Python 用 4 空格缩进"） |
| 项目特有的架构决策          | 经常变化的信息                    |
| 分支命名、提交信息规范        | 逐文件描述代码库                   |
| 开发环境的特殊要求          | 长篇教程或详细 API 文档             |

**维护原则：** 对 CLAUDE.md 的每一行问自己：**"删掉它 Claude 会犯错吗？"** 如果不会就删掉。臃肿的 CLAUDE.md 会导致 Claude 忽略你真正重要的规则。像维护代码一样定期精简它。

**LegoFlow 的实际示例：**

```markdown
# LegoFlow — Claude Code 项目规则

## 技术栈
- Python 3.12+, Temporal SDK, Pydantic v2, FastAPI
- 测试：pytest + pytest-asyncio
- 代码检查：ruff（lint + format）
- 类型检查：pyright

## 代码规范
### 命名约定
- 变量/函数：snake_case
- 类名：PascalCase
- 注释/文档字符串：中文

### Activity 开发规范
1. 所有 Activity 必须继承 BaseActivity[InputT, OutputT]
2. Input/Output 必须是 Pydantic 模型，设置 model_config = ConfigDict(extra="forbid")
3. 每个 Field 必须写 description（供 AI 生成层理解）
...

## Git 工作流
- 主分支：master
- 功能分支：feat/<feature-name>
- 提交信息格式：<type>: <description>
  - type: feat / fix / refactor / test / docs / chore
```

这份 CLAUDE.md 的好处在于：它只包含 Claude 无法从代码推断的信息——命名约定、提交规范、Activity 的特殊开发模式等。

**快速生成：** 如果你的项目还没有 CLAUDE.md，运行 `/init` 命令，Claude 会分析项目结构自动生成一份初始版本，然后你再精化。

#### 5.2 自定义命令（Slash Commands）

将团队的高频操作封装为命令，放在 `.claude/commands/` 目录下，所有人通过 `/命令名` 触发，执行一致。

**LegoFlow 的命令示例：**

| 命令              | 功能                       | 使用场景   |
| --------------- | ------------------------ | ------ |
| `/test`         | 运行测试（支持参数）               | 每次改完代码 |
| `/lint`         | 代码检查 + 格式化               | 提交前    |
| `/check`        | 全量检查（lint + type + test） | PR 前   |
| `/new-activity` | 脚手架生成新 Activity          | 新建能力时  |
| `/new-workflow` | 脚手架生成新 Workflow          | 新建编排时  |
| `/update-docs`  | 同步更新项目文档                 | 功能变更后  |

**命令文件格式：** 每个命令是一个 Markdown 文件，描述 Claude 应该执行的步骤。以 `/test` 为例：

```markdown
# 运行测试

根据参数运行不同范围的测试：

## 使用方式
- `/test` — 运行全部单元测试
- `/test <path>` — 运行指定路径的测试
- `/test integration` — 运行集成测试

## 执行步骤
1. 如果参数是 `integration`，运行：`pytest tests/ -m integration -v --timeout=120`
2. 如果参数是具体路径，运行：`pytest <path> -v --timeout=30`
3. 如果无参数，运行：`pytest tests/ -v --timeout=10`
4. 分析测试结果，报告通过/失败数量
5. 如果有失败，简要分析失败原因

$ARGUMENTS
```

`$ARGUMENTS` 是一个特殊变量，会被用户在 `/test` 后面输入的内容替换。

#### 5.3 权限配置

控制 Claude 可以/不可以执行的命令，既减少确认弹窗，又防止危险操作。

配置位置：`.claude/settings.local.json`

**LegoFlow 的配置示例（精简版）：**

```json
{
  "permissions": {
    "allow": [
      "Bash(pytest *)",
      "Bash(ruff *)",
      "Bash(git status*)",
      "Bash(git diff*)",
      "Bash(git log*)",
      "Bash(git add *)",
      "Bash(git commit *)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force*)",
      "Bash(git reset --hard*)"
    ]
  }
}
```

* **allow**：这些命令 Claude 可以直接执行，不再弹窗确认
* **deny**：这些命令被完全禁止，即使 Claude 想执行也会被阻止

**建议：** 团队约定一份基线权限配置提交到仓库，每个人可以在本地按需覆盖。

#### 5.4 Git Hooks 集成

CLAUDE.md 里的规则是"建议"——Claude 可能遵守，也可能忘记。Git hooks 是"强制"——必须每次发生的检查就用 hooks 保证。

**LegoFlow 的 pre-commit hook：**

```bash
#!/bin/bash
# 1. Ruff lint check
ruff check lego_flow/ tests/ --quiet

# 2. Ruff format check
ruff format --check lego_flow/ tests/ --quiet

# 3. Unit tests (fast)
python -m pytest tests/ -x -q --timeout=10
```

**关键点：** Claude 提交代码时也会触发这些 hooks。这意味着 AI 生成的代码也必须通过同样的质量关卡——lint 通过、格式正确、测试通过，才能被提交。

启用 hooks：

```bash
git config core.hooksPath .githooks
```

#### 5.5 Skills

CLAUDE.md 每次对话都加载，适合放通用规则。但有些知识不是每次都需要——比如"如何开发电商相关 Activity"或"如何部署到生产环境"。这些用 **Skills** 来管理。

Skills 放在 `.claude/skills/` 目录下，Claude 在相关时自动加载，也可以通过 `/skill-name` 手动触发。

```
.claude/skills/
└── api-conventions/
    └── SKILL.md
```

```markdown
---
name: api-conventions
description: REST API 设计规范
---

# API 规范
- URL 路径使用 kebab-case
- JSON 属性使用 camelCase
- 列表接口必须包含分页
```

**何时用 CLAUDE.md vs Skills：**

* 每次开发都需要知道的 → CLAUDE.md
* 只在特定场景需要的领域知识 → Skills

***

### 第 6 章：使用 Superpowers 规范化开发流程

#### 为什么需要 Superpowers

Claude Code 很强大，但也容易带来一个问题：**跳过思考直接动手**。

典型的失败模式是：

```
"帮我做一个 XX 功能" → Claude 直接开始写代码 → 方向不对 → 反复修改 → 浪费大量时间
```

Superpowers 是 Claude Code 的一个官方插件，它通过一套 **skill 工作流**，在关键节点强制插入思考和验证环节。核心理念两句话：

* **Brainstorming before building** — 先想清楚再动手
* **Verification before completion** — 拿到证据才算完

#### 关键 Skill 速览

Superpowers 的 skill 会在合适的时机自动触发（你也可以手动调用）：

| 你在做的事     | 触发的 Skill                        | 它会帮你做什么                             |
| --------- | -------------------------------- | ----------------------------------- |
| 要做一个新功能   | `brainstorming`                  | 逐一提问澄清需求，探索 2-3 种方案，确认后才动手          |
| 方案确定，准备实现 | `writing-plans`                  | 输出分步实现计划，明确每步改哪些文件、怎么测试             |
| 写功能代码     | `test-driven-development`        | 先写失败的测试，再写最小实现，确保代码有测试覆盖            |
| 遇到 bug    | `systematic-debugging`           | 按流程排查：复现 → 定位 → 假设 → 验证，避免瞎猜        |
| 觉得做完了     | `verification-before-completion` | 强制运行所有验证命令，看到通过的输出才宣布完成             |
| 准备合并      | `finishing-a-development-branch` | 引导你选择合并方式（直接 merge / 创建 PR / 清理后合并） |

#### 安装与启用

在 Claude Code 中运行：

```
/plugin
```

搜索 `superpowers` 并启用。或者直接在 `.claude/settings.local.json` 中配置：

```json
{
  "enabledPlugins": {
    "superpowers@claude-plugins-official": true
  }
}
```

#### 对团队的价值

* **一致性**：不论谁用 Claude Code，都走同样的"思考 → 计划 → 实现 → 验证"流程，不会出现有人深思熟虑、有人瞎写一气的情况
* **代码质量**：brainstorming 减少返工，TDD 保证测试覆盖，verification 杜绝"我觉得好了但其实没跑过测试"
* **知识沉淀**：brainstorming 产出设计文档、writing-plans 产出实现计划，都自动保存在 `docs/` 目录下，成为项目的可追溯记录

***

### 第 7 章：推荐 Plugin 与 Skill

Claude Code 拥有一个活跃的插件生态系统。通过 `/plugin` 命令可以浏览和安装插件，扩展 Claude 的能力。以下是我们推荐团队安装的插件和 skill。

#### 7.1 如何管理插件

```bash
# 浏览和安装插件（交互式界面）
/plugin

# 直接安装指定插件
/plugin install plugin-name@claude-plugins-official

# 安装后激活
/reload-plugins
```

安装范围：

* **User**：个人全局生效（默认）
* **Project**：所有协作者共享（写入 `.claude/settings.json`）
* **Local**：仅自己在当前项目生效

#### 7.2 代码智能（Code Intelligence）— 强烈推荐

代码智能插件为 Claude 启用 LSP（Language Server Protocol），让它获得**跳转定义、查找引用、编辑后自动检测类型错误**的能力。这不是"锦上添花"，而是质的飞跃——Claude 编辑文件后能立即看到引入的类型错误并自动修复。

| 语言         | 插件名                 | 需要的本地二进制                     |
| ---------- | ------------------- | ---------------------------- |
| Python     | `pyright-lsp`       | `pyright-langserver`         |
| TypeScript | `typescript-lsp`    | `typescript-language-server` |
| Go         | `gopls-lsp`         | `gopls`                      |
| Rust       | `rust-analyzer-lsp` | `rust-analyzer`              |
| Java       | `jdtls-lsp`         | `jdtls`                      |
| C/C++      | `clangd-lsp`        | `clangd`                     |

**LegoFlow 已启用 `pyright-lsp`**，这是 Python 项目的标配。

安装示例：

```bash
/plugin install pyright-lsp@claude-plugins-official
```

#### 7.3 开发流程插件

| 插件                    | 功能                                                                   | 推荐场景                |
| --------------------- | -------------------------------------------------------------------- | ------------------- |
| **superpowers**       | 规范化开发工作流（brainstorming、TDD、debugging 等）                              | 所有人（见第 6 章）         |
| **feature-dev**       | 7 阶段引导式功能开发（需求→探索→设计→实现→测试→审查→文档）                                    | 中大型功能开发             |
| **commit-commands**   | Git 提交工作流（commit、push、PR 创建）                                         | 日常提交                |
| **pr-review-toolkit** | 专业化 PR 审查 agent                                                      | Code Review         |
| **playwright**        | 让 Claude 操控浏览器进行 UI 测试和视觉验证                                          | 前端开发、E2E 测试、UI 截图对比 |
| **pencil**            | Figma 风格的无限画布设计工具，通过 MCP 将设计上下文直接传给 Claude 生成代码，设计文件（.pen）可纳入 git 管理 | UI/前端设计到代码的完整工作流    |
| **skill-creator**     | 引导式创建自定义 Skill（交互式问答生成 SKILL.md）                                     | 团队沉淀领域知识和可复用工作流     |

#### 7.4 外部集成插件

这些插件预配置了 MCP 服务器，让 Claude 能直接与外部服务交互：

| 类别   | 插件                            | 功能                 |
| ---- | ----------------------------- | ------------------ |
| 源码管理 | `github`、`gitlab`             | 操作 Issue、PR、Review |
| 项目管理 | `linear`、`notion`、`atlassian` | 读写任务、文档            |
| 设计   | `figma`                       | 获取设计稿信息            |
| 监控   | `sentry`                      | 查看错误和性能数据          |
| 基础设施 | `vercel`、`supabase`           | 部署和数据库操作           |

按需安装。例如团队用 GitHub + Linear：

```bash
/plugin install github@claude-plugins-official
/plugin install linear@claude-plugins-official
```

#### 7.5 推荐 MCP Server

MCP（Model Context Protocol）让 Claude 能连接外部工具和数据源。除了通过插件安装，也可以手动配置：

| MCP Server   | 功能                    | 推荐理由                      |
| ------------ | --------------------- | ------------------------- |
| **Context7** | 实时获取第三方库的最新文档和 API 签名 | 防止 Claude 生成过时或错误的 API 调用 |

#### 7.6 团队统一配置建议

建议在项目的 `.claude/settings.json` 中预配置团队共享的插件：

```json
{
  "enabledPlugins": {
    "superpowers@claude-plugins-official": true,
    "pyright-lsp@claude-plugins-official": true
  }
}
```

这样团队成员 clone 项目后，Claude Code 会自动提示安装这些插件。

***

### 第 8 章：进阶技巧

#### 8.1 Context 管理 — 最重要的隐性技能

Claude 的上下文窗口（context window）保存了整个对话中的所有内容——你的每条消息、Claude 读取的每个文件、每条命令的输出。**这是最宝贵的资源，填满后 Claude 的表现会明显下降。**

**关键操作：**

| 操作    | 快捷方式/命令                 | 使用场景              |
| ----- | ----------------------- | ----------------- |
| 清空上下文 | `/clear`                | 切换到不相关的任务时        |
| 压缩对话  | `/compact`              | 对话变长，想保留关键信息但释放空间 |
| 中途停止  | `Esc`                   | Claude 走偏了，立即打断   |
| 回退检查点 | `Esc + Esc` 或 `/rewind` | 想撤销 Claude 刚才的操作  |
| 侧边问题  | `/btw`                  | 快速问个小问题，不污染主对话上下文 |

**三个反模式要避免：**

1. **"厨房水槽会话"**：一个会话里干多件不相关的事 → 任务切换时用 `/clear`
2. **"反复纠正"**：同一问题改了两次还不对 → `/clear` 后用更好的提示重新开始
3. **"无限探索"**：让 Claude 调查但不限范围 → 限定范围或用 subagent

#### 8.2 Plan Mode — 先想清楚再动手

Plan Mode 下 Claude 只读取文件和回答问题，**不做任何修改**。适合在动手前先搞清楚状况。

**什么时候用：** 改多个文件、不确定方案、不熟悉的代码区域

**什么时候不用：** 改一行代码、修拼写、加一条日志

**典型工作流：**

```
1. [Plan Mode]  读取相关代码，理解现状
2. [Plan Mode]  讨论方案，确认实现计划
3. [Normal Mode] 按计划实现代码
4. [Normal Mode] 运行测试验证
5. [Normal Mode] 提交
```

按 `Shift+Tab` 在 Plan Mode 和 Normal Mode 之间切换。

#### 8.3 并行会话 — 成倍提效

Anthropic 工程师 Boris Cherny 的做法：同时开 5 个 Claude 实例并行工作，每天产出 20-30 个 PR。你不需要这么极端，但并行 2-3 个会话确实能显著提升效率。

**典型场景：**

* 一个会话写功能，另一个会话写测试
* 一个会话实现代码，另一个会话 review
* 多个独立任务各开一个会话并行推进

**操作：** 打开多个终端 tab，每个 tab 运行 `claude` 即可。

**会话管理：**

```bash
claude --continue    # 恢复最近的会话
claude --resume      # 从最近的会话列表中选择
```

在会话中运行 `/rename oauth-migration` 给会话起个好名字，方便以后找到它。

#### 8.4 Subagents — 保护主上下文

Subagent 在独立的上下文窗口中工作，完成后只返回摘要给你的主对话。适合"消耗大量上下文"的任务：

```
用 subagent 审查这段代码的安全性
```

```
用 subagent 调查项目中所有的 API 端点，列出每个端点的路径、方法和用途
```

这样你的主对话保持干净，不会被大量文件内容填满。

#### 8.5 非交互模式 — 集成到自动化流程

`claude -p "提示"` 可以在不启动交互会话的情况下执行任务，适合集成到脚本和 CI/CD：

```bash
# 单次执行
claude -p "分析这个项目的依赖是否有安全漏洞"

# 结构化输出（方便脚本解析）
claude -p "列出所有 API 端点" --output-format json

# 流式输出
claude -p "分析这份日志" --output-format stream-json
```

***

### 第 9 章：常见问题与避坑

#### FAQ

| 问题                     | 解决方案                                                                                |
| ---------------------- | ----------------------------------------------------------------------------------- |
| Claude 生成的代码风格和项目不一致   | 检查 CLAUDE.md 是否写了代码风格规则；用 `@文件路径` 指向参考文件让 Claude 对齐                                 |
| Claude 一直在读文件，上下文快满了   | 限定范围（"只看 src/auth/ 目录"）或用 subagent 做调查                                              |
| Claude 反复犯同一个错误        | 把规则写进 CLAUDE.md；如果已经写了还犯，可能文件太长规则被淹没了，精简它                                           |
| 权限弹窗太多太烦               | 在 `.claude/settings.local.json` 中配置 allow 列表                                        |
| Claude 改了不该改的文件        | 在提示中明确范围（"只修改 X 文件"）；配 deny 列表禁止危险操作；用 `/rewind` 回退                                 |
| 如何让团队共享 Claude Code 配置 | CLAUDE.md + `.claude/commands/` + `.githooks/` 提交到 git，`settings.local.json` 按需本地覆盖 |

#### 避坑清单

1. **不要在一个会话里干太多不相关的事** — 任务切换时 `/clear`
2. **不要给模糊指令然后期待完美结果** — 具体的提示 = 更少的返工
3. **不要让 CLAUDE.md 膨胀** — 定期审视，删掉 Claude 不需要的规则
4. **不要跳过验证** — 每次让 Claude 改完代码，都要求它运行测试/lint 确认
5. **不要忽略 context 消耗** — 关注上下文使用量，及时 `/clear` 或 `/compact`
6. **迁移要做就做完** — 半迁移的代码库（两套框架并存）对人和 AI 都是灾难

#### 获取帮助

* 在 Claude Code 中运行 `/help` 查看帮助
* 官方文档：https://code.claude.com/docs/zh-CN
* 官方最佳实践：https://code.claude.com/docs/zh-CN/best-practices
* 问题反馈：https://github.com/anthropics/claude-code/issues
