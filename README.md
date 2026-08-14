# 🤖 QuickAI Plus for PowerToys Run

**English** | [**中文**](README.zh-CN.md)

A feature-packed enhanced fork of [ruslanlap/PowerToysRun-QuickAi](https://github.com/ruslanlap/PowerToysRun-QuickAi) v1.2.1 (MIT License, original copyright preserved).

AI-powered assistance right inside PowerToys Run — now with **LaTeX math rendering**, **rich block-level Markdown**, a **compact sticky-note window**, and **multi-turn follow-up chat**.

---

## ✨ What's New vs Original v1.2.1

### 🧮 LaTeX Math Rendering
- Supports `$$...$$`, `\(...\)`, `\[...\]`, `$...$` formula syntax
- Rendered as real math via [WpfMath 2.1.0](https://www.nuget.org/packages/WpfMath): fractions, radicals, integrals, matrices
- Smart LaTeX sanitizing:
  - Strips environment wrappers (`\begin{align}` / `\begin{array}` / `\begin{cases}` etc.)
  - Converts `\text{中文}` → `\mathrm{...}`
  - Handles multi-letter operators (`\arccot`, `\arcsec`, `\argmax`, `\coth`, `\sech` etc.) → `\mathrm{}`
  - Removes unsupported commands (`\displaystyle`, `\color`, `\tag`, `\hline` etc.)
- **No more red-dot errors**: if rendering fails (`FormulaControl.HasError`), falls back to showing the raw LaTeX text

### 📝 Block-level Markdown
- `#` – `######` headings (size-graded, bold)
- `>` blockquotes (left accent bar + gray background)
- `-` / `*` / `+` unordered lists, `1.` ordered lists
- `---` / `***` horizontal rules
- `| col1 | col2 |` Markdown tables (bold header, thin borders, auto-fit width)
- Blank-line paragraph separation; inline bold/italic/code preserved

### 🏷️ Compact Sticky-note Window
- Result window shrunk from 850×650 to **560×430 compact card**
- Borderless, rounded corners + shadow, **always on top**
- Defaults to bottom-right of the screen (like a sticky note), draggable via header
- Minimal header: Wrap / Copy / Close buttons

### 💬 Follow-up Chat
- Built-in **follow-up input box + send button** at the bottom of the sticky note (native Windows controls, clean look)
- **Multi-turn context**: follow-ups carry the full conversation history to the AI
- Chat-style display: your question appears with a ❓ marker, new answers stream in below
- `· Thinking...` status while AI responds; input locked to prevent duplicate sends

### ⚡ Performance
- Throttled streaming render (~220ms batching) — fixes the lag caused by re-rendering the whole document per token
- Smooth scrolling; final polished render after streaming completes

### 🔧 Other Improvements
- Global sans-serif font (Segoe UI), math and text visually consistent
- `max_tokens` default raised to 2048 (adjustable in settings)
- **WpfMath load fix**: PowerToys' plugin loader doesn't probe deps.json; loads WpfMath explicitly via `AssemblyLoadContext.Resolving` callback

---

## 📥 Installation

### Option 1: Download Release (recommended)
Grab the latest `QuickAi.zip` from [Releases](https://github.com/Greyaircraft/QuickAi-Plus/releases), then:

1. **Copy the whole `QuickAi` folder** into the PowerToys Run plugin directory:
   ```
   %LOCALAPPDATA%\Microsoft\PowerToys\RunPlugins\QuickAi\
   ```
   > ⚠️ Note: new PowerToys uses `RunPlugins\` for third-party plugins, **not** `PowerToys Run\Plugins\` (that's for built-in plugins)

2. **Make sure `WpfMath.dll` and `XamlMath.Shared.dll` sit next to the main DLL** (already included in the release package)

3. **Restart PowerToys** (tray icon → right-click → Exit → relaunch)

4. **Configure API key**: PowerToys Settings → PowerToys Run → Plugins → QuickAI

### Option 2: Build from Source
```powershell
# Requires .NET SDK 9.0+
git clone https://github.com/Greyaircraft/QuickAi-Plus.git
cd QuickAi/Community.PowerToys.Run.Plugin.QuickAi
dotnet build -c Release -p:Platform=x64
```

---

## 🔧 Configuration
- Supports OpenAI Compatible / DeepSeek / OpenAI / Anthropic / Gemini / Cohere / Ollama providers (original feature)
- DeepSeek users: set Base URL to `https://api.deepseek.com` (the plugin appends `/v1/chat/completions` automatically)
- `max_tokens` adjustable in PowerToys settings (default 2048)

## 🏗️ Tech Stack
- C# / .NET 9.0 / WPF
- WpfMath 2.1.0 (LaTeX rendering)
- PowerToys Run Plugin API 0.93+

## 📄 License
MIT License — enhanced fork of [ruslanlap/PowerToysRun-QuickAi](https://github.com/ruslanlap/PowerToysRun-QuickAi) (Copyright (c) 2025 ruslanlap), original copyright preserved.

## 🙏 Acknowledgements
- [ruslanlap/PowerToysRun-QuickAi](https://github.com/ruslanlap/PowerToysRun-QuickAi) — original project
- [WpfMath / xaml-math](https://github.com/ForNeVeR/xaml-math) — LaTeX rendering engine
