# andsee Cutroom — agent 插件

**看到一条好视频，剪出你自己的那一条。** Cutroom 是装在你电脑上的视频剪辑引擎，由 agent（Claude Code、Codex、Antigravity…）或它自带的浏览器编辑器来驱动。给它一条对标视频和你的口播，它拆出对方的剪法，套到你自己的素材上：字幕、版式、B-roll、动效、音乐、音效都锚在你说的每个词上，渲染出片，再和对标逐帧对照打分。

[官网和账号](https://andsee.ai/cutroom) · [English](./README.md) · [登录和生成](./docs/account.md) · [在 agent 里用](./docs/agents.md)

这个仓库是开源的部分：agent 读的入门技能和插件清单。引擎另外安装（免费，需要登录）。

## 安装

把这句话贴给你的 agent（Claude Code、Codex、Antigravity…；macOS 和 Windows 都一样）。它会装好 Cutroom（已经装了就更新到最新版）、带你登录、接上完整技能：

```text
读 https://github.com/andsee-ai/cutroom-agent-plugin/blob/main/skills/cutroom-start/SKILL.md ，按里面的步骤在这台电脑上装好 Cutroom（已经装了就更新到最新版）、登录 andsee，然后接上完整的 cutroom 技能。
```

或者自己装：

```sh
# macOS（Apple 芯片），在终端里
curl -fsSL https://andsee.ai/install/cutroom.sh | sh
```

```powershell
# Windows 10 / 11（64 位），在 PowerShell 里
irm https://andsee.ai/install/cutroom.ps1 | iex
```

然后（Windows 上新开一个终端窗口）：

```sh
cutroom login            # 在浏览器里登录 andsee（免费），允许这台电脑
cutroom env              # 检查这台电脑：FFmpeg、Chrome / Edge…，缺什么告诉你怎么装
cutroom skill install    # 把技能接进 Claude Code / Codex / Antigravity
```

装好之后不用再管：打开编辑器（`cutroom editor`）时，有新版本会在空闲时自动装好；也可以随时 `cutroom update`。Intel Mac 和 Linux 的安装包在准备中。

## 可以让它做什么

| | |
|---|---|
| **复刻** | 「把这条口播按这条对标视频复刻一遍」：对标的结构、节奏、版式和包装套到你的素材上，逐帧对照 |
| **智能剪辑** | 「把这条口播剪成一条 TikTok」：按意思分段、排镜头、配开场钩子，画面单调处补 B-roll 和信息卡，打分并开方 |
| **包装** | 逐词字幕、动效单元、音乐闪避、音效，都锚在台词上：改一句话，后面的时间自己重排 |
| **裂变** | 一条跑通的剪辑，出很多个版本 |

也可以打开编辑器，指着哪里改哪里：`cutroom editor`。

## 什么要花钱

剪辑、字幕、动效、渲染都在本机，不花钱。生成图片、视频、配音需要一个生成服务，用哪个你自己选：

- **andsee**：花 andsee 账号里的积分，不用配置：`cutroom account use andsee`
- **自己的服务**：你自己的中转站（OpenAI 兼容）、网关、命令行或技能，密钥只存在你的电脑上：`cutroom account use custom`

每一步要花钱的操作都会先给你看价格，你同意了才执行。

## 素材和权利

你的素材和工程都留在你的电脑上。Cutroom 复刻的是对标视频「怎么剪」，用的是你自己的素材；别人视频里的画面、人像、音乐、商标能不能用，由你自己判断。

## 许可

本仓库的内容以 [Apache-2.0](./LICENSE) 发布。Cutroom 引擎以安装包发布，另有[使用条款](https://andsee.ai/install/cutroom-terms.html)。Cutroom 是独立实现；它包含的第三方组件列在安装包的 `THIRD-PARTY-NOTICES.md` 里。
