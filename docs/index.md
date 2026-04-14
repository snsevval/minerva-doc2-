<div class="hero-doc" markdown>
<div class="hero-doc__eyebrow" markdown>Documentation</div>

# Minerva

<div class="hero-doc__lead" markdown>
Minerva is a materials-science knowledge graph system that combines extraction, textbook-backed verification, and GraphRAG reasoning in one pipeline. This documentation is organized like a clean product manual: start with setup, walk through the core flow, then inspect the benchmark and system internals.
</div>

<div class="doc-actions" markdown>
[Quick Tutorial](quickstart.md){ .doc-btn .doc-btn--primary }
[Get Started](installation.md){ .doc-btn }
[View Results](evaluation/results.md){ .doc-btn }
</div>
</div>

<div class="terminal-card" markdown>
<div class="terminal-card__bar">
<span class="terminal-dot terminal-dot--warm"></span>
<span class="terminal-dot terminal-dot--hot"></span>
<span class="terminal-dot terminal-dot--dark"></span>
</div>

```text
╭─ Minerva ───────────────────────────────────────────────────────────────╮
│ Verified extraction + TextbookKB + Neo4j GraphRAG                     │
╰─────────────────────────────────────────────────────────────────────────╯

✦ Input: Find materials with superconductivity

Planner   ✓ Create execution path
Retriever ✓ Search paper abstracts + textbook support
Verifier  ✓ Check claims against TextbookKB
Graph     ✓ Store validated relations in Neo4j
Reasoner  ✓ Answer through Cypher + semantic synthesis
```
</div>

<div class="quick-grid" markdown>
<div class="quick-card" markdown>
### Verified Extraction
Entities and relations are extracted from scientific text, then filtered before insertion.
</div>

<div class="quick-card" markdown>
### TextbookKB Support
A FAISS-backed textbook index is used to support or reject extracted claims.
</div>

<div class="quick-card" markdown>
### GraphRAG Querying
Neo4j retrieval and semantic search are combined to answer materials questions.
</div>
</div>

## Walkthrough

Use this documentation in a simple order:

<ol class="walk-list">
<li><strong>Install the stack.</strong> Set up Python, Neo4j, dependencies, and API keys from <a href="installation.md">Get Started</a>.</li>
<li><strong>Run a first query.</strong> Follow the <a href="quickstart.md">Quick Tutorial</a> to see the pipeline end-to-end.</li>
<li><strong>Inspect the system.</strong> Read Architecture, TTD-DR, TextbookKB, and Critic Layer to understand the validation flow.</li>
<li><strong>Check evaluation.</strong> Open Benchmark and Results to see how the system performs on the fill-in-the-blank set.</li>
</ol>

<div class="callout-soft" markdown>
**Project focus**  
Minerva extends the ActiveScience pipeline with verification-first knowledge ingestion. The goal is not only to extract facts, but to reject weak or contradicted claims before they enter the graph.
</div>

## What Minerva Adds

| Layer | Role |
|---|---|
| TTD-DR | Validates extracted claims with textbook evidence before graph insertion |
| TextbookKB | Stores chunked materials-science references in FAISS for retrieval |
| Critic Layer | Applies deterministic checks for type confusion, relation mismatch, and malformed entities |
| GraphRAG | Uses Cypher retrieval plus semantic fallback to answer questions |

## Typical Query Flow

```bash
# Start the API
uvicorn main:app --reload

# Example graph query
curl -X POST http://localhost:8000/graph/ask \
  -H "Content-Type: application/json" \
  -d '{"question":"Which materials have superconductivity?"}'
```

## Next

Head to [Quick Tutorial](quickstart.md) for the product-style walkthrough, or open [Results](evaluation/results.md) if you want the benchmark summary first.
