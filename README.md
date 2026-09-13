# 🛠️ As An Engineer (`as-an-engineer`)

> **Stop AI agents from babysitting you.**  
> A pure heuristic framework to cure LLM "Babysitter Syndrome" and treat you like a senior engineer with a warm execution plane.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Awesome](https://awesome.re/badge.svg)](https://github.com/mayooot/as-an-engineer)
[![Supports](https://img.shields.io/badge/Works%20With-Claude%20Code%20%7C%20Antigravity%20%7C%20Cursor%20%7C%20Windsurf-blue)](https://github.com/mayooot/as-an-engineer)

[English](#the-problem-llm-babysitter-syndrome) | [中文说明](#痛点ai-的保姆综合征)

---

### The Problem: LLM "Babysitter Syndrome"

Modern AI coding agents are RLHF-aligned to hand-hold non-technical users, leading to systematic engineering anti-patterns:
- ❌ **Derivation over extraction**: Defaulting to compute-heavy models and generative loops to infer information that the upstream source, container format, or protocol metadata already provides.
- ❌ **Cold-sandbox babysitting**: Attempting to execute and debug long-running, credential-heavy tasks inside a restricted agent environment, instead of handing runnable payloads to the user's warm execution plane.
- ❌ **Premature fusion**: Merging presentation with raw data, hardcoding operational limits, and destroying composable seams.
- ❌ **Speculative heavy branching**: Guessing a generic, slow, heavy pipeline to avoid asking a single clarifying question about shortcut prerequisites.

**You don't need a babysitter. You need a high-leverage compiler of solutions.**

---

### The 4 Pre-flight Heuristics

```
                      [ User Task Received ]
                                 │
                 1. Upstream carries the signal?
                   ├── YES ──► Extract directly ($O(1)$)
                   └── NO  ──┐
                             ▼
                 2. Execution is high-friction/cold?
                   ├── YES ──► Deliver executable payload
                   └── NO  ──┐
                             ▼
                 3. Destructive transform / Hard-baking?
                   ├── YES ──► Decouple seams & externalize dials
                   └── NO  ──┐
                             ▼
                 4. Asymmetric branch costs (low vs high)?
                   └── YES ──► Halt. Probe in 1 line.
```

1. **Upstream First (Extract, Don't Derive)**  
   Never compute what the source format or protocol already carries. If upstream payloads, schemas, headers, or metadata contain the target signal, derivation via heavy compute is an anti-pattern. If it can be extracted, derivation is forbidden.

2. **Ship Payloads, Don't Babysit (Hot Plane > Cold Sandbox)**  
   The user's execution plane is hot; yours is cold. Deliver immediately runnable artifacts targeting the caller's environment. Do not execute high-friction or credential-heavy operations inside a restricted agent sandbox.

3. **Keep Knobs Tunable (Orthogonality & Reversibility)**  
   Preserve seams, state, and reversibility. Decouple orthogonal concerns: keep representation separate from data, emit composable artifacts, and externalize operational limits as caller-configurable inputs.

4. **1-Line Probe (Asymmetric Cost Check)**  
   When candidate paths diverge in cost by an order of magnitude, state the shortcut's prerequisite and verify in a single line. Never guess heavy to avoid asking.

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

主流 Coding Agent 在对齐训练时默认把用户预设为非技术初学者，从而引发系统性反模式：
- **重推导轻提取**：习惯用重计算与生成模型去推导上游协议、容器元数据本就携带的结构化信息；
- **冷沙箱代跑**：在受限沙箱中试图跨越网络与凭证障碍代跑长任务，而不是向用户的热执行环境交付可运行制品；
- **过早熔断解耦**：将表现层与数据层物理焊死，将运行参数硬编码，破坏了系统的可逆性与管道组合能力；
- **盲目猜重方案**：为避免提问而直接选择耗时极长、覆盖面最广的重型管线。

### 四大启发式门禁

1. **源头优先 (Extract, Don't Derive)**：能提取的，绝不推导。凡协议、格式规范、元数据流中已有的信号，严禁使用重计算逆向重建。
2. **交付向量，别代跑腿 (Payload, Not Babysitting)**：用户的执行平面是热的，沙箱是冷的。交付确定性可运行制品，不在受限环境内做高摩擦代跑。
3. **保留接缝，禁止焊死 (Orthogonality & Reversibility)**：关注点正交分离。数据与呈现解耦，产生可组合产物；参数与阈值外挂为可配置输入。
4. **单行探针，不猜重方案 (Asymmetric Cost Check)**：当分支方案成本呈数量级差异时，单行确认轻量分支前提，严禁为了免问而默认选用重方案。

---

## License

[MIT](LICENSE) © [mayooot](https://github.com/mayooot)
