---
description: xulin
icon: engine
---

# 从 Vibe Coding 到 Agentic Engineering：学会像智能体一样看世界

> 这不是一篇工具教程，而是一次思维方式的升级。 在你打开 Claude Code 之前，先理解你即将扮演的新角色。

***

### 一、一个词的变迁：从"氛围"到"工程"

2025 年初，OpenAI 联合创始人 Andrej Karpathy 发了一条推文，创造了 **Vibe Coding** 这个词：

> "你完全沉浸在氛围里，拥抱指数级增长，忘掉代码的存在。你只管提示、接受、运行，看看能不能跑起来。如果不行，就把错误贴回去再试一次。"

这个词一夜爆红。它精准描述了一种新型开发体验——你不写代码，你跟 AI 聊天；你不调试，你贴错误信息让 AI 猜；你不做设计，你让 AI 直接干。

一年后的 2026 年初，同一个 Karpathy 提出了一个新词：**Agentic Engineering**。

为什么要换词？因为 "vibe" 这个词承载了太多随意的含义。当你告诉 CTO 你在 "vibe 他们的支付系统" 时，你能看到他脸上的担忧。

但这不只是换个好听的名字。**这是两种根本不同的工作方式。**

***

### 二、两种范式的本质区别

|            | Vibe Coding | Agentic Engineering       |
| ---------- | ----------- | ------------------------- |
| **你的角色**   | 提需求的人       | 架构师 + 监工                  |
| **AI 的角色** | 魔法黑箱        | 快速但不可靠的初级工程师              |
| **对代码的态度** | "能跑就行，我不看"  | "每一行 diff 都要过眼"           |
| **出错时**    | 把错误贴回去再试    | 分析根因，给出约束条件后重试            |
| **质量保障**   | 无           | 测试、lint、code review、hooks |
| **适用场景**   | 原型、脚本、学习    | 生产系统、团队协作                 |

Addy Osmani（Chrome 团队工程负责人）说得直白：

> "把 AI 当作一个速度很快但不靠谱的初级开发者——它需要持续的监督。"

**Vibe Coding 不是错的**——它适合原型、个人脚本、学习场景。问题在于很多人把 Vibe Coding 的习惯带进了生产环境。这就像拿草稿纸上的计算去盖楼。

***

### 三、新角色：从"写代码的人"到"指挥 Agent 的人"

Anthropic 的 2026 Agentic Coding Trends Report 揭示了一个关键转变：

> 工程师的角色正在从"代码创作者"转变为"代码策展人"。

这意味着什么？

#### 旧模式：你 = 执行者

```
需求 → 你设计 → 你写代码 → 你调试 → 你测试 → 你提交
```

所有步骤都是你在做，AI 最多帮你补全几行。

#### 新模式：你 = 指挥官

```
需求 → 你设计架构 → Agent 写代码 → 你审查 → Agent 修复 → 你验收
       你定义约束    Agent 写测试    你判断质量   Agent 迭代    你负最终责任
```

你的核心工作变成了三件事：**委派（Delegate）、审查（Review）、负责（Own）**。

这不是降低了对工程师的要求，恰恰相反——Osmani 指出：

> "Agentic Engineering 实际上比传统编码更奖励好的工程实践。基本功成了前提条件，不再是锦上添花。"

高级工程师能获得 2 倍、5 倍甚至更高的效率提升，因为他们**知道好的代码长什么样**。而初级工程师如果跳过基本功，会陷入一种危险的"技能萎缩"——产出自己无法理解的代码。

***

### 四、Agent 的"脾气"：理解它才能驾驭它

AI Agent 不是人，也不是传统工具。它有独特的行为模式，你需要了解它的"脾气"才能高效协作。

#### 脾气一：上下文窗口是它的工作记忆

Agent 的上下文窗口就像人的工作记忆——有限、会满、满了就糊涂。当你在一个会话里塞入太多不相关的内容时，它会开始"遗忘"早期的指令，输出质量下降。

**应对方式：** 一事一议，频繁 `/clear`。别让 Agent 同时记住太多事。

#### 脾气二：它是一个"自信的猜测者"

Agent 不会说"我不确定"。它会用流畅的语言给你一个看起来很合理的答案——即使它完全编造了。这在编程中特别危险：一段看起来正确但实际有隐藏 bug 的代码，比明显的错误更危险。

**应对方式：** 永远要求验证。不是"你觉得对吗"，而是"运行测试给我看结果"。

#### 脾气三：具体指令远比模糊意图有效

Agent 处理"在 lego\_flow/activities/data/ 下新建一个 Activity，参考 sql\_query.py 的模式"的效果，远远好于"写一个处理数据的功能"。

这不是 Agent 笨——而是它的工作方式决定了：越具体的约束 = 越小的搜索空间 = 越高的命中率。

**应对方式：** 提供约束三要素——**做什么、在哪做、参考什么**。

#### 脾气四：它对代码质量敏感

CodeScene 的研究证实：**AI 在健康的代码库中表现最好，在混乱的代码库中和人一样容易犯错。** 半迁移的代码库（两套框架并存）、命名不一致的函数、缺乏测试的模块——这些都会显著降低 Agent 的输出质量。

Armin Ronacher（Flask 作者）的建议更具体：

> "做最简单的可行方案。偏好清晰、描述性、更长的函数名而非类。避免继承和巧妙的 hack。"

**应对方式：** 在让 Agent 工作之前，先确保代码库本身是健康的。好的工程实践会放大 Agent 的效果。

#### 脾气五：它的速度会放大好决策和坏决策

CodeScene 的核心洞察：

> "速度同时放大好的设计和坏的决策。"

Agent 写代码非常快，这意味着一个错误的架构决策会在几分钟内蔓延到十几个文件。传统开发中，慢速度本身就是一道安全阀——你有时间在写到第三个文件时意识到方向不对。Agent 没有这个安全阀。

**应对方式：** 先规划，再动手。在 Agent 开始写代码之前，确保架构方向是对的。

***

### 五、培养 Agent 思维：六个核心心智模型

#### 心智模型一：你是架构师，不是打字员

**旧思维：** "我来写代码" **Agent 思维：** "我来定义目标、约束和验收标准，Agent 来实现"

最大的思维跃迁是：你的产出不再是代码，而是**高质量的意图表达**。一个好的提示（prompt）比手写实现更有价值，因为它可以被 Agent 反复执行和迭代。

#### 心智模型二：测试是你的权力之源

没有测试，你就无法验证 Agent 的产出。你会陷入"看起来对但不确定"的泥潭。

有了测试，你可以大胆地委派——因为错误会被自动捕获。Simon Willison 在 Agentic Engineering Patterns 中将 TDD 列为 Agent 时代的核心模式：

> "测试优先方法帮助 Agent 以最少的额外提示写出更简洁可靠的代码。"

**行动转化：** 先写测试（或让 Agent 写），再让 Agent 写实现，再运行验证。这就是 Superpowers 的 `test-driven-development` skill 所做的事。

#### 心智模型三：先想后做，永远如此

Vibe Coding 最大的问题不是 AI 导致的——是跳过了设计思考。Osmani 的原话：

> "AI 没有导致问题；跳过设计思考才是问题所在。"

Agent 放大了这一点：它写代码太快了，如果方向错了，返工的规模也会很大。

**行动转化：** 任何超过 5 分钟的任务，都先进入 Plan Mode 或触发 brainstorming。

#### 心智模型四：给 Agent 铺轨道，而不是画地图

CLAUDE.md、自定义命令、hooks、skills——这些不是"配置文件"，它们是你为 Agent 铺设的铁轨。

Agent 在轨道上跑得又快又稳。没有轨道，它会四处乱跑。

Armin Ronacher 的实践佐证了这一点：他为 Agent 设计了快速响应的 Makefile、清晰的日志系统、防止重复启动的 pidfile。这些"基础设施"让 Agent 能自主诊断和解决问题。

**行动转化：** 投入时间配置你的项目环境。每一条写进 CLAUDE.md 的规则，都是 Agent 未来每次执行时的"免费生产力"。

#### 心智模型五：委派的粒度决定产出质量

Anthropic 报告中的数据：开发者在 60% 的工作中集成了 AI，但对 80-100% 的委派任务保持主动监督。

关键不是"能不能全交给 Agent"，而是"交给它多大一块"。

* 太大（"帮我做完整个功能"）→ Agent 容易走偏，纠错成本高
* 太小（"帮我写这一行"）→ 退化成 Copilot，浪费 Agent 的能力
* 刚好（"实现这个模块，参考这个模式，写完跑测试"）→ 可验证、可迭代

**行动转化：** 分解到你能自信验证产出的最小单元。

#### 心智模型六：并行是超能力

Boris Cherny（Anthropic 工程师）同时开 5 个 Claude 实例。Anthropic 报告指出多 Agent 协调正在从单 Agent 工作流转向"多个专业 Agent 在编排器下并行工作"。

你不需要一次做一件事。你可以：一个会话写功能，一个会话写测试，一个会话做 review——像管理一个小团队。

**行动转化：** 从今天开始，尝试同时开两个会话处理独立任务。

***

### 六、Agentic Engineering 的工作节奏

把上面的心智模型串起来，一个完整的 Agentic Engineering 工作流长这样：

```
┌─────────────────────────────────────────────────────┐
│  1. 理解需求                                          │
│     └─ 用 Agent 做调研，问问题，澄清模糊点               │
├─────────────────────────────────────────────────────┤
│  2. 设计方案                                          │
│     └─ brainstorming：探索 2-3 种方案，选定方向           │
├─────────────────────────────────────────────────────┤
│  3. 制定计划                                          │
│     └─ writing-plans：分步骤、分文件、明确验证方式         │
├─────────────────────────────────────────────────────┤
│  4. 委派实现                                          │
│     └─ 按计划逐步委派，每步都有测试验证                    │
│        可并行：一个 Agent 写功能，一个写测试               │
├─────────────────────────────────────────────────────┤
│  5. 审查验收                                          │
│     └─ 审查每个 diff，运行全量检查，确认质量               │
├─────────────────────────────────────────────────────┤
│  6. 交付                                             │
│     └─ 提交、创建 PR、文档更新                          │
└─────────────────────────────────────────────────────┘
```

注意这个流程和传统的软件工程流程几乎一样——**唯一的变化是"谁在执行"**。方案是你定的，计划是你审的，质量是你把关的，最终责任是你的。Agent 只是让执行环节变得飞快。

这就是为什么 Osmani 说"Agentic Engineering 比传统编码更奖励好的工程实践"——因为它没有绕过工程，它加速了工程。

***

### 七、给团队的行动建议

#### 今天就可以做的

1. **装好 Claude Code，跑一遍入门指南**——先有手感
2. **在你的项目里配好 CLAUDE.md**——给 Agent 铺第一段铁轨
3. **养成"先想后做"的习惯**——任何超过 5 分钟的任务，先 Plan Mode

#### 一周内建立的习惯

4. **每次委派都要求验证**——"写完跑测试"成为肌肉记忆
5. **用 `/clear` 管理上下文**——切换任务时清空，保持 Agent 专注
6. **开始尝试并行会话**——两个终端，两个独立任务

#### 持续修炼的能力

7. **提升意图表达能力**——具体、有约束、指向参考模式
8. **培养"审查眼"**——Agent 写的代码，你要能判断好坏
9. **学会分解任务**——找到"够大不浪费、够小能验证"的粒度

***

### 写在最后

Vibe Coding 让所有人都能开始和 AI 一起写代码。这是它的贡献。

但从 Vibe Coding 到 Agentic Engineering 的跨越，不是学一个新工具的事——**是学会一种新的工作方式**。

你不再是那个亲手写每一行代码的人。你是定义目标的人、设计约束的人、判断质量的人、承担最终责任的人。Agent 是你的执行团队，但你是 tech lead。

这种转变一开始会不舒服。你会觉得"让 AI 写不如我自己写快"。但一旦你建立了好的工作模式——配置好环境、养成先想后做的习惯、学会恰当粒度的委派——你会发现自己能做到过去做不到的事。

不是因为 AI 替你写了代码，而是因为**你学会了以工程的方式驾驭 AI**。

***

### 参考资料

* [Addy Osmani - Agentic Engineering](https://addyosmani.com/blog/agentic-engineering/)
* [Armin Ronacher - Agentic Coding Recommendations](https://lucumr.pocoo.org/2025/6/12/agentic-coding/)
* [Simon Willison - Agentic Engineering Patterns](https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/)
* [Anthropic - 2026 Agentic Coding Trends Report](https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf)
* [CodeScene - Agentic AI Coding: Best Practice Patterns](https://codescene.com/blog/agentic-ai-coding-best-practice-patterns-for-speed-with-quality)
* [The New Stack - From Vibes to Engineering](https://thenewstack.io/vibe-coding-agentic-engineering/)
* [Sau Sheong - From Vibe Coding to Agentic Engineering](https://sausheong.com/from-vibe-coding-to-agentic-engineering-1ca3ca72b5ac)
* [IBM - What is Agentic Engineering](https://www.ibm.com/think/topics/agentic-engineering)
* [Anthropic: 8 Agentic Coding Trends Shaping Software Engineering in 2026](https://tessl.io/blog/8-trends-shaping-software-engineering-in-2026-according-to-anthropics-agentic-coding-report/)
