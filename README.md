# TechDocs

Hands-on technical deep-dives that pair theory with runnable code and diagrams. Each topic is
its own **module** (a folder) with a `README.md` index and chapter-style docs you read in order
— prev/next links at the top and bottom of every page.

This repo is built as a **learning journey**: it starts from the basics an engineer needs on day
one and climbs all the way to the judgment, architecture, and leadership skills people usually
spend 10+ years accumulating. You can read a single module for a specific topic, or follow the
curated path below from **basic → intermediate → advanced → senior/EM**.

---

## How to read this repo

Every module follows the same shape, so once you learn one, you know them all:

- Open a module's **`README.md`** — it's "chapter 0": the big picture, a contents table, and a
  difficulty tag for each chapter.
- Follow the **Next >** links through the chapters in order.
- Each chapter ends with **takeaways** — the distilled "remember this" list.
- Diagrams use [Mermaid](https://mermaid.js.org/) (renders on GitHub / most Markdown viewers).
  If yours doesn't, paste the ```mermaid block into the [Mermaid Live Editor](https://mermaid.live).

Every chapter is tagged with one of five levels in its module's contents table —
**L1 Beginner**, **L2 Novice**, **L3 Intermediate**, **L4 Advanced**, or **L5 Expert**. Use
the tags to calibrate — it's fine to read an L1 chapter in an otherwise-L4 module and skip
the rest until you're ready.

Missing a topic you'd expect to see? Check [TODO.md](./TODO.md) before assuming it's an
oversight — it's the running list of gaps we already know about.

---

## The learning path (where to start)

```mermaid
flowchart TB
    subgraph L1["1. BASIC - foundations"]
    A["system-design-fundamentals"] --> B["databases (ch 1-3)"]
    B --> C["api-design + testing-and-quality"]
    C --> C2["encryption / quic / smtp<br/>(how the wires work)"]
    C2 --> NET1["networking (how the internet works)"]
    NET1 --> AUTH1["auth (authentication fundamentals)"]
    end
    subgraph L2["2. INTERMEDIATE - building real systems"]
    D["messaging-and-streaming"] --> E["distributed-systems"]
    E --> CC["concurrency"]
    CC --> F["infrastructure"]
    F --> G["realtime / mqtt / security"]
    G --> CON1["containers-and-orchestration<br/>(Docker + K8s core)"]
    CON1 --> CICD1["cicd-and-devops<br/>(pipelines + deployment strategies)"]
    CICD1 --> AUTH2["auth (OAuth2, JWT)"]
    AUTH2 --> NET2["networking (DNS, CDNs)"]
    NET2 --> CLOUD1["cloud-and-serverless<br/>(cloud-native fundamentals)"]
    CLOUD1 --> DJS["distributed-job-schedular"]
    end
    subgraph L3["3. ADVANCED - scale & operate"]
    H["databases (ch 4-5)"] --> I["microservices"]
    I --> J["observability-and-reliability"]
    J --> K["architecture-patterns"]
    K --> AI["ai-ml (AI/ML/DL/GenAI)"]
    AI --> CON2["containers-and-orchestration<br/>(networking, production patterns)"]
    CON2 --> CICD2["cicd-and-devops (GitOps/IaC)"]
    CICD2 --> AUTH3["auth (authorization patterns)"]
    AUTH3 --> CLOUD2["cloud-and-serverless<br/>(serverless + cloud architecture)"]
    CLOUD2 --> DE["data-engineering<br/>(pipelines, warehouses, streaming)"]
    DE --> SE["search-systems<br/>(indexes, ranking, autocomplete)"]
    SE --> PE["performance-engineering<br/>(latency, profiling, load tests)"]
    end
    subgraph L4["4. SENIOR / EM - judgment & people"]
    M["engineering-leadership"]
    end
    L1 --> L2 --> L3 --> L4
    style L1 fill:#e7f3ff,stroke:#004085
    style L2 fill:#fff3e0,stroke:#e65100
    style L3 fill:#d4edda,stroke:#28a745
    style L4 fill:#f3e7ff,stroke:#6f42c1
```

### Stage 1 — Basic (you're new, or shoring up fundamentals)
Start here regardless of experience — these are the mental models everything else builds on.

1. **[system-design-fundamentals/](./system-design-fundamentals/README.md)** — the vocabulary:
   scalability, latency, availability, CAP, estimation, and the design framework. **Read this
   first.**
2. **[databases/](./databases/README.md)** chapters 1-3 — SQL vs NoSQL, indexing, transactions.
   The bottleneck of most systems.
3. **[api-design/](./api-design/README.md)** — REST/gRPC/GraphQL, good API design, versioning.
   The contracts everything talks through.
4. **[testing-and-quality/](./testing-and-quality/README.md)** — the testing pyramid, TDD,
   coverage. How to change code without fear.
5. The networking basics — **[quic/](./quic/README.md)** (TCP/UDP, TLS, HTTP),
   **[encryption/](./encryption/README.md)**, **[smtp/](./smtp/README.md)** — how the wires
   actually work.
6. **[networking/](./networking/README.md)** ch 1 — how the internet actually works: IP, routing,
   NAT, the life of an HTTP request.
7. **[auth/](./auth/README.md)** ch 1 — authentication fundamentals: passwords, hashing,
   sessions vs tokens.

### Stage 2 — Intermediate (you build features; now build systems)
1. **[messaging-and-streaming/](./messaging-and-streaming/README.md)** — sync vs async, queues
   vs streams, delivery guarantees.
2. **[distributed-systems/](./distributed-systems/README.md)** — the fallacies, consensus,
   idempotency, and the failure-handling toolkit you'll use in every service.
3. **[concurrency/](./concurrency/README.md)** — threads vs async vs processes, race conditions,
   locks, and how to avoid the whole minefield.
4. **[infrastructure/](./infrastructure/README.md)** — load balancers, gateways, rate limiting,
   caching & Redis.
5. Protocol deep-dives as needed — **[realtime/](./realtime/README.md)** (WebSocket/WebRTC),
   **[mqtt/](./mqtt/README.md)**, **[security/](./security/README.md)**.
6. **[containers-and-orchestration/](./containers-and-orchestration/README.md)** ch 1-2 — Docker
   fundamentals and Kubernetes core objects.
7. **[cicd-and-devops/](./cicd-and-devops/README.md)** ch 1-2 — CI/CD pipelines and deployment
   strategies (blue/green, canary, rolling).
8. **[auth/](./auth/README.md)** ch 2-3 — OAuth 2.0, OIDC, JWT deep-dive.
9. **[networking/](./networking/README.md)** ch 2-3 — DNS deep-dive, CDNs & edge computing.
10. **[cloud-and-serverless/](./cloud-and-serverless/README.md)** ch 1 — cloud-native
    fundamentals, 12-factor app.
11. **[distributed-job-schedular/](./distributed-job-schedular/README.md)** — leader election,
    heartbeats, job deduplication, priority queues, and Postgres-backed scheduler.

### Stage 3 — Advanced (you scale and operate systems)
1. **[databases/](./databases/README.md)** chapters 4-5 — replication, sharding, data modeling.
2. **[microservices/](./microservices/README.md)** — when (and when *not*) to split, boundaries,
   sagas & the outbox pattern.
3. **[observability-and-reliability/](./observability-and-reliability/README.md)** — metrics/
   logs/traces, SLOs & error budgets, incidents & postmortems.
4. **[architecture-patterns/](./architecture-patterns/README.md)** — clean architecture, ADRs,
   security by design, deployment & cost.
5. **[ai-ml/](./ai-ml/README.md)** — AI vs ML vs DL vs GenAI, machine learning, deep learning,
   transformers & LLMs, RAG/agents, and MLOps. The fast-moving field every engineer now needs.
6. **[containers-and-orchestration/](./containers-and-orchestration/README.md)** ch 3-4 — K8s
   networking, storage, and production patterns (probes, HPA, Helm, service mesh).
7. **[cicd-and-devops/](./cicd-and-devops/README.md)** ch 3 — GitOps, Infrastructure as Code,
   immutable infrastructure.
8. **[auth/](./auth/README.md)** ch 4 — authorization patterns (RBAC, ABAC, ReBAC, zero trust).
9. **[cloud-and-serverless/](./cloud-and-serverless/README.md)** ch 2-3 — serverless patterns,
   multi-region, disaster recovery, cloud cost optimization.
10. **[data-engineering/](./data-engineering/README.md)** — data pipelines, warehouses &
    lakehouses, streaming at scale. The data platform every system eventually needs.
11. **[search-systems/](./search-systems/README.md)** — inverted indexes, Elasticsearch/
    OpenSearch, ranking, and autocomplete. Product search beyond `LIKE '%query%'`.
12. **[performance-engineering/](./performance-engineering/README.md)** — latency budgets,
    profiling & flame graphs, load testing and capacity planning.

### Stage 4 — Senior / Staff / Engineering Manager (judgment & people)
1. **[engineering-leadership/](./engineering-leadership/README.md)** — the career ladder,
   leading without authority, the EM transition, and the collected 10+-year wisdom. Pairs with
   the "trade-offs" and "wisdom" capstone chapters throughout the repo.

---

## All modules

### Core curriculum (career progression)

| Module | Level | What it covers |
|--------|-------|----------------|
| [system-design-fundamentals/](./system-design-fundamentals/README.md) | Basic → Advanced | Scalability, latency, availability, CAP/PACELC, estimation, scaling, the design framework, trade-offs |
| [databases/](./databases/README.md) | Basic → Advanced | SQL vs NoSQL, indexing, transactions/ACID, replication & sharding, data modeling |
| [api-design/](./api-design/README.md) | Basic → Advanced | REST/gRPC/GraphQL, good REST design, versioning, pagination & evolution |
| [testing-and-quality/](./testing-and-quality/README.md) | Basic → Advanced | The testing pyramid, kinds of tests, TDD, coverage, quality gates & reviews |
| [concurrency/](./concurrency/README.md) | Intermediate → Advanced | Concurrency vs parallelism, threads/async/processes, race conditions, locks, safe patterns |
| [distributed-systems/](./distributed-systems/README.md) | Intermediate → Advanced | The fallacies, consensus (Raft/quorums), time & idempotency, failure handling |
| [distributed-job-schedular/](./distributed-job-schedular/README.md) | Intermediate → Advanced | Leader election, heartbeats, job deduplication, priority queues, Postgres scheduler |
| [messaging-and-streaming/](./messaging-and-streaming/README.md) | Basic → Advanced | Sync vs async, queues vs streams (Kafka/RabbitMQ), delivery guarantees, DLQs |
| [microservices/](./microservices/README.md) | Intermediate → Advanced | Monolith vs microservices, boundaries & communication, sagas & outbox |
| [observability-and-reliability/](./observability-and-reliability/README.md) | Intermediate → Advanced | Metrics/logs/traces, SLIs/SLOs/error budgets, incidents & postmortems |
| [architecture-patterns/](./architecture-patterns/README.md) | Intermediate → Advanced | Clean/hexagonal architecture, ADRs, security by design, deployment & cost |
| [ai-ml/](./ai-ml/README.md) | Basic → Advanced | AI vs ML vs DL vs GenAI, machine learning, deep learning, transformers & LLMs, RAG/agents, MLOps |
| [containers-and-orchestration/](./containers-and-orchestration/README.md) | Basic → Advanced | Docker, Kubernetes core, K8s networking & storage, production patterns, service mesh |
| [cicd-and-devops/](./cicd-and-devops/README.md) | Basic → Advanced | CI/CD pipelines, deployment strategies (blue/green, canary), GitOps & Infrastructure as Code |
| [auth/](./auth/README.md) | Basic → Advanced | Authentication, OAuth 2.0/OIDC, JWT, authorization patterns (RBAC/ABAC/ReBAC), zero trust |
| [cloud-and-serverless/](./cloud-and-serverless/README.md) | Basic → Advanced | Cloud-native, 12-factor app, serverless patterns, multi-region, DR, cost optimization |
| [data-engineering/](./data-engineering/README.md) | Basic → Advanced | Data pipelines (ETL/ELT), warehouses & lakehouses, streaming at scale, CDC |
| [search-systems/](./search-systems/README.md) | Basic → Advanced | Inverted indexes, Elasticsearch/OpenSearch, BM25 ranking, autocomplete & facets |
| [performance-engineering/](./performance-engineering/README.md) | Basic → Advanced | Latency budgets & percentiles, profiling/flame graphs, load testing & capacity |
| [engineering-leadership/](./engineering-leadership/README.md) | Senior → EM | Career ladder, technical leadership, the EM transition, career-long wisdom |

### Deep-dive references (networking, protocols, crypto)

| Module | What it covers |
|--------|----------------|
| [networking/](./networking/README.md) | How the internet works (IP, routing, NAT), DNS deep-dive, CDNs & edge computing, BGP |
| [encryption/](./encryption/README.md) | Symmetric/asymmetric encryption, keys, hybrid, digital signatures, real algorithms (AES, RSA, ECC, DH) |
| [quic/](./quic/README.md) | The networking stack: TCP vs UDP, TLS 1.2/1.3, HTTP/1-2-3, and QUIC |
| [mqtt/](./mqtt/README.md) | MQTT pub/sub protocol (topics, QoS, sessions, LWT) and how to use it effectively |
| [realtime/](./realtime/README.md) | WebSocket, WebRTC, WS-vs-WebRTC, and STUN/TURN/ICE NAT traversal |
| [security/](./security/README.md) | TOR (onion routing), forward secrecy, and firewalls |
| [smtp/](./smtp/README.md) | SMTP email delivery, SPF/DKIM/DMARC, and SMTP vs IMAP/POP3 |
| [infrastructure/](./infrastructure/README.md) | L4 load balancers, bastion vs LB vs gateway, rate limiting, API gateway, caching & Redis cluster |

---

## Repo layout

```
TechDocs/
├── README.md                        <- you are here (repo index + learning path)
│
│   # Core curriculum (basic -> senior -> EM)
├── system-design-fundamentals/      <- START HERE: the mental models
├── databases/                       <- SQL/NoSQL, indexing, transactions, sharding, modeling
├── api-design/                      <- REST/gRPC/GraphQL, good design, versioning
├── testing-and-quality/             <- testing pyramid, TDD, coverage, quality gates
├── concurrency/                     <- threads/async/processes, races, locks, safe patterns
├── distributed-systems/             <- fallacies, consensus, idempotency, failure handling
├── distributed-job-schedular/       <- leader election, heartbeats, deduplication, priority queues
├── messaging-and-streaming/         <- async, queues vs streams, delivery guarantees
├── microservices/                   <- monolith vs micro, boundaries, sagas
├── observability-and-reliability/   <- metrics/logs/traces, SLOs, incidents
├── architecture-patterns/           <- clean architecture, ADRs, security, deployment, cost
├── ai-ml/                           <- AI/ML/DL/GenAI, transformers, RAG, MLOps
├── containers-and-orchestration/    <- Docker, Kubernetes, service mesh, production patterns
├── cicd-and-devops/                 <- CI/CD pipelines, deployment strategies, GitOps, IaC
├── auth/                            <- authentication, OAuth2/OIDC, JWT, authorization patterns
├── cloud-and-serverless/            <- cloud-native, serverless, multi-region, cost optimization
├── data-engineering/                <- data pipelines, warehouses, lakehouses, streaming at scale
├── search-systems/                  <- inverted indexes, Elasticsearch, ranking, autocomplete
├── performance-engineering/         <- latency budgets, profiling, load testing, capacity
├── engineering-leadership/          <- career ladder, tech leadership, EM, wisdom
│
│   # Deep-dive references
├── networking/                      <- how the internet works, DNS, CDNs, edge computing
├── encryption/                      <- how encryption works
├── quic/                            <- transport & HTTP evolution
├── mqtt/                            <- IoT pub/sub messaging
├── realtime/                        <- WebSocket, WebRTC, STUN/TURN/ICE
├── security/                        <- TOR, forward secrecy, firewalls
├── smtp/                            <- email delivery
└── infrastructure/                  <- LBs, gateways, bastions, rate limits, caching
```

---

## Not sure where to start?

- **"I'm early-career / a student"** → read
  [system-design-fundamentals](./system-design-fundamentals/README.md) cover to cover, then
  [databases](./databases/README.md) ch 1-3. That's the foundation the whole industry stands on.
- **"I have a system design interview"** → fundamentals (all), plus the design framework and
  trade-offs chapters, then skim databases, distributed-systems, and microservices.
- **"I'm becoming a senior / tech lead"** → distributed-systems, microservices,
  observability-and-reliability, and architecture-patterns — then
  [engineering-leadership](./engineering-leadership/README.md).
- **"I'm moving into management"** → jump to
  [engineering-leadership](./engineering-leadership/README.md), especially the EM-transition and
  wisdom chapters.
- **"I want to understand AI / build with LLMs"** → read [ai-ml](./ai-ml/README.md) start to
  finish — it goes from "what is AI?" through ML/DL to transformers, RAG, agents, and MLOps.

> The fastest way to grow: read a module, then **build something small that uses it.** Theory
> sticks when it survives contact with a keyboard.

---

## Running the code

Examples are mostly Python. Install any needed library with `uv` against the Walmart index:

```bash
uv pip install <package> \
  --index-url https://pypi.ci.artifacts.walmart.com/artifactory/api/pypi/external-pypi/simple \
  --allow-insecure-host pypi.ci.artifacts.walmart.com
```

## Diagrams

Docs use [Mermaid](https://mermaid.js.org/) diagrams — they render on GitHub and in most
Markdown viewers. If yours doesn't, paste the fenced ```mermaid block into the
[Mermaid Live Editor](https://mermaid.live).
