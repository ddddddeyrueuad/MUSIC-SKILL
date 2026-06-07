---
name: score-maker
description: "🎼 乐队总谱自动生成 — 从音频/MIDI生成MusicXML五线谱→PDF乐谱→和弦级数谱→Whisper歌词转录→和弦歌词对齐。4引擎PDF渲染自动降级。支持批量队列处理。"
version: 2.7.0
tags:
  - sheet-music
  - musicxml
  - chord-analysis
  - lyrics-transcription
  - pdf-generation
  - music21
  - whisper
  - jianpu
category: media/audio
author: 风灯 (Feng Deng)
license: MIT
platforms:
  - windows
  - linux
  - macos
runtime: python
dependencies:
  - python>=3.8
  - music21
  - librosa
  - faster-whisper
  - gradio
  - numpy
  - scipy
---

# 🎼 Score Maker — 乐队总谱 + 和弦级数谱 + 歌词 自动生成

## 概述

制谱仔从音频生成完整的乐队总谱：MusicXML 五线谱 → PDF 谱面 → 和弦级数谱 → Whisper 歌词转录 → 和弦歌词对齐谱。支持简谱（数字谱）输出。

> **边界**：制谱仔不含音源分离。需要分轨时请先用 `stem-splitter`，再用其输出的 MIDI 配合音频来制谱。

## 核心流程

```
输入: 音频文件 + [可选: 分轨仔输出的 MIDI]
  │
  ├── Step 1: 音频 → 分轨（通过分轨仔模块）→ 每轨 MIDI
  ├── Step 2: music21 → MusicXML 多声部乐队总谱（4-6 声部）
  ├── Step 3: MIDI → 五线谱（MusicXML），duration 量化防 verovio 警告
  ├── Step 4: PDF 谱面渲染（4引擎自动降级）
  ├── Step 5: librosa 和弦分析 → 罗马级数谱
  ├── Step 6: Whisper 歌词转录（离线模型缓存）
  ├── Step 7: 歌词内联到和弦级数谱
  └── Step 8: 歌词注入 MusicXML → 和弦锚点插值对齐 → 重渲染带歌词 PDF
```

## PDF 渲染引擎

| 引擎 | 方式 | 平台 | 优先级 |
|------|------|------|:------:|
| A. **MuseScore CLI** | `mscore -o output.pdf input.musicxml` | Windows | 🥇 首选 |
| B. **Edge 无头模式** | verovio → SVG → HTML → msedge --headless --print-to-pdf | Windows | 🥈 |
| C. **verovio + svglib** | verovio → SVG → svglib → reportlab → PDF | 全平台 | 🥉 |
| D. **LilyPond** | lilypond 渲染 | 全平台 | 4th |

从 v6.2.1 开始，制谱仔在找不到 MuseScore 时会**自动下载并静默安装** MuseScore 4。

## 快速开始

### 安装依赖
```bash
pip install music21 librosa faster-whisper gradio numpy scipy soundfile
```

### CLI 使用
```bash
# 从音频生成完整乐谱
python main.py 歌曲.mp3 -o ./score

# 带 MIDI 输入（更准确的音符识别）
python main.py 歌曲.mp3 -m 歌曲.mid -o ./score --key C --bpm 85

# 跳过歌词转录（纯乐谱 + 和弦）
python main.py 歌曲.mp3 -o ./score --skip-lyrics
```

### WebUI
```bash
python webui.py -port 7862
```

## 输出文件

| 文件 | 说明 |
|------|------|
| `*_band_score.musicxml` | 🎼 MusicXML 五线谱 |
| `*_band_score.pdf` | 📄 PDF 谱面 |
| `*_score.mid` | 谱面对应 MIDI |
| `*_chords.txt` | 📝 和弦级数谱 |
| `*_chord_lyric.txt` | 🎤 和弦歌词对齐谱 |
| `*_lyrics.txt` | 纯歌词文本 |
| `*_jianpu.txt` | 🔢 简谱（数字谱 1234567） |

## 声部结构

```
┌─ vocals  (人声) ──── 主旋律
├─ piano   (钢琴) ──── 和声伴奏
├─ guitar  (吉他) ──── 和弦节奏
├─ bass    (贝斯) ──── 低音线条
├─ drums   (鼓)   ──── 节奏声部
└─ other   (其他) ──── 其余声部
```

## 版本历史

| 版本 | 日期 | 说明 |
|------|------|------|
| 2.7.0 | 2026-06-04 | 和弦锚点插值修复歌词同步 + MuseScore自动安装 |
| 2.5.0 | 2026-06-01 | 多声部乐器名映射修复 + PDF渲染4引擎降级 |
| 2.0.0 | 2026-05-31 | 独立项目代码打包 |
| 1.0.0 | 2026-05 | 初始版本 |
