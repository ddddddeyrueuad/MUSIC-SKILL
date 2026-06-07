---
name: detection-bypass
description: "🔍 AI原创检测绕过处理器 — 15种检测方案下拉选择。SubmitHub通过标准：光谱Human≥50%/时域Human≥50%。R5hq方案已达标(58%/56%)。WebUI内置Kliga检测集成。"
version: 15.0.0
tags:
  - ai-detection
  - originality-check
  - submit-hub
  - audio-bypass
  - rubberband
  - mmm-phase-noise
  - spectral-processing
  - temporal-processing
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
  - ffmpeg>=4.4
  - numpy
  - scipy
  - soundfile>=0.12
  - librosa
  - gradio
---

# 🔍 Detection Bypass — AI原创检测绕过处理器

## 概述

检测仔是专为绕过 AI 原创检测而设计的音频处理工具。采用多种信号处理技术（相位噪声、移调、混响、动态处理等），使 AI 检测器将处理后的音频识别为"人类创作"。

## 核心理念

### 推荐方案：R5hq ✅（已通过 SubmitHub 标准）
```
rubberband -3半音 + 轻phaser + 动态±0.5dB + 房间混响25/55ms×0.07 + 本底噪声-75dB + 高频补偿+4dB@7kHz
```

### 两条技术路线（不可杂交）
| 路线 | 原理 | 光谱Human | 时域Human |
|------|------|:---------:|:---------:|
| **R5hq（移调系）** | rubberband -3 + phaser + 混响 | **58%** ✅ | **56%** ✅ |
| **MMM（相位系）** | FFT相位噪声 + 子块抖动 | 9% ❌ | **84%** 🏆 |

## SubmitHub 通过标准

```
光谱分析: Human ≥ 57% (could be) / Hybrid ≤ 32% / Pure AI ≤ 11%
时域分析: Human ≥ 42% (could be) / Pure AI ≤ 6%
```

## 快速开始

### 安装依赖
```bash
pip install numpy scipy soundfile librosa gradio
# 确保 FFmpeg 已安装
```

### CLI 使用
```bash
# R5hq 模式（推荐，默认）
python main.py input.mp3 -o output.mp3

# M3 模式（MMM全手法）
python main.py input.mp3 -o output.mp3 --mode m3

# M3B 模式（双遍处理）
python main.py input.mp3 -o output.mp3 --mode m3b

# 批量处理
python main.py ./input_dir/ -o ./output/ --batch --mode r5hq
```

### WebUI
```bash
python webui.py --port 7861
# → 浏览器打开 http://localhost:7861
```

## 所有可用模式

| 模式 | 策略 | 光谱Human | 时域Human | 音质 | 状态 |
|------|------|:---------:|:---------:|:----:|:----:|
| **R5hq** 🏆 | rubberband -3 + phaser + 混响 + 底噪 + 高频补偿 | **58%** | **56%** | ✅ | **已达标** |
| R5 | rubberband -3 + phaser + 房间混响 | 63% | 55% | ⚠️ 闷 | 历史最佳检测 |
| R8 | R5 + 高频补偿调整 | 60% | 52% | ⚠️ 人声闷 | 备选回退 |
| M3 v3 | MMM全手法8项（无MFCC） | Human 6% | **42%** | ✅ 零变化 | 时域最佳 |
| M3B v7 | 全手法减半 + R系微调 | Hybrid 80% | Hybrid 79% | ✅ 最佳平衡 | 纯相位天花板 |
| MMM v1 | 纯FFT相位噪声 + 起音 + HF + RBJ | Human 5% | Human 1% | ✅ 零变化 | 保音质备选 |
| MR | MMM + 极轻混响 | Pure AI 84% ❌ | Hybrid 81% | ✅ | 已废弃 |

## 检测验证

- **SubmitHub AI Song Checker** — 唯一检测标准（只接受公开 URL）
- **内置检测器** — 基于 librosa MFCC + chroma KNN（仅供参考）
- **Kliga 集成** — WebUI 中一键检测（自动上传 tmpfiles.org）

## 输出文件

| 文件 | 说明 |
|------|------|
| `output.mp3` | 处理后的音频文件（已绕过检测） |
| `原始文件名_对比.wav` | 处理前后波形对比（WebUI 生成） |

## 版本历史

| 版本 | 日期 | 说明 |
|------|------|------|
| 15.0.0 | 2026-06-03 | MMM修复版SubmitHub验证 + R5hq/MMM互补发现 |
| 12.0.0 | 2026-06-03 | M3B v10-v11 + 铁律确立 |
| 10.0.0 | 2026-06-03 | M3模式（MMM全7项手法） |
| 9.0.0 | 2026-06-03 | R9: MMM集成方案 |
| 7.0.0 | 2026-06-03 | R7: 微音高漂移 |
| 1.0.0 | 2026-05 | 初始版本 |
