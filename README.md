# Kapeka-AI

**Middleware that makes LLMs faster and cheaper.**

Kapeka-AI is a persistent memory and reasoning layer that attaches to any large language model. Instead of re-feeding entire context windows on every call, Kapeka retrieves only the relevant knowledge chains — cutting search space, latency, and token cost by orders of magnitude.

> ⚡ **3,136× faster routing than linear search** at 100k items
> 🧠 **88ms** to retrieve 25 knowledge chains from **1,000,000 tokens**
> 🗜️ **99.6%** search-space reduction (1M tokens → 3,861 synthesis nodes)

---

## The Problem

Every LLM call today pays the same tax: context has to be stuffed into the prompt, tokenized, and attended over from scratch. As knowledge bases grow, this gets slower and more expensive linearly — or worse. Retrieval-augmented approaches help, but most treat memory as a flat vector store with no structure, no reasoning, and no persistence of *insight*.

## The Approach

Kapeka-AI models memory as a typed, decaying knowledge graph with a dedicated routing algorithm on top:

- **ARIA routing algorithm** — sub-linear traversal that reaches relevant nodes without scanning the full store. Benchmarked at 3,136× faster than linear search at 100k items.
- **4D vector scoring (Vec4)** — every node is scored across four independent dimensions: frequency, accuracy, connectivity, and inference weight. Retrieval balances all four rather than relying on similarity alone.
- **Typed semantic relationships** — 10 distinct edge types (not just "related to"), enabling a formal logic engine to reason over the graph with defined inference rules.
- **Synthesis nodes** — a persistent insight layer that doesn't decay. Discovered patterns are promoted into durable knowledge instead of being recomputed every session.
- **MCP server architecture** — Kapeka attaches to LLMs through the Model Context Protocol, making it a drop-in memory layer for any compatible model.

## Benchmarks

| Metric | Result | Condition |
|---|---|---|
| Routing speed | **3,136× faster** than linear search | 100,000 items |
| Retrieval latency | **88ms** for 25 knowledge chains | 1,000,000-token corpus |
| Compression | **99.6%** search-space reduction | 1M tokens → 3,861 synthesis nodes |

*Benchmarks are from internal v5.0 planning builds. Methodology and reproduction details available on request.*

## Applied Result: DNA Decay Finder

To validate the graph-decay mechanics on real data, Kapeka's decay model was applied to cancer genomics. The **DNA decay finder** detects mutation hotspots and was validated against the public **TCGA** cancer genomics dataset — demonstrating that the same routing and decay machinery that accelerates LLM memory generalizes to structured scientific data.

## Architecture at a Glance

```
        ┌─────────────┐
  LLM ──│ MCP Server  │── attachment point
        └──────┬──────┘
               │
        ┌──────▼───────────────────────────┐
        │  ARIA Routing  (sub-linear)       │
        ├──────────────────────────────────┤
        │  Typed Knowledge Graph            │
        │   • Vec4-scored nodes             │
        │   • 10 typed relationship edges   │
        │   • Logic engine (formal rules)   │
        ├──────────────────────────────────┤
        │  Synthesis Layer  (no decay)      │
        └──────────────────────────────────┘
               │
        ┌──────▼──────┐
        │  Postgres   │  route persistence
        └─────────────┘
```

- **Multi-tenant** with zero-knowledge encryption
- **Route persistence** on Supabase / PostgreSQL
- **Consumer UI** with a dark neural aesthetic and real-time 3D knowledge-graph visualization (Fibonacci-sphere layout, force-directed)

## Status

Kapeka-AI is in active development at **v4.7**, progressing toward **v5.0**. Core components — ARIA routing, Vec4 scoring, the typed edge store, the logic engine, and the validated DNA decay finder — are working and benchmarked.

## About

Built by **Matthew McBerry**, founder & CEO of **Dorcas Innovations**.

The full engine is under active development and kept private as core IP. This repository is a public overview — for a live demo, benchmark reproduction, or partnership inquiries, reach out.

📧 MatthewMcBerry@DorcasInnovations.onmicrosoft.com

---

*Kapeka-AI — persistent memory and reasoning for any LLM.*
