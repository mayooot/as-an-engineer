# 🛠️ As An Engineer (`as-an-engineer`)

> **Stop AI agents from babysitting you.**  
> A 30-line heuristic skill to cure LLM "Babysitter Syndrome" and treat you like a senior engineer with a warm terminal.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Awesome](https://awesome.re/badge.svg)](https://github.com/mayooot/as-an-engineer)
[![Supports](https://img.shields.io/badge/Works%20With-Claude%20Code%20%7C%20Antigravity%20%7C%20Cursor%20%7C%20Windsurf-blue)](https://github.com/mayooot/as-an-engineer)

[English](#the-problem-llm-babysitter-syndrome) | [中文说明](#痛点ai-的保姆综合征)

---

### The Problem: LLM "Babysitter Syndrome"

Modern AI coding agents are heavily RLHF-aligned to hand-hold non-technical users. When you ask them to build or debug something:
- ❌ **They over-compute**: You ask for video subtitles—they spin up Whisper STT and burn subtitles into the MP4 (wasting 20 mins & 100k tokens), completely ignoring that the platform or container already provides clean `.vtt` tracks.
- ❌ **They babysit execution**: You ask for database progress—they attempt to probe your K8s namespaces, SSH across jump hosts, and time out inside a cold sandbox, instead of handing you a 2-second SQL query to paste into your already-connected shell.
- ❌ **They weld things shut**: They hardcode magic timeouts and merge views with data, destroying intermediate artifacts.

**You don't need a babysitter. You just need a high-leverage code compiler.**

---

### The 4 Pre-flight Heuristics

```
                      [ User Task Received ]
                                 │
                 1. Upstream has metadata?
                   ├── YES ──► Extract immediately ($O(1)$)
                   └── NO  ──┐
                             ▼
                 2. Execution is expensive/cold?
                   ├── YES ──► Deliver executable payload (SQL/Shell)
                   └── NO  ──┐
                             ▼
                 3. Destructive / Hard-baking?
                   ├── YES ──► Decouple into sidecars & flags
                   └── NO  ──┐
                             ▼
                 4. Asymmetric branch costs (5s vs 20m)?
                   └── YES ──► Stop. Probe in 1 line.
```

1. **Upstream First (Extract, Don't Derive)**  
   If container metadata, protocols, or HTTP headers have it, derivation via STT, OCR, DOM rendering, or blind embeddings is forbidden.
2. **Ship Payloads, Don't Babysit (Hot Shell > Cold Sandbox)**  
   Your shell has credentials and speed; the agent sandbox is cold. Deliver immediately executable vectors (precise SQL, 1-liner shell, single-file scripts).
3. **Keep Knobs Tunable (Decouple & Sidecar)**  
   Never hard-bake views into data. Output sidecars (`.srt`, `.json`) and streams. Expose thresholds and concurrency as CLI flags/env vars.
4. **1-Line Probe (Asymmetric Cost Check)**  
   If a choice is between a 5-second privileged shortcut and a 20-minute generic pipeline, ask **one line**. Never guess heavy to avoid asking.

---

### Quick Install

#### Antigravity / Agent Skill Standard
```bash
mkdir -p .agents/skills/as-an-engineer
curl -fsSL https://raw.githubusercontent.com/mayooot/as-an-engineer/main/SKILL.md -o .agents/skills/as-an-engineer/SKILL.md
```

#### Claude Code
Append to your global `~/.claude/CLAUDE.md` or workspace `CLAUDE.md`:
```bash
curl -fsSL https://raw.githubusercontent.com/mayooot/as-an-engineer/main/rules/CLAUDE.md >> CLAUDE.md
```

#### Cursor
Save to `.cursorrules`:
```bash
curl -fsSL https://raw.githubusercontent.com/mayooot/as-an-engineer/main/rules/.cursorrules -o .cursorrules
```

#### Global Rule (Antigravity / Generic Agents)
```bash
mkdir -p ~/.gemini/config
curl -fsSL https://raw.githubusercontent.com/mayooot/as-an-engineer/main/rules/AGENTS.md >> ~/.gemini/config/AGENTS.md
```

---

## 中文说明

### 痛点：AI 的“保姆综合征”

主流 Coding Agent 在对齐训练时默认把所有用户当成初学者：
- **无脑上重模型**：要视频字幕，它启动 Whisper 耗时 20 分钟转录并烧进像素，却无视上游本就有现成的 `.vtt` 轨道；
- **死守冷沙箱代跑**：要查海量数据进度，它在受限沙箱里跨网络翻 Pod、探 SSH，卡死超时，也不肯直接给你一条 2 秒就能回车跑完的 SQL；
- **不可逆焊死**：把配置写死、把表现层与数据层物理烧录，毁掉中间状态。

### 四大启发式门禁

1. **源头优先**：能提取的，绝不推导。严禁使用重算力去反推协议和容器本身就携带的结构化信息。
2. **交付向量，别代跑腿**：用户的终端是热的，沙箱是冷的。交付立即可跑的制品，不要在沙箱里当低效保姆。
3. **保留接缝，禁止焊死**：正交解耦，产出旁挂文件，旋钮外挂为 flags / 环境变量。
4. **单行探针，不猜重方案**：当分叉意味着“5秒特权解”与“20分钟通用解”时，单行询问，绝不自作主张选重方案。

---

## License

[MIT](LICENSE) © [mayooot](https://github.com/mayooot)
