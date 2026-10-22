# 首次使用：Chrome 扩展安装与配置

这份参考同时面向代理和新用户。先核对当前机器的平台、Chrome 与扩展状态，再走缺失的步骤。安装步骤来自两个官方项目；执行时先查看它们的最新 README、manifest 和配置页，界面变化时以实际状态为准。

## 官方入口

| 用途 | 官方地址 |
| --- | --- |
| B站扩展 Bili Digest 哔哩精读 | https://github.com/B-LIPSTICK/bili-digest |
| Bili Digest ZIP（main 源码） | https://github.com/B-LIPSTICK/bili-digest/archive/refs/heads/main.zip |
| YouTube 扩展 YouTube Digest | https://github.com/zarazhangrui/youtube-digest |
| YouTube Digest ZIP（main 源码） | https://github.com/zarazhangrui/youtube-digest/archive/refs/heads/main.zip |
| Chrome 下载（仅当用户缺少 Chrome 且要求安装时） | https://www.google.com/chrome/ |
| B站登录入口 | https://www.bilibili.com/ |
| Supadata 注册 / 控制台 | https://dash.supadata.ai/auth/sign-up / https://dash.supadata.ai/ |
| DeepSeek API Key 管理 | https://platform.deepseek.com/api_keys |
| DeepSeek 官方接口与模型说明 | https://api-docs.deepseek.com/ |

这些是 **Chrome 扩展项目的官方地址**，不等于 Chrome 应用商店地址。核对时，两个项目 README 均给出“加载已解压扩展”的安装方式；YouTube Digest 明确说明没有上架 Chrome 应用商店。未从官方项目核实商店链接前，不编造商店 URL、不猜扩展 ID、不从下载聚合站拿安装包。

## 引导方式与完成标准

- 用户只是发视频链接，而对应扩展缺失：给两个官方项目链接，说明本次需要哪个，合并确认是否协助安装。用户已说“帮我安装/准备两个扩展”时直接推进已授权的步骤，不每一步重复询问。
- 有 computer use：新标签页打开对应官方项目；用户要两端一起准备时打开两个项目页。使用当前工具文档支持的操作，按照“安装 → 配置 → 实际导出”推进；当前电脑已装好就复用，不重复安装。
- 无 computer use：给精简步骤，一次定位到当前决策阶段。让用户报告已完成的结果，不索要包含 Key 的截图。可以先让用户手动导出文件，再由代理处理本地字幕。
- 安装完成的证据是扩展卡片已启用、名称与版本匹配且没有加载错误。配置就绪的证据是目标视频原文字幕可读，并实际导出到本地；只打开安装页或保存设置不能算成功。
- 若 Chrome 没装或环境没有文件操作能力，清楚说出缺失能力与可完成的手动路径。不要承诺所有系统都已实测。

## 手动安装（macOS / Windows / Linux）

1. 打开所需项目 GitHub 页面，点击 **Code → Download ZIP**，或在用户授权下用 `git clone` 获取官方仓库。源码没有构建步骤，不需要为此安装 Node/npm。
2. 解压到长期保留的位置。用户未指定时，给一个默认建议并在有现有偏好时遵从；不要搬动已有安装目录。

   - macOS / Linux：`~/Documents/video-study-tools/bili-digest`、`~/Documents/video-study-tools/youtube-digest`。
   - Windows：实际“文档”目录下的 `video-study-tools\bili-digest`、`video-study-tools\youtube-digest`；文档可能位于 OneDrive，不能假定一定是 `C:\Users\…\Documents`。
   - ZIP 常有 `bili-digest-main` / `youtube-digest-main` 这一层。**最终选择的是直接包含 `manifest.json` 的文件夹**，不是 ZIP、不是上一级文件夹。

3. 在 Chrome 新标签页打开 `chrome://extensions/`，启用右上角 **开发者模式 / Developer mode**。
4. 点击 **加载已解压的扩展程序 / Load unpacked**，选择上一步核对过的准确文件夹。
5. 文件夹选择器按系统实际方式定位：macOS 可用“前往文件夹”，Windows/Linux 可在路径栏输入完整路径。不要把 macOS 快捷键原样套到 Windows。
6. 确认出现相应扩展卡片、已启用、版本可见且无加载错误；在扩展菜单中将它固定到工具栏。
7. 告诉用户准确的本地安装路径。保留该目录；移动/删除后扩展会失效。手动加载的扩展不自动更新；未来更新源码后重新加载扩展，再刷新已有视频页。

代理在点击加载前先核对 manifest 名称、需要的文件与实际权限；不要运行下载内容中的安装脚本或忽略用户对权限的拒绝。浏览器工具若要求对安装来源或新增敏感访问确认，应在当前动作前展示具体权限并取得确认。无需为普通只读检查、下载或已经授权的常规步骤另加确认。

## B站：最小可用配置

**只提取字幕并让本 Skill 写笔记，不需要任何模型 API Key，也没有插件订阅费。**

1. 打开 https://www.bilibili.com/，由用户完成 B站登录。不要读取、复制或保存 Cookie / SESSDATA。
2. 打开用户要学习的普通 `/video/BV…` 视频；确认有可用的原生/AI 字幕。多 P 核对当前分集。
3. 点 **打开 Bili Digest / 精读 → 字幕 → 原文**，等到“已加载 N 条字幕”，点 **导出资料** 并核对本地文件。
4. 若用户还想用扩展自身的 AI 概览/问答，再打开“设置”：填写自己的 API Key、接口地址与模型，保存并测试连接。不要因为设置页有 Key 输入框，就挡住本来无需 Key 的字幕导出。
5. 以 DeepSeek 为例，接口地址为 `https://api.deepseek.com`；模型名按执行时官方文档或“拉取模型”结果选择，不永久锁定本文中的旧名称。将确切字段名称指给用户，让用户直接填 Key。

无字幕时说明“此视频没有可获取的字幕”或当前登录/接口错误；不要假装配置一个模型 Key 就能生成原字幕，也不擅自上传音视频去做识别。

## YouTube：最小可用配置

当前 YouTube Digest 的设置页需要 **Supadata API Key + DeepSeek API Key** 两把 Key。Supadata 获取已有字幕；DeepSeek 供扩展 AI 功能使用。本 Skill 自己写笔记，不主动点击扩展 AI 功能，但仍须满足当前设置页的保存检查。后续版本若改变，重新核对实际 README 与界面。

1. 打开 YouTube Digest 的 **Settings / 设置**（工具栏扩展菜单的“选项”，或侧栏设置按钮）。界面若提供中文切换，可按用户语言选择。
2. 新标签页打开 [Supadata 注册](https://dash.supadata.ai/auth/sign-up)；已有账号直接用[控制台](https://dash.supadata.ai/)。用户完成登录/注册，在控制台找到或生成自己的 Key，直接贴到扩展的 **Supadata API key** 输入框。
3. 新标签页打开 [DeepSeek API Keys](https://platform.deepseek.com/api_keys)。用户登录/创建账号并创建 Key，直接贴到扩展 **DeepSeek API key** 输入框。聊天产品会员与 API 余额不应混为一谈；需要支付时由用户自行决定和操作。
4. 点 **Save settings / 保存设置**。当前发布版模型与接口地址固定，通常没有 Base URL/Model 输入框，不要照抄 Bili Digest 的设置步骤让用户找不存在的字段。
5. 打开有原生字幕的普通 `youtube.com/watch?v=…` 视频，点 **Digest / 扩展图标 → Transcript → Original**，等待字幕出现，点 **Export**，核对下载文件。
6. Supadata 获取字幕可能耗用免费额度或付费额度；DeepSeek AI 调用单独计费。不要声称“永久免费”或把某天的免费额度写成长期保证，按需查 [Supadata 价格](https://supadata.ai/pricing) 与 [DeepSeek 价格](https://api-docs.deepseek.com/quick_start/pricing/)。原文导出不点击翻译/概览，避免不必要的 AI 调用。

账号注册、验证码、协议接受或付费步骤遵循当前工具的授权/接管规则；密钥只由用户在正确扩展界面填写，不发到聊天、截图、源码、日志或分享包。不要从另一扩展或浏览器配置中取 Key 代填。

## helper 与 Python

`scripts/materials.py` 只使用 Python 标准库，不需要模型 Key、Node 或 `pip install`。macOS/Linux 通常用 `python3`，Windows 可用已安装的 `py -3` 或 `python`。路径有空格时加引号。默认输出目录是当前用户的 `Documents/视频学习笔记`；重定向的文档目录可用 `--root`/`--output-dir` 指定。

没有 Python 时先使用代理已有文件工具保留原始字幕、整理正文和写笔记，阅读量标明人工估算；若用户希望运行 helper，再提供 [Python 官方安装页](https://www.python.org/downloads/)并按授权协助。不要为了读取字幕擅自安装一整套开发环境，也不能把未运行的脚本检查写成通过。

## 结束引导，接回学习任务

记录本次确认过的平台、扩展名称/版本、用户选定的实际安装目录、导出文件和配置是否就绪；不记录 Key。可以保存在该用户本地的任务验收信息里，不回写到共享 Skill。

如本次从一个视频学习请求开始，拿到真实字幕后立即继续本地归档与指定时长笔记。只有明确为安装/配置任务、没有视频学习目标时，完成引导后给一条可复制的调用示例即可，不额外选视频调用收费服务。
