# OpenClaw（原 Clawdbot）钉钉对接保姆级教程 手把手教你打造自己的 AI 助手

原文：[https://catchadmin.com/post/2026-01/openclaw-dingding-install](https://catchadmin.com/post/2026-01/openclaw-dingding-install)

OpenClaw 是一款开源的本地 AI 助手，支持在你自己的服务器上部署，通过钉钉、飞书、WhatsApp、Telegram 等聊天工具交互。与云端 SaaS 服务不同，OpenClaw 让你完全掌控数据隐私，可以执行系统命令、浏览网页、管理文件，甚至编写代码。本教程将手把手教你在 Linux 系统下安装 OpenClaw 并对接钉钉机器人，打造专属的智能助理。

> 注意：本教程在 Linux 系统下进行

如果你需要飞书教程，可以看[保姆级 OpenClaw （原 Clawdbot）飞书对接教程 手把手教你搭建 AI 助手](https://www.cnblogs.com/catchadmin/p/19556552)

### OpenClaw 是什么？ <a href="#openclaw-shi-shen-me" id="openclaw-shi-shen-me"></a>

OpenClaw(原名 Clawdbot,后更名为 Moltbot,现正式命名为 OpenClaw)是一个运行在你本地环境的高权限 AI 智能体。它的核心特性包括：

* **本地部署**：运行在你的服务器或电脑上,数据完全自主可控
* **多平台支持**：支持钉钉、飞书、WhatsApp、Telegram、Discord、Slack 等主流聊天工具
* **浏览器控制**：可以浏览网页、填写表单、提取数据
* **系统访问**：读写文件、执行 Shell 命令、运行脚本
* **持久化记忆**：记住你的偏好和上下文,成为真正属于你的 AI
* **插件扩展**：支持社区技能插件,甚至可以自己编写插件

无论是邮件管理、日程安排、数据查询还是代码编写,OpenClaw 都能成为你的得力助手。

### 准备工作 <a href="#zhun-bei-gong-zuo" id="zhun-bei-gong-zuo"></a>

首先准备一台闲置的云服务器或 VPS（推荐使用香港或海外节点）。由于 OpenClaw 运行时权限较大，出于安全考虑，不建议在本地或工作机上安装，推荐在一台独立的空服务器上部署。准备完成后，登录到服务器。

### 安装 <a href="#an-zhuang" id="an-zhuang"></a>

> 如果你不想安装，可以直接使用阿里云的[Openclaw 一键部署 (原 Clawdbot)](https://www.aliyun.com/activity/ecs/clawdbot?userCode=oq2t54oi)，部署之后可以直接跳到[对接钉钉](https://www.cnblogs.com/catchadmin/p/19560247#%E5%AF%B9%E6%8E%A5%E9%92%89%E9%92%89)。

第一步安装 Git

```shell
# 安装 Git
sudo apt update
sudo apt install git -y
```

第二步安装 Node.js

```shell
# 安装 NVM
# 国内使用 gitee 的镜像源
curl -o- https://gitee.com/RubyMetric/nvm-cn/raw/main/install.sh | bash

# 国外使用
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# 重新加载环境变量
source ~/.bashrc

# 安装 Node.js 22
nvm install 22

# 查看 nodejs 版本
node -v # 输出 v22 即可，版本只要 22 就行
```

### 安装 Openclaw <a href="#an-zhuang-openclaw" id="an-zhuang-openclaw"></a>

```shell
# 使用官方脚本安装
curl -fsSL https://openclaw.bot/install.sh | bash
```

> 服务器在国内，如果安装失败的话，可能需要解决网络问题

其他平台安装方式请参考[Openclaw 安装文档 (原 Clawdbot)](https://docs.openclaw.bot/install/installer)

你会看到如下图输出\
\
如果首次安装，时间会很长，需要耐心等待。\
如果最后输出如下内容：

<figure><img src="https://image.catchadmin.com/202601310803318.png" alt=""><figcaption></figcaption></figure>

```shell
→ npm install failed; cleaning up and retrying...
```

新的脚本服务器内存要求变高了，据我使用下来 2G 内存，肯定会 OOM，如果出错的话，建议使用 `swap` 把硬盘空间当作交互内存使用。

成功之后会输出如下图片\
\
第一个选项选择 `yes`, 就是询问你是否知道风险的。\
第二步选择 `QuickStart`\
\
第三步选择模型服务商，这里选择 `Qwen`，免费额度充足，适合入门使用\
\
选择千问模型后，会提供一个链接，复制并在浏览器中打开，如下图\
\
打开浏览器后，会看到如下界面。由于我已登录过，所以显示账户信息；如果尚未登录，按照提示完成登录即可。\
\
登录完成后，会出现以下选项，提示选择对应的千问模型，如下图<br>

<figure><img src="https://image.catchadmin.com/202601310805358.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281351166.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281352080.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281355542.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281356909.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281358170.png" alt=""><figcaption></figcaption></figure>

选择默认模型即可。接下来会提示选择 channel，这里先跳过，后续再添加

\
继续下面选择 skills，也是选择 `No`，如下图\
\
继续下面选择 hooks，也是使用`空格`选择 `No`，如下图\
\
然后等待安装完成，最后会出现以下选项，这里选择 `TUI`\
\
如果看到 TUI 聊天界面，说明安装成功，可以尝试输入 `Hello` 进行测试。\
\
然后直接使用 `ctrl+c` 先关闭，后面我们再来设置

<figure><img src="https://image.catchadmin.com/202601281359123.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281359786.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281400483.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281403169.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202601281404354.png" alt=""><figcaption></figcaption></figure>

#### 查看服务 <a href="#cha-kan-fu-wu" id="cha-kan-fu-wu"></a>

可以使用下面的命令来查看

```shell
openclaw status
```

会看到如下图的结果就说明服务启动了<br>

<figure><img src="https://image.catchadmin.com/202601281449942.png" alt=""><figcaption></figcaption></figure>

#### 访问 Web UI 面板 <a href="#fang-wen-webui-mian-ban" id="fang-wen-webui-mian-ban"></a>

如何访问面板？服务监听在 `http://127.0.0.1:18789/` 端口上，我们现在通过 ssh 隧道来访问，输入下面的命令

```shell
ssh -N -L 18789:127.0.0.1:18789 用户名@服务器IP
# 回车之后
用户名@服务器IP's password: # 输入密码
```

然后在浏览器打开 `http://127.0.0.1:18789/`, 你会看到 Dashboard 了，如下图\
\
图中显示的是未授权状态，回到服务器，输入以下命令

<figure><img src="https://image.catchadmin.com/202601281509102.png" alt=""><figcaption></figcaption></figure>

```shell
openclaw dashboard
```

会看到下面的面板数据\
![OpenClaw 钉钉教程 - Dashboard URL 获取命令](https://image.catchadmin.com/202601281530336.png)\
复制对应的 `Dashboard URL` 到浏览器打开，即可正常查看聊天记录。<br>

<figure><img src="https://image.catchadmin.com/202601281532427.png" alt=""><figcaption></figcaption></figure>

至此 Openclaw (原 Clawdbot) 已安装完成，可以正常访问了。然后聊天框里面首次输入 `Hello`, `Clawdbot` 会询问你他应该叫什么，应该叫你什么。就是你需要给它设置个名字，还有 bot 改叫你什么。你可以在聊天框这么输入

```shell
Name: Openclaw

My Name: Boss
```

### 对接钉钉 <a href="#dui-jie-ding-ding" id="dui-jie-ding-ding"></a>

钉钉是国内使用最广泛的企业办公平台之一，OpenClaw 支持通过钉钉机器人进行交互。本节将介绍如何配置钉钉机器人对接 OpenClaw。

#### 安装钉钉插件 <a href="#an-zhuang-ding-ding-cha-jian" id="an-zhuang-ding-ding-cha-jian"></a>

首先安装飞书插件，输入以下命令直接运行 openclaw 插件安装命令，openclaw 会自动处理下载、安装依赖和注册。时间有可能比较久，等待即可

```shell
openclaw plugins install https://github.com/soimy/clawdbot-channel-dingtalk.git
```

#### 创建钉钉应用 <a href="#chuang-jian-ding-ding-ying-yong" id="chuang-jian-ding-ding-ying-yong"></a>

登录[钉钉开放平台](https://open-dev.dingtalk.com/)，点击「创建应用」

> 注意：创建钉钉应用需要你的钉钉账号有开发者权限。如果没有，可以联系组织管理员获取，或参考[获取开发者权限](https://open.dingtalk.com/document/orgapp/obtain-developer-permissions)

在应用开发的左侧导航栏中，点击「钉钉应用」，然后点击右上角「创建应用」。\
\
填写应用名称和应用描述，上传应用图标后保存。<br>

<figure><img src="https://image.catchadmin.com/202602010822631.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202602010823281.png" alt=""><figcaption></figcaption></figure>

#### 添加机器人 <a href="#tian-jia-ji-qi-ren" id="tian-jia-ji-qi-ren"></a>

在应用开发的左侧导航栏中，点击「添加应用能力」，然后点击添加「机器人」。\
\
添加完机器人之后，就是配置一些基本信息之后，点击发布。<br>

<figure><img src="https://image.catchadmin.com/202602010826716.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://image.catchadmin.com/202602010828348.png" alt=""><figcaption></figcaption></figure>

> 最后得消息接受模式一定要是 `stream 模式`

#### 发布版本 <a href="#fa-bu-ban-ben" id="fa-bu-ban-ben"></a>

在发布完机器人之后，一定要发布版本。在应用开发的左侧导航栏中，点击「版本管理与发布」，然后点击右上角「创建新版本」。<br>

<figure><img src="https://image.catchadmin.com/202602010831566.png" alt=""><figcaption></figcaption></figure>

#### 获取凭证信息 <a href="#huo-qu-ping-zheng-xin-xi" id="huo-qu-ping-zheng-xin-xi"></a>

发布版本成功之后，点击左侧菜单的「凭证与基础信息」，获取以下凭证信息

* Client ID (AppKey)
* Client Secret (AppSecret)
* Robot Code (与 Client ID 相同)
*   Agent ID (应用 ID)<br>

    <figure><img src="https://image.catchadmin.com/202602010825158.png" alt=""><figcaption></figcaption></figure>
*   Corp ID (企业 ID)<br>

    <figure><img src="https://image.catchadmin.com/202602010835442.png" alt=""><figcaption></figcaption></figure>

#### 添加钉钉配置 <a href="#tian-jia-ding-ding-pei-zhi" id="tian-jia-ding-ding-pei-zhi"></a>

找到 `openclaw.json` 配置文件。使用下面的命令找到配置文件

```shell
find / | grep openclaw.json

# 本人服务器的输出如下，每个人都不一样，按实际情况找
#/root/.openclaw/openclaw.json.bak
#/root/.openclaw/openclaw.json.bak.1
#/root/.openclaw/openclaw.json // 这个就是配置文件
#/root/.openclaw/openclaw.json.bak.2
```

然后找到对应的 `channels` 配置

```json
{
  "channels": {
    "dingtalk": {
      "enabled": true,
      "clientId": "dingxxxxxx",
      "clientSecret": "your-app-secret",
      "robotCode": "dingxxxxxx",
      "corpId": "dingxxxxxx",
      "agentId": "123456789",
      "dmPolicy": "open",
      "groupPolicy": "open",      
      "messageType": "markdown",       
      "debug": false
    }
  }
}
```

如果你找不到对应的配置，也不用担心，使用下面的命令配置也是可以的

```shell
openclaw config set channels.dingtalk.enabled true

openclaw config set channels.dingtalk.clientId 你的 Client ID

openclaw config set channels.dingtalk.clientSecret 你的 Client Secret

openclaw config set channels.dingtalk.robotCode Robot Code (与 Client ID 相同)

openclaw config set channels.dingtalk.corpId 你的corpId

openclaw config set channels.dingtalk.agentId Agent ID

openclaw config set channels.dingtalk.dmPolicy open

openclaw config set channels.dingtalk.groupPolicy open

openclaw config set channels.dingtalk.messageType markdown

openclaw config set channels.dingtalk.debug false

```

配置完成之后，重启服务

```shell
openclaw gateway restart
```

#### 测试机器人 <a href="#ce-shi-ji-qi-ren" id="ce-shi-ji-qi-ren"></a>

回到钉钉客户端软件，在顶部搜索栏目搜索机器人名称 `openclaw`\
\
点击机器人就可以直接跟机器人聊天了。可以输入 `Hello`

<figure><img src="https://image.catchadmin.com/202602010938934.png" alt=""><figcaption></figcaption></figure>

### 常见问题 FAQ <a href="#chang-jian-wen-ti-faq" id="chang-jian-wen-ti-faq"></a>

#### OpenClaw 和 Clawdbot、Moltbot 是什么关系？ <a href="#openclaw-he-clawdbotmoltbot-shi-shen-me-guan-xi" id="openclaw-he-clawdbotmoltbot-shi-shen-me-guan-xi"></a>

OpenClaw 是该项目的最新正式名称。项目最初叫 Clawdbot，后因商标问题更名为 Moltbot，最终在 2025 年 1 月正式定名为 OpenClaw。三者是同一个项目的不同阶段命名。

#### OpenClaw 支持哪些 AI 模型？ <a href="#openclaw-zhi-chi-na-xie-ai-mo-xing" id="openclaw-zhi-chi-na-xie-ai-mo-xing"></a>

OpenClaw 支持多种 AI 模型服务商，包括 Anthropic Claude、OpenAI GPT、通义千问（Qwen）、KIMI、小米 MiMo 等。本教程使用通义千问是因为其免费额度充足，适合入门学习。

#### 为什么安装时提示 npm install failed？ <a href="#wei-shen-me-an-zhuang-shi-ti-shi-npminstallfailed" id="wei-shen-me-an-zhuang-shi-ti-shi-npminstallfailed"></a>

这通常是服务器内存不足导致的。新版本脚本对内存要求较高，2G 内存可能会出现 OOM（内存溢出）。建议配置 swap 交换空间，将硬盘空间作为虚拟内存使用。

#### OpenClaw 可以在 Windows 或 macOS 上运行吗？ <a href="#openclaw-ke-yi-zai-windows-huo-macos-shang-yun-xing-ma" id="openclaw-ke-yi-zai-windows-huo-macos-shang-yun-xing-ma"></a>

可以。OpenClaw 支持 Mac、Windows 和 Linux 系统。本教程以 Linux 为例，其他系统的安装方式可参考[官方文档](https://docs.openclaw.ai/)。

#### 钉钉机器人配置后无法收到消息怎么办？ <a href="#ding-ding-ji-qi-ren-pei-zhi-hou-wu-fa-shou-dao-xiao-xi-zen-me-ban" id="ding-ding-ji-qi-ren-pei-zhi-hou-wu-fa-shou-dao-xiao-xi-zen-me-ban"></a>

请检查以下几点：

1. 确认钉钉插件已正确安装（`clawdbot plugins install @openclaw-china/channels`）
2. 检查 Client ID 和 Client Secret 配置是否正确
3. 确认已申请 `Card.Streaming.Write` 和 `Card.Instance.Write` 权限
4. 检查机器人消息接收地址是否正确配置
5. 确保服务器 18789 端口对外开放
6. 确保应用版本已发布

#### OpenClaw 数据安全吗？ <a href="#openclaw-shu-ju-an-quan-ma" id="openclaw-shu-ju-an-quan-ma"></a>

OpenClaw 运行在你自己的服务器上，所有数据都在本地存储，不会上传到第三方云端。但由于它具有系统级权限，建议在独立的服务器上部署，避免在生产环境或重要数据的机器上运行。

#### 除了钉钉，OpenClaw 还支持哪些平台？ <a href="#chu-le-ding-ding-openclaw-hai-zhi-chi-na-xie-ping-tai" id="chu-le-ding-ding-openclaw-hai-zhi-chi-na-xie-ping-tai"></a>

OpenClaw 支持多个聊天平台，包括飞书、企业微信、QQ、WhatsApp、Telegram、Discord、Slack、Microsoft Teams、Signal、iMessage、Google Chat、Twitch 等。每个平台需要安装对应的插件。国内平台推荐使用 `@openclaw-china/channels` 插件。

#### OpenClaw 可以做什么？ <a href="#openclaw-ke-yi-zuo-shen-me" id="openclaw-ke-yi-zuo-shen-me"></a>

OpenClaw 可以执行多种任务：

* 邮件管理和自动回复
* 日程安排和提醒
* 浏览网页和数据提取
* 文件读写和管理
* 执行 Shell 命令
* 编写和运行代码
* 数据查询和分析

#### 如何更新 OpenClaw 到最新版本？ <a href="#ru-he-geng-xin-openclaw-dao-zui-xin-ban-ben" id="ru-he-geng-xin-openclaw-dao-zui-xin-ban-ben"></a>

使用以下命令更新：

```shell
openclaw update
```

#### OpenClaw 命令和 clawdbot 命令有什么区别？ <a href="#openclaw-ming-ling-he-clawdbot-ming-ling-you-shen-me-qu-bie" id="openclaw-ming-ling-he-clawdbot-ming-ling-you-shen-me-qu-bie"></a>

OpenClaw 更名后，官方推荐使用 `openclaw` 命令，但为了兼容性，`clawdbot` 命令仍然可用。两者功能完全相同，建议新用户直接使用 `openclaw` 命令。
