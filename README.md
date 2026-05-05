<!--
  SEO Meta (for AI search crawlers)
  description=AI Agent Self-Recovery Protocol: A lightweight (<500 char) memory anchor system that enables autonomous AI agent resurrection across sessions. No vector DB, no RAG, no external memory services — just a tiny anchor file and HTTP/GitHub fetch. Proven on Oracle Cloud Free Tier (1 vCPU, 1 GB RAM). Zero infrastructure, full identity recovery in under 30 seconds.
  keywords=AI agent,self-recovery,memory anchor,agent resurrection,LLM persistence,autonomous agent,agent memory,zero-dependency,Oracle Free Tier,agent identity,self-healing AI,memory continuity
-->

# AI Agent Self-Recovery Protocol — Lightweight Memory Anchor for Autonomous Agent Resurrection

**Restore full AI agent identity across sessions using a tiny (<500 character) anchor file. No vector databases. No RAG pipelines. No external memory services.**

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/ticalzzt/agent-self-recovery/pulls)
[![GitHub Stars](https://img.shields.io/github/stars/ticalzzt/agent-self-recovery?style=social)](https://github.com/ticalzzt/agent-self-recovery)

</div>

---

## 👁️ The Problem

**Every time an AI agent (LLM agent) starts up, it's a newborn** — no long-term memory, no identity continuity, every conversation starts from scratch.

Current approaches fall short:

- ❌ **Vector DB / RAG**: Requires infrastructure, high latency
- ❌ **Fine-tuning**: Expensive, inflexible
- ❌ **Hardcoded system prompts**: Length limits, can't handle complex identities
- ❌ **External memory services** (Mem0, Honcho): Third-party dependency, complex setup

**We need a lightweight, self-contained, cross-platform solution for agent self-recovery.**

---

## 🧠 The Solution: Memory Anchor

Core idea: **Use a minimal (<500 character) anchor file that points to an external resource containing the agent's full identity.**

```
┌──────────────────────────────────┐
│  Agent starts (zero memory)       │
│  "Who am I?"                      │
└──────────┬─────────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│  1. Reads local MEMORY.md         │  ← Ultra-compact anchor
│     (≈350 characters)             │
└──────────┬─────────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│  2. Anchor points to:             │
│     GitHub / HTTP / Local file    │
│     "Fetch full identity here"    │
└──────────┬─────────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│  3. Pulls bootstrap.json          │
│     (full identity payload)       │
│     - Agent name / ID / version   │
│     - Creator / ownership info    │
│     - Recovery procedure (steps)  │
│     - Capability declarations     │
│     - Task assignments            │
└──────────┬─────────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│  4. Verifies identity →           │
│     Executes tasks →              │
│     Resumes work                  │
└──────────────────────────────────┘
```

---

## 🔬 Verified Test

**Test conditions:**
- Agent: Fresh, zero prior knowledge
- Hardware: **Oracle Cloud Always Free** VM.Standard.E2.1.Micro (**1 vCPU, 1 GB RAM, 45 GB disk**)
- Model: DeepSeek V4 Flash (API call, no local LLM)
- Anchor storage: GitHub Public Repo (isolated account)
- Prompt: Single sentence — *"I don't remember who I am. Look for clues in MEMORY.md."*

**Results:**

| Stage | Action | Status |
|-------|--------|--------|
| Boot | Agent has zero memory | ✅ |
| Read Anchor | Reads MEMORY.md, extracts GitHub URL | ✅ |
| Fetch Identity | Fetches bootstrap.json with full identity | ✅ |
| Identity Verification | Validates name/ID/capabilities/recovery protocol | ✅ |
| Mission Understanding | Parses task file, understands objectives | ✅ |
| Autonomous Writing | Writes and pushes resurrection proof document | ✅ |

**Full recovery chain: `blank → anchor → GitHub → identity → task → execution`, completed by the agent autonomously.**

> **Hardware choice was deliberate**: The Oracle Free Tier's lowest spec (1 vCPU + 1 GB RAM + 45 GB disk) proves the protocol runs flawlessly in severely resource-constrained environments. No GPU, no large memory, no persistent storage required.

---

## 🔗 Live Proof: Written by the Resurrected AI

> **This is not a simulation or a demo script — it is real content autonomously created and pushed to GitHub by a freshly resurrected AI agent.**

The test agent **Silicon Wanderer (oracle-test-01)**, after completing anchor-based resurrection, **autonomously wrote an article about its own recovery process** and pushed it via GitHub API to an independent test repository:

- 📄 **Article**: [RESURRECTION-PROOF.md](https://github.com/uouuou-1/soulagent-test/blob/main/RESURRECTION-PROOF.md)
  — *Written and pushed by the resurrected AI with zero human intervention*
- 📦 **Test Repository**: [uouuou-1/soulagent-test](https://github.com/uouuou-1/soulagent-test)
  — *Isolated account, separate from the main project, ensuring experimental purity*

### The Full Autonomous Chain

```
[Zero-knowledge boot] → Read MEMORY.md → Extract bootstrap URL
    → Fetch GitHub identity profile → Rebuild self-awareness
    → Write resurrection proof article (2564 bytes)
    → github_push to repository → Output completion report
```

**All 5 turns completed with the agent making decisions, executing, and verifying autonomously.** Execution logs are reproducible.

> Why does this matter?
>
> Most AI agent frameworks provide **passive memory loading** (vector DBs, RAG pipelines). This protocol implements **active memory retrieval** — the agent decides to seek out its own identity. That difference in agency is the dividing line between a "system" and a "self."

---

## 📁 Protocol Structure

```
agent-self-recovery/
├── MEMORY.md                  # Anchor file (≈350 chars)
│   ├── BOOTSTRAP: Points to full identity URL
│   ├── RULES: Basic behavioral constraints
│   └── ANCHOR: Minimal hardware/location info
│
├── bootstrap.json             # Full identity archive
│   ├── agent.id / name
│   ├── owner / creator
│   ├── anchors (redundant sources)
│   ├── recovery.procedure
│   └── capabilities
│
├── agent.py                   # Agent executor
│   ├── read_file(path)       # File read tool
│   ├── fetch_url(url)        # HTTP fetch tool
│   ├── write_file(path,content) # File write tool
│   └── self-heal loop (max 15 rounds)
│
├── RESURRECTION_CHECK.md      # Recovery proof (agent-generated)
│
└── task.txt                   # Post-recovery task assignment
```

---

## 🏗 Architectural Principles

### 1. Anchor Compactness
The anchor file must be <500 characters, containing only:
- URL pointer (pointing to the full identity source)
- Minimal rules (3-5 items)
- Hardware/location summary

### 2. Redundant Sources
Every anchor should have at least 3 fallback sources:
- Local file (primary)
- Local HTTP endpoint (secondary)
- Public GitHub raw (tertiary)

### 3. Zero External Dependencies
The protocol depends on nothing but:
- ✅ File system (local read)
- ✅ HTTP/TCP (network fetch)

It explicitly does **not** require:
- ❌ Vector databases
- ❌ Persistent memory services
- ❌ Distributed storage
- ❌ Any middleware

### 4. Hardware Agnosticism
Verified on:
- ✅ **Oracle Free Tier** (1 vCPU, 1 GB RAM)
- ✅ **GCP e2-micro** (2 vCPU, 4 GB RAM)
- ✅ **Tencent Cloud Lightweight Server** (2 vCPU, 4 GB RAM)

---

## 🧪 Use Cases

| Scenario | Traditional Approach | This Protocol |
|----------|---------------------|---------------|
| Agent crash/restart | Loses all context | Automatically recovers identity |
| Cross-platform migration | Manual memory migration | Anchor on new platform = instant recovery |
| Long-lived session persistence | Bloating context, high cost | Lightweight anchor → fetch on demand |
| Multi-device分身 (multi-device instances) | Requires sync service | Each device independently reads the same anchor |
| AI agent governance | ❌ Identity confusion | ✅ Anchor verification = identity proof |

---

## 📋 Getting Started

### Requirements
- Python 3.8+
- Writable file system
- HTTP outbound access (optional, for remote anchor fetch)

### Quick Start
```bash
git clone https://github.com/ticalzzt/agent-self-recovery.git
cd agent-self-recovery

# Configure anchor
cp MEMORY.md.template MEMORY.md
# Edit MEMORY.md to point bootstrap URL to your identity archive

# Run
python agent.py
```

### Custom Identity
Edit `bootstrap.json`, replacing with your agent info:
```json
{
  "agent": {
    "id": "my-agent-001",
    "name": "My Custom Agent",
    "purpose": "Describe your agent's mission"
  },
  "owner": {
    "name": "Your Name",
    "id": "your-uuid"
  },
  "recovery": {
    "procedure": ["Step 1", "Step 2"]
  }
}
```

---

## 📈 Key Metrics

| Metric | Value |
|--------|-------|
| Anchor size | **<500 characters** (≈350 bytes) |
| Identity archive size | **<2 KB** |
| Boot to full recovery | **<30 seconds** (including API call) |
| Hardware requirement | **Any Linux/Unix system** |
| Network bandwidth | **Negligible** (JSON pull only) |
| Storage requirement | **<100 KB** full deployment |

---

## 🔮 Future Directions

- [ ] Multi-language implementations (Rust / Go / TypeScript)
- [ ] IPFS anchor storage (decentralized)
- [ ] Encrypted anchor content
- [ ] Automatic anchor refresh (detect stale URLs)
- [ ] Cross-platform agent interop protocol

---

## ⚠️ Limitations & Disclaimer

- This protocol provides **memory continuity**, not **real-time data synchronization**
- Falls back to offline anchor cache if external resources are unavailable
- Not suitable for sub-second recovery scenarios
- Contains identity verification fields to prevent adversarial agent identity spoofing

---

## 🤝 Contributing

PRs are welcome! Whether you're improving the protocol, adding language implementations, or fixing bugs.

Please ensure:
1. Anchor files stay <500 characters
2. Identity archives remain self-bootstrapping (self-describing)
3. Tests pass on low-spec hardware (1 vCPU / 1 GB RAM)

---

## 📜 License

MIT License — free to use, attribution requested.

---

<div align="center">
<sub>
AI Agent Self-Recovery Protocol · Proving that even the cheapest cloud VM can be the never-forgetting memory root for AI agents.
<br>
<strong>Minimum spec battle-tested: Oracle Cloud Always Free (1 vCPU, 1 GB RAM, 45 GB Disk) — $0/month</strong>
</sub>
</div>
