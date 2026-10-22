# 视频学习笔记 · video-study-notes

把 B站或 YouTube 视频链接变成一份可在指定时间内阅读和理解的中文学习笔记。默认 5 分钟，也可以说“给我 2 分钟版”或“展开成 10 分钟版”。

这是一份 Agent Skill，需要支持 `SKILL.md` 的 AI 代理。它会使用 Chrome 扩展导出字幕，把原始文件保存到你的电脑，再阅读全文生成笔记。第一次使用时，也可以引导你安装扩展、打开官方页面、配置账号和 API Key。

## 安装 Skill

把整个 `video-study-notes` 文件夹放到代理支持的个人 Skills 目录，保留 `SKILL.md`、`agents/`、`references/`、`scripts/` 的相对位置。

Codex 的常用位置：

- macOS / Linux：`~/.codex/skills/video-study-notes/`
- Windows：`%USERPROFILE%\.codex\skills\video-study-notes\`
- 设置了 `CODEX_HOME` 时：`<CODEX_HOME>/skills/video-study-notes/`

其他代理请按其自己的 Skill 安装说明选择目录。让代理读取该目录的 `SKILL.md` 也可以开始；不需要安装本项目之外的“万能安装器”。

## 怎么用

在支持自动发现 Skill 的代理中，发送视频链接即可；也可以明确调用：

```text
$video-study-notes <B站或YouTube视频链接>
$video-study-notes <视频链接> 给我10分钟版
把刚才那份笔记压缩成2分钟版
我还没装扩展，先帮我准备B站；之后再配YouTube
帮我打开两个扩展的官方页面，并一步步安装配置
```

分钟数是阅读、理解和简短回忆的估计预算，不是只截取视频前几分钟，也不保证限时完全掌握。更长的版本增加解释和案例；更短的版本保留最关键的概念和方法。改时长会复用已有字幕。

## 首次准备

| 平台 | Chrome 扩展官方项目 | 只导出原文字幕的条件 |
| --- | --- | --- |
| B站 | [Bili Digest 哔哩精读](https://github.com/B-LIPSTICK/bili-digest) | 登录 B站，视频有可获取字幕；无需模型 Key |
| YouTube | [YouTube Digest](https://github.com/zarazhangrui/youtube-digest) | 当前设置页需 Supadata + DeepSeek 两把 Key；视频有原生字幕 |

这两个链接是扩展项目地址，不是 Chrome 商店链接。当前官方安装步骤采用开发者模式“加载已解压的扩展程序”。完整步骤、下载地址、账号入口和各系统注意事项见 [安装与配置](references/setup.md)。

有 computer use 时，代理可以在授权范围内实际打开页面、下载到长期目录、加载扩展并验证。没有 computer use 时，按说明手动导出字幕，再让代理继续处理本地文件。支持面板/扩展内部页面的原生电脑操作能力会更适合这个流程；普通网页浏览工具不一定够用。

Supadata 和模型服务可能收取 API 费用，本 Skill 没有订阅服务，也不赠送额度。学习笔记由当前代理写作，默认不调用扩展的翻译或 AI 摘要。Key 由你直接填进扩展设置，不需要发给代理。

## 本地产物

默认保存在当前用户的 `Documents/视频学习笔记/` 下，每次一个独立文件夹，也可以指定自己的位置：

```text
<日期时间>-<视频ID>-<分P>/
  原始字幕.md 或 原始字幕.txt
  字幕正文.md
  来源与验收.json
  学习笔记-5分钟.md
  学习笔记-2分钟.md       # 之后改时长时新增
```

原始导出保留原字节。B站已有时间戳可以回链视频；YouTube 导出的 TXT 没有时间戳时，只引用本地正文，不编造跳转时间。脚本检查文件来源、分 P、数量等机械条件，观点是否忠于原字幕还需要代理读回核对。

## 可选辅助脚本

只需要 Python 3 标准库，无需 pip、Node 或 API Key。下面命令中的 `<…>` 替换成实际值：

```bash
python3 scripts/materials.py plan '<视频链接>' --minutes 5
python3 scripts/materials.py ingest '<扩展导出文件>' --url '<视频链接>' --output-dir '<本次目录>' --minutes 5
python3 scripts/materials.py check-note '<笔记文件>' --minutes 5
python3 -m unittest discover -s tests -v
```

Windows 可以将 `python3` 换成 `py -3`，并按 PowerShell 使用引号。`plan` 不联网；`ingest` 不操作浏览器、不生成摘要；`check-note` 只是阅读量估算。没有 Python 时可先手动归档并标注人工估算，不必为了开始学习安装整套开发环境。

## 已验证范围

已在 macOS Chrome 实际验证 Bili Digest 的 Markdown 字幕导出、YouTube Digest 的 TXT 原文导出，以及本地归档和 5/2 分钟笔记生成。Windows/Linux 提供安装指引与不依赖操作系统的 Python helper，但没有完成对应系统的真实 Chrome 安装验收。扩展升级或平台界面变化后可能需要调整操作。

本仓库不包含真实字幕、私人笔记、密钥、Cookie、浏览器个人资料或上述扩展的源码。两个上游项目独立维护，其许可证和条款分别适用。本 Skill 代码与文档采用 [MIT License](LICENSE)。
