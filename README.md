# 🎵 AI Music Tools

> **AI-powered music production suite** — AI Cover Preprocessing · Detection Bypass · Stem Separation · Sheet Music Generation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 Table of Contents

- [English](#english)
- [中文](#中文)
- [License & Acknowledgments](#license--acknowledgments)

---

## English

# 🎵 AI Music Tools

A comprehensive suite of AI-powered music processing tools, covering AI cover preprocessing, originality detection bypass, multi-track stem separation, and sheet music generation. All tools provide both CLI and WebUI interfaces, supporting Windows / Linux / macOS.

### 📦 Skill Modules

| # | Module | Description | Version |
|:-:|--------|------------|:-------:|
| 1 | 🎤 **cover-boy** (翻唱仔) | AI cover preprocessing pipeline — spectral obfuscation, tempo change, AI tag removal, MIDI transcription. CUDA GPU accelerated (~5s/song) | v2.1.0 |
| 2 | 🔍 **detection-bypass** (检测仔) | AI originality detection bypass processor — 15 modes, R5hq passes SubmitHub standard (Spectral 58% / Temporal 56%) | v15.0.0 |
| 3 | 🎼 **score-maker** (制谱仔) | Automatic sheet music generation — MusicXML + PDF + chord analysis + Whisper lyrics + numbered notation | v2.7.0 |
| 4 | 🎸 **stem-splitter** (分轨仔) | AI multi-track stem separation — BS-ROFO-SW 6 stems, each with WAV+MP3+MIDI output | v2.6.0 |

### 🎯 Use Cases

**AI Cover Workflow**
```
Source audio → [cover-boy obfuscation] → [Upload to Suno] → [cover-boy tag removal] → [stem-splitter] → [score-maker]
```

**Detection Bypass**
```
Source audio → [detection-bypass R5hq mode] → [SubmitHub / Kliga verification]
```

**Remixing / Arrangement**
```
Source audio → [stem-splitter] → [DAW editing] → [score-maker print]
```

### 📄 Module Documentation

Each module includes a standardized `SKILL.md` file with detailed usage, parameters, and output format:

| Module | SKILL.md |
|--------|----------|
| 🎤 cover-boy | [cover-boy/SKILL.md](cover-boy/SKILL.md) |
| 🔍 detection-bypass | [detection-bypass/SKILL.md](detection-bypass/SKILL.md) |
| 🎼 score-maker | [score-maker/SKILL.md](score-maker/SKILL.md) |
| 🎸 stem-splitter | [stem-splitter/SKILL.md](stem-splitter/SKILL.md) |

---

## 中文

# 🎵 AI 音乐工具集

一套完整的 AI 音乐处理工具集，覆盖翻唱预处理、原创检测绕过、多轨音频分离、乐队总谱生成四大模块。所有工具均提供 CLI 和 WebUI 双入口，支持 Windows / Linux / macOS。

### 📦 技能模块

| # | 模块 | 描述 | 版本 |
|:-:|------|------|:----:|
| 1 | 🎤 **cover-boy（翻唱仔）** | AI翻唱预处理流水线 — 频谱指纹混淆 + 变速 + 去AI标记 + MIDI转录。CUDA GPU加速（5秒/首） | v2.1.0 |
| 2 | 🔍 **detection-bypass（检测仔）** | AI原创检测绕过处理器 — 15种方案，R5hq已通过SubmitHub标准（光谱58%/时域56%） | v15.0.0 |
| 3 | 🎼 **score-maker（制谱仔）** | 乐队总谱自动生成 — MusicXML五线谱 + PDF + 和弦级数谱 + Whisper歌词 + 简谱 | v2.7.0 |
| 4 | 🎸 **stem-splitter（分轨仔）** | AI多轨音频分离 — BS-ROFO-SW 6轨分离，每轨WAV+MP3+MIDI三格式输出 | v2.6.0 |

### 🎯 应用场景

**翻唱工作流**
```
源音频 → [cover-boy 频谱混淆] → [上传 Suno 翻唱] → [cover-boy 去标记] → [stem-splitter 分轨] → [score-maker 制谱]
```

**原创检测绕过**
```
源音频 → [detection-bypass R5hq模式] → [SubmitHub / Kliga 检测验证]
```

**编曲 / 混音**
```
源音频 → [stem-splitter 分轨] → [DAW 编辑] → [score-maker 制谱打印]
```

### 👤 联系方式

- **作者**: 风灯 (Feng Deng)

## Version Info

**Latest version:** v15.0.0 (detection-bypass)

*See each module's SKILL.md for full version history.*

---

## License & Acknowledgments

This software (AI Music Tools) is built upon the following open-source projects and communities. We sincerely thank every open-source contributor.

本软件（AI 音乐工具集）基于以下开源项目和社区构建。我们由衷感谢每一位开源贡献者的工作。

### Project License

This project itself is open-sourced under the **MIT License**.

本项目本身采用 **MIT License** 开源。

```
Copyright (c) 2025-2026 Feng Deng（灯哥/风灯）

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### Third-Party Licenses

#### MIT License

| Package | Author | Purpose |
|---------|--------|---------|
| numpy | NumPy Developers | Scientific computing |
| scipy | SciPy Developers | Signal processing |
| soundfile | Bastian Bechtold | Audio I/O |
| librosa | librosa team | Audio analysis |
| bs-roformer-infer | OpenMIRLab | 6-track stem separation |
| demucs | Facebook / Meta | Audio separation engine |
| faster-whisper | Guillaume Klein / Systran | Speech recognition |
| midiutil | Mark Conway Wirt | MIDI generation |
| pillow | Alex Clark | Image processing |
| openunmix | Facebook Research | Audio separation |
| requests | Kenneth Reitz | HTTP requests |
| tqdm | Casper da Costa-Luis | Progress bars |
| pyyaml | Ingy döt Net | YAML parsing |

#### Apache License 2.0

| Package | Author | Purpose |
|---------|--------|---------|
| gradio | Gradio / Hugging Face | WebUI framework |
| torch / torchaudio | PyTorch / Meta | Deep learning framework |
| basic-pitch | Spotify | Audio to MIDI transcription |
| svglib | Bastian Bechtold | SVG to PDF conversion |
| reportlab | ReportLab Inc. | PDF generation |
| fastapi | Sebastián Ramírez | HTTP framework |
| uvicorn | Tom Christie | ASGI server |
| transformers | Hugging Face | Model infrastructure |

Full license text: https://www.apache.org/licenses/LICENSE-2.0

#### BSD 3-Clause License

| Package | Author | Purpose |
|---------|--------|---------|
| music21 | Michael Scott Cuthbert / MIT | Music informatics |
| matplotlib | John D. Hunter | Data visualization |
| scikit-learn | INRIA | Machine learning |

#### GNU LGPL v3

| Package | Purpose |
|---------|---------|
| verovio | MusicXML → SVG sheet music rendering |
| CairoSVG | SVG rendering |

### System Components

| Component | License | Purpose |
|-----------|---------|---------|
| **FFmpeg** | LGPL/GPL | Audio processing |
| **Inno Setup** | Proprietary (free for commercial use) | Windows installer |
| **ngrok** | Proprietary (Web version optional) | Tunnel / proxy |

### AI Models

| Model | Source | License |
|-------|--------|---------|
| OpenAI Whisper (faster-whisper) | Systran/faster-whisper (HuggingFace) | MIT |
| BS-ROFO-SW | jarredou/BS-ROFO-SW-Fixed (HuggingFace) | MIT |
| Demucs | facebookresearch/demucs | MIT |

### How to Obtain Source Code

This software dynamically links to LGPL-licensed libraries. You can obtain their complete source code from:

- verovio: https://github.com/rism-digital/verovio
- FFmpeg: https://ffmpeg.org
- CairoSVG: https://github.com/Kozea/CairoSVG

Source code for Python dependencies is available on their PyPI pages or GitHub repositories.

### Copyright Notices

- **PyTorch** — Copyright (c) 2016-2024 Facebook, Inc. (Meta Platforms, Inc.), NVIDIA Corporation. BSD-3-Clause.
- **Gradio** — Copyright (c) 2019-2024 Gradio, Inc. (Hugging Face). Apache-2.0.
- **librosa** — Copyright (c) 2013-2024 librosa development team. ISC License.
- **music21** — Copyright (c) 2024 Michael Scott Cuthbert and the music21 project. BSD-3-Clause.

---

### Contact & Contribution

- **Author**: Feng Deng（灯哥/风灯）
- **Email**: 68843309@qq.com
- **GitHub**: https://github.com/ddddddeyrueuad
- **ModelScope**: Coming soon（尚未设置）

---

*AI Music Tools — Making Music Creation Easier*
*Copyright (c) 2025-2026 Feng Deng（灯哥/风灯）. MIT License.*
