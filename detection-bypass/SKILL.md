---
name: detection-bypass
description: "检测仔 — AI原创检测绕过处理器方案。🏆(H+方案)实测SubmitHub光谱Human 78%/时域Human 91% Human made 🎉。"
version: 6.4.0
tags: [detection-bypass, originality-check, ai-detection, submit-hub]
platforms: [windows, linux, wsl]
triggers:
  - 原创检测绕过
  - AI检测绕过
  - 检测仔
  - 过原创检测
   
---
# 🔍 检测仔 — AI原创检测绕过处理器

**🏆 推荐方案：方案1+（H+）** — SubmitHub实测光谱Human 78%/时域Human 91%，音质基本无损



## SubmitHub 达标标准

```
Spectral:      Human ≥ 57% (could be)
Temporal:      Human ≥ 42% 或 Hybrid ≥ 53% (could be)
Pure AI:       ≤ 20% (probably not)
```

## 用法

### 桌面版 WebUI
1. 双击 `start.bat` 启动
2. 点 **检测仔** 标签
3. 下拉选 **方案号**（默认 1+）
4. 上传音频 → 点 **开始处理**
5. 下载输出 MP3 → 到 [SubmitHub AI Song Checker](https://www.submithub.com/ai-song-checker) 验证


### 系统要求
- Python 3.10+
- FFmpeg（已打包在安装包内）

## 检测工具

**唯一验证工具：** [SubmitHub AI Song Checker](https://www.submithub.com/ai-song-checker)

SubmitHub 使用 Meteor DDP 协议（WebSocket），无法通过 HTTP 自动化检测。需手动上传处理后 MP3 验证。

> ⚠️ 内置检测器(M3B)与SubmitHub无线性关系，分数仅供参考。最终验证必须SubmitHub。

## 文件结构

```text
~/.hermes/skills/media/detection-bypass/
├── SKILL.md                     ← 本文档
├── main.py                      ← 检测引擎主代码
├── webui.py                     ← 独立WebUI
└── references/                  ← 参考文档
    ├── detection-algorithm.md           ← 内置检测算法
    ├── windows-deployment.md            ← Windows部署
    ├── audiocleaner-kb-extraction.md    ← AudioCleaner Pro参数提取方法
    └── webui-terminal-cleanup.md        ← UI清理规范
```
