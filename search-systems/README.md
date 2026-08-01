# Search Systems

SQL `LIKE '%query%'` works until it doesn't. The moment you need ranked relevance, typo
tolerance, autocomplete, or searching across millions of documents, you need a real search
system. This module covers how full-text search actually works — from inverted indexes to
Elasticsearch/OpenSearch, ranking, and the autocomplete patterns every product eventually needs.

## Contents

| # | Chapter | Level | What you'll learn |
|---|---------|-------|-------------------|
| 1 | [Search Fundamentals](./search-fundamentals.md) | Basic → Intermediate | Why SQL fails, inverted indexes, tokenization, analyzers |
| 2 | [Search Engines in Practice](./search-engines.md) | Intermediate | Elasticsearch/OpenSearch, sharding, indexing pipeline, queries |
| 3 | [Ranking, Relevance & Autocomplete](./ranking-and-autocomplete.md) | Advanced | BM25, boosting, fuzzy match, typeahead, faceted search |

## How to read this module

- **Chapter 1** is the mental model: what an inverted index is and why it beats scanning rows.
- **Chapter 2** is the production tool: how Elasticsearch (and friends) actually store and query.
- **Chapter 3** is the product craft: making results *feel* right and building autocomplete.

```mermaid
flowchart LR
    Why["Why search?<br/>(SQL isn't enough)"] --> Engine["Search engine<br/>(index + query)"]
    Engine --> Rank["Relevance & UX<br/>(rank, autocomplete)"]
    style Why fill:#e7f3ff,stroke:#004085
    style Engine fill:#fff3e0,stroke:#e65100
    style Rank fill:#d4edda,stroke:#28a745
```

## Related modules

Builds on [databases](../databases/README.md) (indexing, data modeling) and
[infrastructure/caching](../infrastructure/caching-redis.md). Pairs with
[data-engineering](../data-engineering/README.md) when search indexes are fed by pipelines/CDC.

## The one truth

> **Search is not filtering — it's ranking.** Returning every document that matches is easy.
> Returning the *right* ten documents, in the right order, under 50ms, for every query, is the
> hard part.

Start with [search-fundamentals.md](./search-fundamentals.md). **Next >**
