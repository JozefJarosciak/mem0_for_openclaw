# Persistent Memory for OpenClaw (Self-hosted Mem0 + Qdrant)

A self-installing Mem0 + Qdrant persistent memory upgrade for [OpenClaw](https://openclaw.ai).

Attach the `.md` file to your OpenClaw chat, hit send, and it walks itself through the entire setup — detecting your OS, paths, and architecture automatically. No manual config hunting required.

---

## The problem with the default setup

The official Mem0 quickstart for OpenClaw works, but the default `memory` vector store is **ephemeral**. Restart your gateway and your memories are gone. SQLite handles audit history, not your vectors.

This guide fixes that with a proper self-hosted stack:

| Layer | What it does |
|---|---|
| **Qdrant** (local) | Durable vector store — persists across restarts |
| **Mem0 OSS** (open-source mode) | Semantic recall and fuzzy search layer |
| **Markdown files** | Source of truth — untouched, canonical, portable |
| **OpenRouter or local Ollama** | LLM + embeddings backend — your choice |

---

## Cloud vs Self-hosted — how they compare

Scored across 15 real criteria (persistence, privacy, cost, debuggability, architecture, operations):

![Cloud vs Self-hosted comparison](https://raw.githubusercontent.com/JozefJarosciak/mem0_for_openclaw/main/comparison.jpg)

| | Cloud (managed) | Self-hosted (this guide) |
|---|---|---|
| **Total score** | 38 / 75 | **66 / 75** |
| **Criteria won** | 2 of 15 | **13 of 15** |
| **Wins** | Setup speed, zero ops | Persistence, privacy, cost, portability, transparency |
| **Weaknesses** | Ephemeral store, cloud lock-in, quota limits | Higher setup complexity, you own maintenance |

---

## Files

| File | Description |
|---|---|
| [OPENCLAW-MEM0-SETUP.md](https://github.com/JozefJarosciak/mem0_for_openclaw/blob/main/OPENCLAW-MEM0-SETUP.md) | The self-installing guide — attach this to OpenClaw and send |
| [OPENCLAW-MEM0-SETUP.pdf](https://github.com/JozefJarosciak/mem0_for_openclaw/blob/main/OPENCLAW-MEM0-SETUP.pdf) | Same guide in PDF — for reading before you run it |

---

## How to use it

1. Download `OPENCLAW-MEM0-SETUP.md`
2. Open your OpenClaw chat (Telegram, WhatsApp, Slack, web — wherever you talk to it)
3. Attach the file and send it
4. OpenClaw will read the guide and begin the installation
5. Whenever it restarts the gateway, type **`continue`** to resume — that's the only input needed during the process

---

## LLM backend options

You choose during setup:

- **Option A — OpenRouter** — works on any machine, small per-call cost, no GPU needed
- **Option B — Local Ollama** — fully offline, free after setup, GPU recommended for best speed

---

## Platform support

Tested on **Linux (5 instances, zero issues)**. The guide uses environment detection and should work on macOS and broadly on other platforms, but has not been tested there. Windows users will need Docker for Qdrant — the guide covers this path.

Use at your own discretion. Best-effort, no guarantees.

---

## Key gotcha to know before you start

During the install, OpenClaw will restart the gateway at least once. When that happens, it will pause and wait. Just type:

```
continue
```

Single word. That's it. It'll resume and finish the rest on its own.

---

## Background

This guide was produced from a real migration on a production OpenClaw instance. Every issue documented — the missing `ollama` npm dependency, the Qdrant version warnings, the 409 conflict noise, the junk memory cleanup — was encountered and resolved in practice.

The full comparison chart and both X posts that accompany this repo are linked in the [original thread]([https://x.com/xenpub/status/2032839708816896375](https://x.com/xenpub/status/2032839708816896375)).

---

## License

MIT — use it, share it, improve it.
