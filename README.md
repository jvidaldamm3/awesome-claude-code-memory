# Awesome Claude Code Memory [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of projects giving Claude Code persistent memory.

Claude Code writes to append-only JSONL transcript files that get deleted after ~30 days. It has no built-in persistent memory across sessions. These projects fix that — through hooks, MCP servers, vector databases, knowledge graphs, and novel cognitive architectures.

## Contents

- [Deep Memory Systems](#deep-memory-systems)
- [Graph-Based Memory](#graph-based-memory)
- [Advanced & Novel Approaches](#advanced--novel-approaches)
- [Observability & Monitoring](#observability--monitoring)
- [Hook Collections & Frameworks](#hook-collections--frameworks)
- [Key Patterns](#key-patterns)

---

## Deep Memory Systems

Hook-driven projects that give Claude Code persistent memory across sessions.

| Project | Stars | Storage | Retrieval | Description |
|---------|-------|---------|-----------|-------------|
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 33.9k | SQLite + Chroma | Vector | **Description:** Hook-driven memory system using all 6 lifecycle hooks.<br>**Innovation:** 3-layer progressive disclosure (index → timeline → full), ~10x token savings. |
| [zilliztech/memsearch](https://github.com/zilliztech/memsearch) | 814 | Markdown + Milvus | Hybrid RRF | **Description:** By Zilliz (Milvus makers). Markdown-first, Milvus as derived cache.<br>**Innovation:** Hybrid BM25+vector fusion via Reciprocal Rank Fusion. |
| [rlancemartin/claude-diary](https://github.com/rlancemartin/claude-diary) | 335 | Markdown | None | **Description:** Generative Agents-inspired diary system for Claude Code.<br>**Innovation:** PreCompact hook → diary entries → reflection → rules injected into CLAUDE.md. |
| [davegoldblatt/total-recall](https://github.com/davegoldblatt/total-recall) | 186 | Markdown, 4 tiers | None | **Description:** Tiered markdown memory with ~1500 word working memory.<br>**Innovation:** Write-gating: asks "Will this change future behavior?" before promoting. |
| [GMaN1911/claude-cognitive](https://github.com/GMaN1911/claude-cognitive) | 438 | Attention-scored files | Attention decay | **Description:** Most biomimetic memory system with HOT/WARM/COLD tiers.<br>**Innovation:** Files decay 15%/turn, jump to 1.0 on re-mention — mimics human working memory. |
| [obra/episodic-memory](https://github.com/obra/episodic-memory) | 283 | SQLite + sqlite-vec | Vector | **Description:** Fully offline memory using Transformers.js local embeddings.<br>**Innovation:** Session-end hook archives JSONL transcripts into searchable vector store. |
| [hjertefolger/cortex](https://github.com/hjertefolger/cortex) | 167 | SQLite + sqlite-vec | Hybrid (60/40) | **Description:** Hybrid search memory with statusline integration.<br>**Innovation:** 60% vector + 40% BM25 + recency decay with 7-day half-life. |
| [raoulbia-ai/claude-recall](https://github.com/raoulbia-ai/claude-recall) | 5 | SQLite | Pattern matching | **Description:** Correction-focused memory — no vectors, pattern matching only.<br>**Innovation:** Classifies user feedback as corrections via Haiku + regex. |
| [yuvalsuede/memory-mcp](https://github.com/yuvalsuede/memory-mcp) | 85 | JSON + CLAUDE.md | Confidence rank | **Description:** Two-tier memory at ~$0.05/day.<br>**Innovation:** Top ~150 lines ranked by confidence in CLAUDE.md, full store in .memory/state.json. |
| [memvid/claude-brain](https://github.com/memvid/claude-brain) | 318 | Single `.mv2` file | Vector | **Description:** Native Rust, sub-millisecond ops, no DB dependency.<br>**Innovation:** Portable single `.mv2` file you can git commit. |

## Graph-Based Memory

Projects that model memory as entity-relationship graphs.

| Project | Stars | Storage | Retrieval | Description |
|---------|-------|---------|-----------|-------------|
| [amarodeabreu/claude-graph-memory](https://github.com/amarodeabreu/claude-graph-memory) | 1 | Neo4j | Graph traversal | **Description:** 100% local graph memory. Browse at localhost:7474.<br>**Innovation:** MCP tools for store/retrieve/cypher queries over entity graphs. |
| [blas0/Severance](https://github.com/blas0/Severance) | 43 | Custom graph | Graph traversal | **Description:** Cross-session Adaptive Memory (CAM) system.<br>**Innovation:** Auto-builds concept relationship graphs via hooks — no manual tagging. |
| [gannonh/memento-mcp](https://github.com/gannonh/memento-mcp) | 409 | Neo4j 5.13+ | Graph + temporal | **Description:** Graph memory with temporal awareness.<br>**Innovation:** Point-in-time queries, confidence decay, version history on entities. |
| [doobidoo/mcp-memory-service](https://github.com/doobidoo/mcp-memory-service) | 1.5k | SQLite-vec + D3.js | Vector + graph | **Description:** Knowledge graph with D3.js visualization dashboard.<br>**Innovation:** 6 relationship types, autonomous consolidation (decay + compression). |

## Advanced & Novel Approaches

Projects with distinctive architectures or research contributions.

| Project | Stars | Storage | Retrieval | Description |
|---------|-------|---------|-----------|-------------|
| [samvallad33/vestige](https://github.com/samvallad33/vestige) | 413 | SQLite + FTS5 + USearch | Hybrid + FSRS | **Description:** 22MB Rust binary with 29 cognitive modules and 3D visualization dashboard.<br>**Innovation:** FSRS-6 spaced repetition, HyDE query expansion, prediction error gating (only stores surprising info), "memory dreaming" consolidation. |
| [zircote/MIF](https://github.com/zircote/MIF) | 4 | Markdown + JSON-LD | — | **Description:** Open standard for AI memory interchange (format spec, not a memory system).<br>**Innovation:** Dual format (Markdown + JSON-LD) with W3C PROV provenance tracking. Goal: interoperability between memory providers. |
| [zircote/git-notes-memory](https://github.com/zircote/git-notes-memory) | 4 | Git notes + SQLite + sqlite-vec | Hybrid BM25+vector | **Description:** Memories stored as git notes — sync with `git push/pull`.<br>**Innovation:** 10 named namespaces, semantic search via all-MiniLM-L6-v2 embeddings, progressive hydration. |
| [letta-ai/letta-code](https://github.com/letta-ai/letta-code) | 1.8k | Letta server | Agent memory | **Description:** MemGPT-based persistent agent for Claude Code. Model-agnostic.<br>**Innovation:** Single agent that survives across sessions. `/skill` extracts reusable patterns. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 49.3k | Qdrant + Ollama | Vector | **Description:** General-purpose agent memory (+26% over OpenAI Memory on LOCOMO).<br>**Innovation:** OpenMemory MCP: fully local with Qdrant + Ollama, no cloud dependency. |

## Observability & Monitoring

Projects focused on understanding what Claude Code is doing, not storing memories.

| Project | Stars | Storage | Retrieval | Description |
|---------|-------|---------|-----------|-------------|
| [disler/claude-code-hooks-multi-agent-observability](https://github.com/disler/claude-code-hooks-multi-agent-observability) | 1.3k | SQLite | — | **Description:** Real-time swarm monitoring for multi-agent Claude Code setups.<br>**Innovation:** Hooks → Bun server → SQLite → WebSocket → Vue dashboard pipeline. |
| [TechNickAI/claude_telemetry](https://github.com/TechNickAI/claude_telemetry) | 18 | OpenTelemetry | — | **Description:** OpenTelemetry wrapper for Claude Code with <10ms overhead.<br>**Innovation:** Supports Logfire, Sentry, Honeycomb, Datadog out of the box. |
| [nexus-labs-automation/agent-observability](https://github.com/nexus-labs-automation/agent-observability) | 3 | — | — | **Description:** 14 observability skills for Claude Code agents (plugin, not standalone).<br>**Innovation:** Tracing, cost tracking, prompt versioning, guardrails. Integrates with 10 vendors. |

## Hook Collections & Frameworks

Projects focused on Claude Code's hook system (lifecycle events that trigger shell commands).

| Project | Stars | Storage | Retrieval | Description |
|---------|-------|---------|-----------|-------------|
| [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) | 3.3k | — | — | **Description:** Comprehensive educational resource covering all 13 hook lifecycle events.<br>**Innovation:** Security hooks, TTS, sub-agent orchestration patterns. |
| [carlrannaberg/claudekit](https://github.com/carlrannaberg/claudekit) | 627 | Git stashes | Checkpoint restore | **Description:** TypeScript toolkit for Claude Code hooks.<br>**Innovation:** `file-guard`, `thinking-level` (reasoning prompts), `self-review` (auto-critique on file changes), hook profiling. |
| [trailofbits/claude-code-config](https://github.com/trailofbits/claude-code-config) | 1.5k | — | — | **Description:** Security-focused hooks from a professional audit firm.<br>**Innovation:** Hooks as "structured prompt injection at opportune times." |
| [karanb192/claude-code-hooks](https://github.com/karanb192/claude-code-hooks) | 241 | — | — | **Description:** Copy-paste shell scripts for Claude Code hooks.<br>**Innovation:** Block dangerous commands, protect secrets, auto-stage git changes. |
| [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) | 69.8k | JSONL + Markdown | Pattern detection | **Description:** Agent harness for Claude Code. Won Cerebral Valley x Anthropic hackathon (Feb 2026).<br>**Innovation:** "Instincts" — auto-learned debugging skills stored as YAML-frontmatter markdown, promoted across projects. |

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
