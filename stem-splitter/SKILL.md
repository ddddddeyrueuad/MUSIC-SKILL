---
name: stem-splitter
description: "🎸 AI多轨音频分离 — BS-ROFO-SW 6轨分离 + 每轨3格式输出(WAV+MP3+MIDI)。GPU加速自动检测+OOM→CPU降级。回退Demucs 4轨。支持WebUI操作。"
version: 2.6.0
tags:
  - stem-separation
  - audio-splitting
  - bs-roformer
  - demucs
  - multi-track
  - midi-transcription
  - vocal-isolation
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
  - torch>=2.0
  - demucs
  - numpy
  - scipy
  - soundfile
  - librosa
  - basic-pitch
  - gradio
---

# 🎸 Stem Splitter — AI多轨音频分离 + 每轨MIDI转录

## 概述

分轨仔将音频分离为多个独立音轨，每轨输出 3 种格式：WAV（无损）+ MP3（通用）+ MIDI（可编辑）。支持 BS-ROFO-SW 6 轨分离和 Demucs 4 轨回退。

## 核心流程

```
源音频 → 引擎分离(BS-ROFO/Demucs) → 每轨3格式输出(WAV+MP3+MIDI)
```

## BS-ROFO-SW 6轨输出

```
./output/
├── vocals/  → vocals.wav + vocals.mp3 + vocals.mid   🎤 人声
├── drums/   → drums.wav  + drums.mp3  + drums.mid    🥁 鼓
├── bass/    → bass.wav   + bass.mp3   + bass.mid     🎸 贝斯
├── guitar/  → guitar.wav + guitar.mp3 + guitar.mid   🎸 吉他
├── piano/   → piano.wav  + piano.mp3  + piano.mid    🎹 钢琴
└── other/   → other.wav  + other.mp3  + other.mid    🎛️ 其他
```

### Demucs 4轨回退
```
├── vocals/  🎤 人声
├── drums/   🥁 鼓
├── bass/    🎸 贝斯
└── other/   🎛️ 其他（含吉他+钢琴）
```

## 快速开始

### 安装依赖
```bash
pip install torch torchaudio demucs numpy soundfile librosa basic-pitch gradio
pip install bs-roformer-infer -i https://pypi.org/simple/
```

### CLI 使用
```bash
# 6轨分离（默认）
python main.py input.mp3 -o ./output

# 强制 CPU 模式
python main.py input.mp3 -o ./output --force-cpu

# 指定 Demucs 引擎
python main.py input.mp3 -o ./output --engine demucs

# 跳过 MIDI 转录（只做音频分离）
python main.py input.mp3 -o ./output --skip-midi

# 批量处理
python main.py ./input_dir/ -o ./output --batch
```

### WebUI
```bash
python webui.py --port 7863
```

## 引擎对比

| 引擎 | 轨数 | 显存需求 | 5分钟歌曲 | 模型大小 |
|------|:----:|:--------:|:---------:|:--------:|
| BS-ROFO-SW | 6轨 | ~6GB | ~45s | 668MB |
| Demucs | 4轨 | ~4GB | ~26s | 自动下载 |

## 回退链

```
BS-ROFO → [失败] → Demucs → [失败] → basic-pitch MIDI
```

## 显卡检测策略

| 场景 | 结果 |
|------|:----:|
| `--force-cpu` 参数 | 🔒 CPU |
| 无 CUDA / 无 NVIDIA 卡 | ⚠️ CPU |
| 显存 < 4GB | ⚠️ CPU |
| CUDA 实测分配失败 | ⚠️ CPU |
| 显存充足 | 🖥️ GPU |
| 推理时 OOM | → 自动 CPU 重试 |

## 输出格式说明

| 格式 | 适用场景 | 编码 |
|------|----------|------|
| WAV | 无损编辑/DAW导入 | PCM 16-bit 44.1kHz |
| MP3 | 通用分享/试听 | 320kbps CBR |
| MIDI | 打谱/编曲 | Standard MIDI File |

## 版本历史

| 版本 | 日期 | 说明 |
|------|------|------|
| 2.6.0 | 2026-06-04 | 模型下载源清理 + Windows中文路径修复 |
| 2.5.0 | 2026-06-01 | BS-ROFO import兼容 + OOM→CPU自动重试 + 显卡检测 |
| 2.0.0 | 2026-05-31 | 独立项目代码打包 |
| 1.0.0 | 2026-05 | 初始版本 |
