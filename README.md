# Awesome Claude Code Memory [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of projects giving Claude Code persistent memory.

Claude Code writes to append-only JSONL transcript files that get deleted after ~30 days. It has no built-in persistent memory across sessions. These projects fix that — through hooks, MCP servers, vector databases, knowledge graphs, and novel cognitive architectures.

## Contents

- [Hook Collections & Frameworks](#hook-collections--frameworks)
- [Deep Memory Systems](#deep-memory-systems)
- [Graph-Based Memory](#graph-based-memory)
- [Advanced & Novel Approaches](#advanced--novel-approaches)
- [Observability & Monitoring](#observability--monitoring)
- [General-Purpose Agent Memory](#general-purpose-agent-memory)
- [Key Patterns](#key-patterns)

---

## Hook Collections & Frameworks

Projects focused on Claude Code's hook system (lifecycle events that trigger shell commands).

| Project | Stars | Description |
|---------|-------|-------------|
| [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) | 3k+ | Comprehensive educational resource covering all 13 hook lifecycle events. Security hooks, TTS, sub-agent orchestration. |
| [carlrannaberg/claudekit](https://github.com/carlrannaberg/claudekit) | — | TypeScript toolkit: `file-guard`, `thinking-level` (reasoning prompts), `self-review` (auto-critique on file changes), hook profiling. |
| [trailofbits/claude-code-config](https://github.com/trailofbits/claude-code-config) | — | Security-focused hooks from a professional audit firm. Philosophy: hooks as "structured prompt injection at opportune times." |
| [karanb192/claude-code-hooks](https://github.com/karanb192/claude-code-hooks) | — | Copy-paste shell scripts: block dangerous commands, protect secrets, auto-stage git changes. |
| [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) | — | Agent harness with "Instincts" — auto-learned debugging skills that persist. Won Cerebral Valley x Anthropic hackathon (Feb 2026). |

## Deep Memory Systems

Hook-driven projects that give Claude Code persistent memory across sessions.

| Project | Storage | Key Innovation |
|---------|---------|----------------|
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | SQLite + Chroma | 3-layer progressive disclosure (index → timeline → full), ~10x token savings. All 6 lifecycle hooks. |
| [zilliztech/memsearch](https://github.com/zilliztech/memsearch) | Markdown + Milvus | By Zilliz (Milvus makers). Markdown-first, Milvus as derived cache. Hybrid BM25+vector via RRF. |
| [rlancemartin/claude-diary](https://github.com/rlancemartin/claude-diary) | Markdown | Generative Agents-inspired. PreCompact hook → diary entries → reflection → rules injected into CLAUDE.md. |
| [davegoldblatt/total-recall](https://github.com/davegoldblatt/total-recall) | Markdown, 4 tiers | Write-gated: asks "Will this change future behavior?" before promoting. ~1500 word working memory. |
| [GMaN1911/claude-cognitive](https://github.com/GMaN1911/claude-cognitive) | Attention-scored files | Most biomimetic: files decay 15%/turn, jump to 1.0 on re-mention. HOT/WARM/COLD tiers mimic human working memory. |
| [obra/episodic-memory](https://github.com/obra/episodic-memory) | SQLite + sqlite-vec | Fully offline: Transformers.js local embeddings, session-end hook archives JSONL transcripts. |
| [hjertefolger/cortex](https://github.com/hjertefolger/cortex) | SQLite + sqlite-vec | Hybrid search (60% vector + 40% BM25 + recency decay with 7-day half-life). Statusline integration. |
| [raoulbia-ai/claude-recall](https://github.com/raoulbia-ai/claude-recall) | SQLite | Correction detector classifies user feedback via Haiku + regex. No vectors — pattern matching only. |
| [yuvalsuede/memory-mcp](https://github.com/yuvalsuede/memory-mcp) | JSON + CLAUDE.md | Two-tier: top ~150 lines ranked by confidence in CLAUDE.md, full store in .memory/state.json. ~$0.05/day. |
| [memvid/claude-brain](https://github.com/memvid/claude-brain) | Single `.mv2` file | Native Rust, sub-millisecond ops, no DB. Portable file you can git commit. |

## Graph-Based Memory

Projects that model memory as entity-relationship graphs.

| Project | Backend | Key Feature |
|---------|---------|-------------|
| [amarodeabreu/claude-graph-memory](https://github.com/amarodeabreu/claude-graph-memory) | Neo4j | 100% local. Browse graph at localhost:7474. MCP tools for store/retrieve/cypher. |
| [blas0/Severance](https://github.com/blas0/Severance) | Custom graph | CAM (Cross-session Adaptive Memory) — auto-builds concept relationship graphs via hooks. |
| [gannonh/memento-mcp](https://github.com/gannonh/memento-mcp) | Neo4j 5.13+ | Temporal awareness: point-in-time queries, confidence decay, version history on entities. |
| [doobidoo/mcp-memory-service](https://github.com/doobidoo/mcp-memory-service) | SQLite-vec + D3.js | Knowledge graph dashboard, 6 relationship types, autonomous consolidation (decay + compression). |

## Advanced & Novel Approaches

Projects with distinctive architectures or research contributions.

| Project | What Makes It Unique |
|---------|---------------------|
| [samvallad33/vestige](https://github.com/samvallad33/vestige) | 22MB Rust binary, 29 cognitive modules. FSRS-6 spaced repetition (forgetting curves), HyDE query expansion, prediction error gating (only stores surprising info), "memory dreaming" consolidation. 3D visualization dashboard. |
| [zircote/MIF](https://github.com/zircote/MIF) | Open standard for AI memory interchange. Dual format: Markdown + JSON-LD. W3C PROV provenance tracking. Goal: interoperability between memory providers. |
| [zircote/git-notes-memory](https://github.com/zircote/git-notes-memory) | Memories stored as git notes — sync with `git push/pull`. 10 named namespaces. Hybrid BM25+vector via sqlite-vec. |
| [letta-ai/letta-code](https://github.com/letta-ai/letta-code) | MemGPT-based: single persistent agent that survives across sessions. `/skill` extracts reusable patterns. Model-agnostic. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | General-purpose agent memory (+26% over OpenAI Memory on LOCOMO). OpenMemory MCP: fully local with Qdrant + Ollama. |

## Observability & Monitoring

Projects focused on understanding what Claude Code is doing, not storing memories.

| Project | Description |
|---------|-------------|
| [disler/claude-code-hooks-multi-agent-observability](https://github.com/disler/claude-code-hooks-multi-agent-observability) | Real-time swarm monitoring: hooks → Bun server → SQLite → WebSocket → Vue dashboard. |
| [TechNickAI/claude_telemetry](https://github.com/TechNickAI/claude_telemetry) | OpenTelemetry wrapper. <10ms overhead. Supports Logfire, Sentry, Honeycomb, Datadog. |
| [nexus-labs-automation/agent-observability](https://github.com/nexus-labs-automation/agent-observability) | 14 observability skills: tracing, cost tracking, prompt versioning, guardrails. |

---

## Key Patterns

Recurring design decisions across the landscape:

1. **PreCompact is the memory hook** — fires when context is long, natural moment to capture before compaction shrinks it.

2. **Write-gating** — multiple projects independently converged on "don't save everything, ask if it changes future behavior" (total-recall, claude-diary, vestige's prediction error gating).

3. **Hybrid search dominates** — most vector-backed projects combine keyword + semantic signals, typically via RRF.

4. **Markdown-first** — even vector-backed projects keep markdown as the authoritative source, with the database as a derived index (memsearch, claude-diary, git-notes-memory).

5. **Attention decay** — claude-cognitive's approach (files fade 15%/turn when not referenced) is the most biomimetic, mimicking human working memory.

6. **Local-first** — the trend is toward fully offline systems (local embeddings, local vector DBs) rather than API-dependent memory.

---

## Contributing

Contributions welcome! Please open an issue or PR to:

- Add a project (include: repo link, storage approach, key innovation)
- Update star counts or project status
- Correct any inaccuracies

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is dedicated to the public domain under CC0 1.0.
