# 🤖 QuickAI Plus for PowerToys Run — Enhanced Edition

> **EN**: A feature-packed enhanced fork of [ruslanlap/PowerToysRun-QuickAi](https://github.com/ruslanlap/PowerToysRun-QuickAi) v1.2.1 (MIT License, original copyright preserved).
> **中文**: 基于 [ruslanlap/PowerToysRun-QuickAi](https://github.com/ruslanlap/PowerToysRun-QuickAi) v1.2.1 的增强改造版（MIT 协议，保留原版权）。

**AI-powered assistance right inside PowerToys Run — now with LaTeX rendering, rich Markdown, a compact sticky-note window, and multi-turn follow-up chat.**
**在 PowerToys Run 里直接使用 AI——支持 LaTeX 公式渲染、富 Markdown、紧凑便签窗口、多轮追问对话。**

---

## ✨ 新增功能（相对原版 v1.2.1） / What's New vs Original v1.2.1

### 🧮 LaTeX 数学公式渲染 / LaTeX Math Rendering
- 支持 `$$...$$`、`\(...\)`、`\[...\]`、`$...$` 四种公式语法
- 基于 [WpfMath 2.1.0](https://www.nuget.org/packages/WpfMath) 渲染为真正的数学公式（分数、根号、积分、矩阵等）
- 智能公式清洗：自动剥离 `\begin{align}`/`\begin{array}` 等环境外壳、转换 `\text{中文}` → `\mathrm{}`、处理多字母算子（`\arccot`、`\arcsec`、`\argmax`、`\coth`、`\sech` 等）、去除 `\displaystyle`/`\color`/`\tag`/`\hline` 等不兼容命令
- **红点兜底**：渲染失败（`FormulaControl.HasError`）自动回退显示原始 LaTeX 文本，绝不显示错误占位符

### 📝 块级 Markdown 渲染 / Block-level Markdown
- `#` ~ `######` 标题（字号分级加粗）
- `>` 引用块（左侧色条 + 灰底）
- `-` / `*` / `+` 无序列表、`1.` 有序列表
- `---` / `***` 分隔线
- `| 列1 | 列2 |` Markdown 表格（表头加粗、细边框、自适应宽度不撑满）
- 空行自动分段；行内加粗/斜体/代码保留

### 🏷️ 紧凑便签窗口 / Compact Sticky-note Window
- 结果窗口 850×650 → **560×430 紧凑卡片**
- 无系统边框、圆角卡片 + 阴影、**置顶显示**（Topmost）
- 默认贴屏幕右下角（像便签），可拖顶栏移动
- 精简顶栏：Wrap / Copy / 关闭按钮

### 💬 继续追问 / Follow-up Chat
- 便签窗口底部内置**追问输入框 + 发送按钮**（Windows 系统默认控件外观，白底黑字统一风格）
- **多轮对话**：追问携带完整对话历史，AI 上下文连贯
- 聊天式显示：追问以 ❓ 标记插入，新回答流式追加，可滚动
- AI 思考时显示 `· Thinking...`，输入框自动锁定防重复发送

### ⚡ 性能优化 / Performance
- 流式渲染节流（~220ms 合并一次），解决逐 token 全量重渲染导致的卡顿
- 滚动流畅，流结束后自动完整渲染最终版

### 🔧 其他增强 / Other Improvements
- 全局无衬线字体（Segoe UI），公式与正文协调
- `max_tokens` 默认提升到 2048（可在设置中调整）
- **WpfMath 依赖加载修复**：PowerToys 插件加载器不按 deps.json 探测依赖，通过 `AssemblyLoadContext.Resolving` 回调从插件目录显式加载

---

## 📥 安装 / Installation

### 方法一：Release 直接下载（推荐） / Download Release
从 [Releases](https://github.com/Greyaircraft/QuickAi-Plus/releases) 下载最新的 `QuickAi.zip`，解压后：

1. **复制整个 `QuickAi` 文件夹**到 PowerToys Run 插件目录：
   ```
   %LOCALAPPDATA%\Microsoft\PowerToys\RunPlugins\QuickAi\
   ```
   > ⚠️ 注意：新版 PowerToys 的第三方插件目录是 `RunPlugins\`，不是 `PowerToys Run\Plugins\`（那是内置插件目录）

2. **确保 WpfMath.dll 和 XamlMath.Shared.dll 与主 DLL 同目录**（Release 包已包含）

3. **重启 PowerToys**（托盘图标右键 → Exit → 重新启动）

4. **配置 API Key**：PowerToys Settings → PowerToys Run → Plugins → QuickAI

### 方法二：源码构建 / Build from Source
```powershell
# 需要 .NET SDK 9.0+
git clone https://github.com/Greyaircraft/QuickAi-Plus.git
cd QuickAi/Community.PowerToys.Run.Plugin.QuickAi
dotnet build -c Release -p:Platform=x64
```

---

## 🔧 配置 / Configuration
- 支持 OpenAI Compatible / DeepSeek / OpenAI / Anthropic / Gemini / Cohere / Ollama 等 provider（原版功能）
- DeepSeek 用户：Base URL 填 `https://api.deepseek.com`（插件自动拼接 `/v1/chat/completions`）
- max_tokens 可在 PowerToys 设置里调整（默认 2048）

## 🏗️ 技术栈 / Tech Stack
- C# / .NET 9.0 / WPF
- WpfMath 2.1.0（LaTeX 渲染）
- PowerToys Run Plugin API 0.93+

## 📄 License
MIT License — 基于 [ruslanlap/PowerToysRun-QuickAi](https://github.com/ruslanlap/PowerToysRun-QuickAi)（Copyright (c) 2025 ruslanlap）改造，保留原版权声明。

## 🙏 Acknowledgements
- [ruslanlap/PowerToysRun-QuickAi](https://github.com/ruslanlap/PowerToysRun-QuickAi) — 原版项目
- [WpfMath / xaml-math](https://github.com/ForNeVeR/xaml-math) — LaTeX 渲染引擎
