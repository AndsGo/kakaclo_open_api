# OpenClaw(Clawdbot)快速接入Discord指南

原文 [https://cloud.tencent.com/developer/article/2626068](https://cloud.tencent.com/developer/article/2626068)\
本文是 OpenClaw 接入 Discord 的完整配置步骤，可直接衔接你已完成的OpenClaw服务器部署流程，全程在 Discord 开发者平台 + 云服务器 SSH 终端操作，核心是创建 Discord Bot、配置权限、在 OpenClaw 中绑定，最后完成安全与后台运行设置，确保可在 Discord 频道 / 私聊中稳定调用 OpenClaw。

## 前置准备工作 <a href="#wpky-1770779374218" id="wpky-1770779374218"></a>

在你正式开始为OpenClaw（Clawdbot）配置Discord前，请依次检查如下事项是否准备完成：

* Discord 账号（[注册地址](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdiscord.com%2Fregister\&objectId=2625092\&objectType=1\&contentType=undefined)，并创建 / 加入目标服务器）。
* 是否已经在Lighthouse服务器实例（推荐海外地域）部署且配置好了OpenClaw，且为2026.2.3或更高版本。如果暂时还没有，建议：
* 如果您希望新购一台[Lighthouse](https://cloud.tencent.com/product/lighthouse?from_column=20421\&from=20421)服务器来安装运行OpenClaw，可以前往腾讯云Lighthouse产品的[购买页](https://buy.cloud.tencent.com/lighthouse)选购，或者前往腾讯云[OpenClaw专属活动](https://cloud.tencent.com/act/pro/lighthouse-moltbot)进行优惠下单。详细的部署和配置OpenClaw流程可参考[云上OpenClaw(原Clawdbot)一键秒级部署指南](https://cloud.tencent.com/developer/article/2624003)。
* 如果已有之前部署的OpenClaw，但不是最新版本的应用模板，可以参考教程进行版本更新：[如何更新服务器OpenClaw应用版本](https://cloud.tencent.com/developer/article/2627964)

## 接入Discord <a href="#id-8g7w-1770779374248" id="id-8g7w-1770779374248"></a>

#### 创建 Discord Bot 并获取 Token（开发者平台操作） <a href="#thb7-1770779374250" id="thb7-1770779374250"></a>

这是接入的核心凭证，步骤如下：1. 打开 Discord 开发者平台：[https://discord.com/developers/applications](https://discord.com/developers/applications)，点击New Application，输入 Bot 名称（如 Moltbot-AI），同意条款后创建

![0](../.gitbook/assets/0)

![0](<../.gitbook/assets/0 (1)>)

2\. 进入应用页面，点击左侧Bot，复制Token（点击Reset Token生成，妥善保存，泄露会导致 Bot 被滥用）；

![0](<../.gitbook/assets/0 (2)>)

3\. 开启关键权限（必做，否则 Moltbot 无法读取消息 / 发送回复）：下滑到Privileged Gateway Intents，开启MESSAGE CONTENT INTENT（读取消息内容）、SERVER MEMBERS INTENT（可选，用于服务器成员权限控制），开启后点击下方Save Changes；

![0](<../.gitbook/assets/0 (3)>)

4\. 配置 Bot 权限：左侧OAuth2→URL Generator，勾选以下权限（最小化原则）：Scopes：bot + applications.commands；

![0](<../.gitbook/assets/0 (4)>)

a. 下滑继续选择Bot Permissions：Send Messages、Read Message History、Embed Links、Use Slash Commands；

![0](<../.gitbook/assets/0 (5)>)

5\. 复制生成的Invite Link，在浏览器打开，将 Bot 邀请到你的 Discord 服务器（需服务器管理员权限）。点击继续后进行授权，即可邀请bot加入：

![0](<../.gitbook/assets/0 (6)>)

![0](<../.gitbook/assets/0 (7)>)

添加完成的效果如下图所示：

![0](<../.gitbook/assets/0 (8)>)

#### 为OpenClaw配置模型 <a href="#ekjq-1770779374287" id="ekjq-1770779374287"></a>

接下来需要为已经完成部署的OpenClaw配置模型。进入腾讯云[控制台](https://console.cloud.tencent.com/lighthouse)，选中对应的已部署OpenClaw的Lighthouse服务器，点击服务器卡片进入“管理实例”页面。

![0](<../.gitbook/assets/0 (9)>)

模型配置为OpenClaw配置模型API Key可以在Lighthouse服务器的应用管理页面进行操作。详情可参考[云上OpenClaw(原Clawdbot)一键秒级部署指南](https://cloud.tencent.com/developer/article/2624003)-配置模型APIKey，此处不再赘述。

#### OpenClaw基础配置 <a href="#bact-1770779374304" id="bact-1770779374304"></a>

首次登入服务器后，输入并回车运行如下命令开始配置：代码语言：Bash自动换行AI代码解释clawdbot onboard运行 clawdbot onboard 后，需要通过键盘来完成后续配置动作，关键操作：方向键控制选项，回车表示选择并确认。同意免责声明运行上面的命令后，将会出现一个问题：是否知晓风险，选择Yes就行。

![0](<../.gitbook/assets/0 (10)>)

配置模式选择：快速入门接下来需要选择Onboarding的模式，我们选择QuickStart。

![0](<../.gitbook/assets/0 (11)>)

配置处理方式选择 Use existing values

![0](<../.gitbook/assets/0 (12)>)

模型配置上述过程中已在腾讯云控制台配置大模型，跳过此步骤即可（按下图示例选择）。为OpenClaw配置模型APIKey可以在Lighthouse服务器的应用管理页面进行操作。详情可参考[云上OpenClaw(原Clawdbot)一键秒级部署指南](https://cloud.tencent.com/developer/article/2624003)-配置模型APIKey，此处不再赘述。Skip for now

![0](<../.gitbook/assets/0 (13)>)

All providers

![0](<../.gitbook/assets/0 (14)>)

Keep current

![0](<../.gitbook/assets/0 (15)>)

#### Channel配置-接入Discord <a href="#stta-1770779374370" id="stta-1770779374370"></a>

在 Select channel 的步骤中，用键盘方向键选中 Discord (Bot API) ，并且回车：

![0](<../.gitbook/assets/0 (16)>)

输入Discord bot token这里就是前文提到生成的 Bot token

![0](<../.gitbook/assets/0 (17)>)

配置访问权限选择 Yes 。

![0](<../.gitbook/assets/0 (18)>)

访问权限模式选择 Open(allow all channels)

![0](<../.gitbook/assets/0 (19)>)

配置 Skills选择：No原因：Skills 可以启用系统级自动化能力，包括：

* 文件访问
* 浏览器控制
* Shell命令执行

对于初次部署，限制权限可以提升稳定性和安全性。

![0](<../.gitbook/assets/0 (20)>)

启用 Hooks（若未出现此步骤，跳过即可）只选择: session-memory（按键盘的上下箭移动光标，空格键选中，回车键确认进入下一步）原因：

* 不会执行任何系统命令
* 安全风险最低

请勿选择：

* 启动时自动运行脚本（boot-md）
* 命令跟踪与日志记录（command-logger）

![0](<../.gitbook/assets/0 (21)>)

安装完成选择 Restart

![0](<../.gitbook/assets/0 (22)>)

启动方式选择 Do this later

![0](<../.gitbook/assets/0 (23)>)

安装命令补全功能选择 No注意：此处如果选择Yes，后续OpenClaw运行的时候容易导致服务器CPU负载高，导致OpenClaw运行出问题。

![0](<../.gitbook/assets/0 (24)>)

在Discord中与Bot聊天点击刚才创建的Bot

![0](<../.gitbook/assets/0 (25)>)

选择私聊，发送第一条消息

![0](<../.gitbook/assets/0 (26)>)

首次对话，会发送一个配对码，运行下方命令完成配对

![0](<../.gitbook/assets/0 (27)>)

代码语言：Bash自动换行AI代码解释openclaw pairing approve discord \<code>注意：将`替换为您在Discord中收到的Pairing code，输入时不加<>`![0](<../.gitbook/assets/0 (28)>)`现在，您可以在Discord中和已经接入的OpenClaw机器人进行聊天了`

![0](<../.gitbook/assets/0 (29)>)<br>
