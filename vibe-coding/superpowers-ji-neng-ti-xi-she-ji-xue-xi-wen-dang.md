---
description: xulin
icon: car-battery
---

# Superpowers 技能体系设计学习文档

> 基于 superpowers v4.3.1 全部 15 个技能的深度分析

***

### 一、体系总览

Superpowers 是一套为 Claude Code (AI 编程代理) 设计的**软件工程方法论技能系统**。它不是工具集合，而是一套**将人类软件工程最佳实践编码为 AI 可执行流程**的框架。

#### 1.1 技能清单与分类

| 类别        | 技能名                            | 核心职责                        |
| --------- | ------------------------------ | --------------------------- |
| **入口/路由** | using-superpowers              | 会话启动时的技能发现与调度               |
| **设计阶段**  | brainstorming                  | 将想法转化为设计文档                  |
| **计划阶段**  | writing-plans                  | 将设计转化为可执行的实施计划              |
| **环境准备**  | using-git-worktrees            | 创建隔离工作空间                    |
| **执行阶段**  | executing-plans                | 批量执行计划（独立会话）                |
| **执行阶段**  | subagent-driven-development    | 子代理驱动开发（当前会话）               |
| **执行阶段**  | dispatching-parallel-agents    | 并行调度多个独立任务                  |
| **质量保障**  | test-driven-development        | 测试驱动开发 (RED-GREEN-REFACTOR) |
| **质量保障**  | systematic-debugging           | 系统化调试（根因分析优先）               |
| **质量保障**  | verification-before-completion | 完成前验证（证据先于断言）               |
| **评审阶段**  | requesting-code-review         | 请求代码评审                      |
| **评审阶段**  | receiving-code-review          | 接收代码评审反馈                    |
| **收尾阶段**  | finishing-a-development-branch | 分支收尾（合并/PR/保留/丢弃）           |
| **元技能**   | writing-skills                 | 创建新技能（技能的 TDD）              |

#### 1.2 完整开发流水线

```
using-superpowers (路由)
    │
    ▼
brainstorming (设计)
    │ 输出: docs/plans/YYYY-MM-DD-<topic>-design.md
    ▼
writing-plans (计划)
    │ 输出: docs/plans/YYYY-MM-DD-<feature-name>.md
    ▼
using-git-worktrees (环境)
    │ 输出: 隔离的 worktree 工作空间
    ▼
┌───────────────────────────────────┐
│ 选择执行模式:                      │
│  A) subagent-driven-development   │
│     (当前会话, 子代理逐任务)        │
│  B) executing-plans               │
│     (独立会话, 批量执行)            │
│  C) dispatching-parallel-agents   │
│     (并行处理独立问题)              │
└───────────────────────────────────┘
    │ 贯穿: test-driven-development
    │ 贯穿: systematic-debugging
    │ 贯穿: verification-before-completion
    │ 贯穿: requesting/receiving-code-review
    ▼
finishing-a-development-branch (收尾)
    │ 选项: 合并 / PR / 保留 / 丢弃
    ▼
完成
```

***

### 二、核心设计模式分析

#### 2.1 Iron Law 模式（铁律模式）

**出现频率:** 4/15 个技能使用了此模式

这是 superpowers 体系最具标志性的设计手法。用**不可违反的绝对规则**来锚定代理行为的底线。

| 技能                             | Iron Law                                                   |
| ------------------------------ | ---------------------------------------------------------- |
| test-driven-development        | `NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST`          |
| systematic-debugging           | `NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST`          |
| verification-before-completion | `NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE` |
| writing-skills                 | `NO SKILL WITHOUT A FAILING TEST FIRST`                    |

**设计意图：**

* LLM 在压力下（时间紧迫、沉没成本、看似简单）倾向于走捷径
* Iron Law 作为**硬性门控**，在认知偏差出现前就阻断错误路径
* 措辞刻意使用全大写 + 代码块格式，增强视觉权重

**为什么有效：** Iron Law 利用了 LLM 对明确指令的高度服从性。比起"尽量先写测试"这种柔性建议，"没有失败的测试就不能写生产代码"的绝对约束被违反的概率显著降低。

#### 2.2 反合理化表格模式（Rationalization Table）

**出现频率:** 5/15 个技能

这是针对 LLM 的**心理防御机制**设计。LLM 会生成看似合理的借口来绕过规则，superpowers 预先列举并逐一反驳。

```
| Excuse                        | Reality                                       |
|-------------------------------|-----------------------------------------------|
| "Too simple to test"          | Simple code breaks. Test takes 30 seconds.    |
| "I'll test after"             | Tests passing immediately prove nothing.      |
| "TDD will slow me down"       | TDD faster than debugging.                    |
```

**设计原理：**

1. **预测性反驳** — 不等 LLM 产生借口再纠正，而是提前占据认知空间
2. **格式选择** — 表格比段落更容易被扫描匹配，LLM 在生成借口时更容易"命中"已列出的条目
3. **语气设计** — Reality 列使用简短、断言式的语句，而非说教性的长解释

**这是 Superpowers 体系最具创造性的设计之一** — 它本质上是在给 AI 做"认知免疫接种"。

#### 2.3 Red Flags 模式（红旗自检）

**出现频率:** 6/15 个技能

与 Rationalization Table 互补，Red Flags 提供了一个**实时自检清单**，让代理在行为发生时（而非事后）识别违规倾向。

```
## Red Flags - STOP and Start Over
​
- Code before test
- Test passes immediately
- "I already manually tested it"
- "This is different because..."
​
**All of these mean: Delete code. Start over with TDD.**
```

**设计特征：**

* 使用 bullet list 而非表格 — 优化扫描速度
* 每条都以具体的**思维特征**或**行为特征**描述 — 不是抽象原则
* 结尾统一给出**明确动作** — "STOP and Start Over"

#### 2.4 Gate Function 模式（门控函数）

**出现频率:** 3/15 个技能

将流程控制点表达为**伪代码门控条件**，强制代理在满足条件前不能继续。

```
# verification-before-completion
BEFORE claiming any status:
1. IDENTIFY: What command proves this claim?
2. RUN: Execute the FULL command
3. READ: Full output, check exit code
4. VERIFY: Does output confirm the claim?
   - If NO: State actual status
   - If YES: State claim WITH evidence
```

```
# brainstorming
HARD-GATE: Do NOT invoke any implementation skill
until you have presented a design and the user has approved it.
```

**设计意图：**

* LLM 天然理解代码逻辑，用代码格式表达流程控制比自然语言更精确
* Gate Function 是 Iron Law 的**可执行版本** — 不仅说"不要"，还说"按这个顺序做"

#### 2.5 Graphviz 流程图模式

**出现频率:** 8/15 个技能

使用 `dot` 语法的 Graphviz 图来表达决策流程和状态转换。

```
digraph tdd_cycle {
    red -> verify_red;
    verify_red -> green [label="yes"];
    verify_red -> red [label="wrong failure"];
    green -> verify_green;
    ...
}
```

**设计选择分析：**

* **为什么用 Graphviz 而不是 Mermaid？** — Graphviz 的 `dot` 语法更紧凑，且 LLM 对其解析更可靠
* **为什么不用纯文本流程？** — 图形化表达能让 LLM 更准确地理解**分支条件**和**循环回路**
* **使用场景限定** — writing-skills 明确指出：只在"决策非显而易见"时使用流程图，线性流程用编号列表

#### 2.6 技能链接模式（Skill Chaining）

技能之间通过标准化的链接声明建立依赖关系：

```
**REQUIRED SUB-SKILL:** Use superpowers:test-driven-development
**REQUIRED BACKGROUND:** You MUST understand superpowers:systematic-debugging
```

**链接类型：**

| 标记                    | 含义           | 举例                                               |
| --------------------- | ------------ | ------------------------------------------------ |
| `REQUIRED SUB-SKILL`  | 必须在此技能执行中调用  | executing-plans → finishing-a-development-branch |
| `REQUIRED BACKGROUND` | 必须先理解再使用当前技能 | writing-skills → test-driven-development         |
| `Integration` 段落      | 描述协作关系       | using-git-worktrees ← brainstorming (调用方)        |

**关键设计决策：** 使用文本引用而非 `@` 文件链接。writing-skills 明确解释：`@` 语法会立即加载文件消耗 context，而文本引用让 LLM 按需加载。

***

### 三、关键设计原则深度解析

#### 3.1 "假设工程师零上下文"原则

writing-plans 技能开篇就声明：

> Write comprehensive implementation plans assuming the engineer has zero context for our codebase and questionable taste.

**这直接指向 LLM 代理的核心挑战：**

* 每个子代理 (subagent) 都是一个**无状态的新实例**
* 不能假设它"记得"之前的决策
* 计划必须包含**精确文件路径、完整代码、确切命令**

这就是为什么 writing-plans 要求每一步都是 2-5 分钟的原子操作，而不是模糊的"实现验证功能"。

#### 3.2 "两阶段评审"原则

subagent-driven-development 实现了独特的**双阶段代码评审**：

```
实现者子代理 → 规格合规评审 → 代码质量评审
                    ↑ 不通过则返回      ↑ 不通过则返回
```

**为什么分两阶段而不是一次评审？**

1. **规格合规** — "做对了吗？" (功能正确性)
2. **代码质量** — "做好了吗？" (实现质量)

这避免了评审者同时关注两个维度导致的遗漏。每个维度有独立的 prompt 模板和评判标准。

#### 3.3 "证据先于断言"原则

verification-before-completion 的核心哲学：

```
✅ [Run test command] [See: 34/34 pass] "All tests pass"
❌ "Should pass now" / "Looks correct"
```

**失败案例驱动：** 这个技能引用了 24 个真实失败记忆，包括：

* "I don't believe you" — 信任被打破
* 未定义函数被发布 — 运行时崩溃
* 缺失需求被发布 — 功能不完整

这体现了 superpowers 的另一个设计原则：**用真实失败案例证明规则的必要性**。

#### 3.4 "不要表演性认同"原则

receiving-code-review 的禁止响应列表极为独特：

```
**NEVER:**
- "You're absolutely right!"
- "Great point!" / "Excellent feedback!"
- "Thanks for catching that!"
​
**INSTEAD:**
- Just fix it and show in the code
```

**这解决了 LLM 的一个系统性问题：** 讨好倾向 (sycophancy)。LLM 天然倾向于过度认同用户，这在代码评审场景中是危险的 — 它可能盲目实现错误的建议而不加质疑。

***

### 四、架构设计洞察

#### 4.1 状态机架构

整个 superpowers 体系可以建模为一个**有限状态机**：

```
         ┌─────────────────────────────────────┐
         │          DESIGN PHASE               │
         │  brainstorming → writing-plans      │
         └──────────────┬──────────────────────┘
                        │
         ┌──────────────▼──────────────────────┐
         │         SETUP PHASE                 │
         │  using-git-worktrees                │
         └──────────────┬──────────────────────┘
                        │
         ┌──────────────▼──────────────────────┐
         │       EXECUTION PHASE               │
         │  subagent-driven / executing-plans   │
         │  + TDD + debugging + verification   │
         │  + code-review (request/receive)    │
         └──────────────┬──────────────────────┘
                        │
         ┌──────────────▼──────────────────────┐
         │       COMPLETION PHASE              │
         │  finishing-a-development-branch      │
         └─────────────────────────────────────┘
```

**每个阶段都有明确的入口条件和出口产物：**

| 阶段 | 入口条件      | 出口产物       |
| -- | --------- | ---------- |
| 设计 | 用户想法/需求   | 设计文档 (.md) |
| 计划 | 设计文档      | 实施计划 (.md) |
| 环境 | 实施计划      | 隔离工作空间     |
| 执行 | 计划 + 工作空间 | 通过测试的代码    |
| 收尾 | 通过测试的代码   | 合并/PR/保留   |

#### 4.2 横切关注点 (Cross-Cutting Concerns)

三个技能贯穿整个执行阶段，不属于任何特定步骤：

* **test-driven-development** — 每个实现步骤都遵循 RED-GREEN-REFACTOR
* **systematic-debugging** — 任何失败都走四阶段调试流程
* **verification-before-completion** — 任何完成声明都需要证据

这类似于面向切面编程 (AOP) 中的横切关注点 — 它们不是流水线的某个阶段，而是在每个阶段中都起作用的约束。

#### 4.3 元技能设计 (Meta-Skill)

writing-skills 是整个体系中最特殊的技能 — 它是**用于创建其他技能的技能**，且自身遵循与 TDD 完全相同的方法论：

```
TDD 写代码:     写失败测试 → 看它失败 → 写最少代码 → 看它通过 → 重构
TDD 写技能:     写压力场景 → 看代理违规 → 写最少文档 → 看代理合规 → 堵漏洞
```

**这个递归应用创造了一个自引用的质量保证循环：**

* writing-skills 本身是一个技能，它教你如何创建技能
* 它要求你用 TDD 来测试技能，而 TDD 本身也是一个用同样方法创建的技能
* 这保证了整个体系的自洽性

***

### 五、CSO (Claude Search Optimization) — 独创概念

writing-skills 引入了一个有趣的概念：**Claude 搜索优化 (CSO)**，类比 SEO。

#### 核心发现

> Testing revealed that when a description summarizes the skill's workflow, Claude may follow the description instead of reading the full skill content.

**这揭示了 LLM 工具调用的一个微妙行为：**

* description 字段被注入到系统提示中
* 如果 description 包含了流程摘要，LLM 可能直接按摘要行动
* 而不去读取完整的 SKILL.md 内容

**解决方案：** description 只描述**何时触发**，绝不描述**怎么做**：

```
# 错误: 暴露了流程
description: Use when executing plans - dispatches subagent per task with code review between tasks
​
# 正确: 只描述触发条件
description: Use when executing implementation plans with independent tasks in the current session
```

***

### 六、设计模式速查表

| 模式                        | 目的             | 使用场景          |
| ------------------------- | -------------- | ------------- |
| **Iron Law**              | 设定不可违反的底线      | 核心纪律类技能       |
| **Rationalization Table** | 预先反驳 LLM 的常见借口 | 容易被绕过的规则      |
| **Red Flags**             | 实时行为自检         | 执行过程中的偏差识别    |
| **Gate Function**         | 用伪代码控制流程       | 严格的顺序依赖       |
| **Graphviz Flow**         | 可视化决策逻辑        | 非显而易见的分支决策    |
| **Skill Chaining**        | 技能间依赖声明        | 多技能协作流水线      |
| **Good/Bad 对比**           | 用具体例子示范        | 编码风格和实践       |
| **Announce Pattern**      | 技能启动时的自我声明     | 让用户知道正在使用什么流程 |
| **Checklist Pattern**     | 完成前的验证清单       | 质量关卡          |
| **Real-World Impact**     | 用数据证明价值        | 说服性段落         |

***

### 七、可借鉴的设计智慧

#### 7.1 给 AI 写 "流程文档" 的核心法则

1. **绝对规则 > 柔性建议** — LLM 对 "NEVER" 的遵从度远高于 "try to avoid"
2. **预测性反驳 > 事后纠正** — 不要等 LLM 犯错再教它，提前列出所有可能的借口
3. **代码格式 > 自然语言** — 用伪代码和流程图表达约束，比文字描述更精确
4. **具体行为 > 抽象原则** — "删除代码，从头开始" 比 "保持测试优先" 更有效
5. **真实案例 > 理论说教** — "24 个失败记忆" 比 "验证很重要" 更有说服力

#### 7.2 对比传统文档的差异

| 维度   | 传统文档 (给人类) | Superpowers (给 AI) |
| ---- | ---------- | ------------------ |
| 假设读者 | 有经验、有判断力   | 零上下文、会合理化          |
| 规则表达 | 指导性、弹性的    | 绝对性、不可违反的          |
| 反面案例 | 偶尔提及       | 系统性列举 + 逐条反驳       |
| 流程控制 | 隐含在文字中     | 显式的状态机/门控函数        |
| 验证方式 | 靠人类判断      | 要求可执行的证据           |
| 自检机制 | 无          | Red Flags 清单       |

#### 7.3 体系设计的哲学基础

Superpowers 体系隐含了几个深层假设：

1. **AI 代理是"聪明但不可靠的初级工程师"** — 它们能力强但缺乏纪律，需要严格的流程约束
2. **流程纪律不是束缚而是加速器** — 系统化调试 15-30 分钟 vs 随机修复 2-3 小时
3. **文档即代码** — 技能文档应该用 TDD 来测试，就像代码一样
4. **最小权限原则** — 每个子代理只应知道执行当前任务所需的最少信息
5. **信任但验证** — 接受外部反馈但要先技术验证，接受自身判断但要先跑测试

***

### 八、总结

Superpowers 的核心创新不在于它教了什么技术，而在于它**如何教 AI 代理遵守纪律**。 它证明了一个重要的洞察：

> 给 AI 编程代理写流程文档，不是在写"参考手册"， 而是在写"行为约束系统"。

这套体系的设计者深刻理解 LLM 的两个特性：

* **能力强但纪律差** — 需要 Iron Law 和 Gate Function
* **善于合理化** — 需要 Rationalization Table 和 Red Flags

每个技能都是对 LLM 行为弱点的精准回应，而整个体系构成了一个**自洽、可测试、可扩展**的软件工程方法论框架。

***

_文档生成日期: 2026-03-06_ _分析对象: superpowers v4.3.1 (15 个技能)_
