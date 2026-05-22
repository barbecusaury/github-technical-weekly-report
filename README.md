# GitHub技术周报

`github-technical-weekly-report` 是一个 Codex skill，用于生成、维护和发布单文件版 GitHub 技术周报 HTML。它面向 GitHub 一周热榜、一个月热榜和飙升榜这类排行榜页面，要求产物可以直接打开，内联 CSS/JS，不依赖本地构建流程。

## 适用场景

- 每周生成 GitHub 技术排行榜单页。
- 修复或增强已有 HTML 周报页面。
- 给周报增加简体中文、繁体中文和英语切换。
- 维护榜单项目摘要、弹窗项目介绍、作用说明和使用建议的本地化。
- 上传报告或 skill 到 GitHub，并在远端页面验证文件存在。

## 关键能力

- 保持技术编辑类排行榜视觉风格，避免营销页式卡片堆砌。
- 支持三类榜单：一周内热榜、一个月内热榜、飙升榜。
- 支持榜单前 10 直接展示、第 11 到 20 名折叠展开。
- 弹窗支持关闭按钮、点击遮罩关闭、Esc 关闭和键盘可访问性。
- 中文 locale 下，列表摘要和弹窗“项目介绍”都会走本地化内容，不回退显示英文。
- 验证 HTML 文件存在、内联脚本可解析、语言按钮存在、交互钩子存在。

## 仓库结构

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── github-upload-via-chrome.md
    ├── intro.en.md
    ├── intro.zh-CN.md
    └── intro.zh-Hant.md
```

## 使用方式

在 Codex 中调用 `$github-technical-weekly-report`，并提供目标 HTML 文件，或说明要新生成一份 GitHub 周报。修改后应运行项目内验证脚本；如果要发布到 GitHub，应确认目标仓库、分支和文件路径，再提交或网页上传。

## 本地验证建议

```powershell
node scripts\verify-report.mjs
```

如果只使用本 skill 仓库，可重点检查 `SKILL.md`、`agents/openai.yaml` 和 `references/` 是否完整；真正的 HTML 报告验证脚本通常位于调用该 skill 的周报项目中。
