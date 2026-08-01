# Ranking, Relevance & Autocomplete

[< Back](./search-engines.md) | [Index](./README.md) | [Next: None >](./README.md)

---

Matching documents is table stakes. Users judge search by whether the *first* result is what they
meant. Ranking, boosting, fuzzy matching, and autocomplete are how search becomes a product
feature instead of a database feature.

## BM25: The Default Ranking Function

Modern Lucene-based engines score with **BM25**. Intuition:

- Rare terms that match count more than common terms (IDF — inverse document frequency)
- More occurrences in a doc help, with diminishing returns (TF saturation)
- Short documents matching the query tend to rank higher than long ones that mention the term once (length normalization)

You rarely reimplement BM25. You **steer** it with field boosts, functions, and re-ranking.

## Steering Relevance

| Technique | What it does | Example |
|-----------|--------------|---------|
| **Field boosts** | Weight some fields higher | `title^3`, `description^1` |
| **Function score** | Multiply/add business signals | Boost in-stock, high-rated, recent |
| **Synonyms** | Expand query vocabulary | `sneakers` ↔ `trainers` |
| **Phrase / proximity** | Prefer terms near each other | `"running shoes"~2` |
| **Negative boosts** | Demote junk | Downrank discontinued SKUs |

```mermaid
flowchart LR
    Q[Query] --> BM25[BM25 text score]
    BM25 --> Biz[Business signals<br/>stock, rating, margin]
    Biz --> TopK[Top-K results]
    TopK --> Rerank[Optional re-ranker<br/>ML / LTR]
    Rerank --> Page[Results page]
```

**Learning to Rank (LTR)** uses ML models on features (clicks, dwell time, text score) for a
second-pass re-rank. Worth it only after you've exhausted analyzers and boosts — and have click
data that isn't garbage.

## Fuzzy Matching and Typos

Users misspell. Engines handle this with:
- **Edit distance (Levenshtein)** — `runing` ≈ `running`
- **N-grams / edge n-grams** — index character slices for partial matches
- **Phonetic filters** — Soundex/Metaphone for names (`Smith` ≈ `Smyth`)

Fuzzy queries are expensive. Prefer:
1. Correct analyzers and synonyms first
2. Suggest "Did you mean?" from a popular-query dictionary
3. Fuzzy only on short queries or as a fallback when exact match returns nothing

## Autocomplete / Typeahead

Autocomplete is a **different index shape**, not just "search but truncated."

| Approach | How | Best for |
|----------|-----|----------|
| **Edge n-grams** | Index `run`, `runn`, `runni`… on fields | Prefix match as you type |
| **Completion suggester** | FST (finite state transducer) optimized for prefix | Fast brand/SKU/title suggest |
| **Search-as-you-type** field type | ES built-in n-gram variants | Quick product setups |
| **Dedicated suggest index** | Popular queries + product titles, aggressively trimmed | Large catalogs with query analytics |

Design rules:
- Debounce on the client (150–300ms)
- Limit payload (5–10 suggestions)
- Prefer **popular queries** and **categories** over dumping raw catalog noise
- Separate "query suggest" from "product suggest" in the UX

## Faceted Search and Filters

Facets (aggregations) let users narrow: brand, size, price buckets, color.

- Compute facets on the **filtered** set, not the whole index
- High-cardinality fields (user IDs) make terrible facets
- Cache common filter combinations when traffic is hot

## Measuring Whether Search Is Good

| Signal | What it tells you |
|--------|-------------------|
| **Zero-result rate** | Analyzer/synonym gaps, bad queries |
| **Click-through on position 1–3** | Ranking quality |
| **Reformulation rate** | Users retrying = relevance miss |
| **Latency p95/p99** | Shard fan-out, script scores, giant aggregations |

Log queries (carefully — PII!), sample failures weekly, and treat relevance tuning as an ongoing
product loop — not a one-time mapping change.

## Takeaways

- **BM25** ranks by term rarity, frequency, and doc length; you steer it with boosts and signals.
- Put business logic (stock, quality, freshness) into scoring or you will ship "technically correct" junk.
- **Autocomplete** needs its own indexing strategy (edge n-grams / completion), not naive prefix SQL.
- Measure zero-results, clicks, and reformulations — relevance without metrics is vibes.

---

[< Back](./search-engines.md) | [Index](./README.md) | [Next: None >](./README.md)
