# TODO — Missing Topics

This repo covers a lot, but a full audit against the 5-level learning path
(see [README.md](./README.md#the-5-level-learning-path)) turned up real gaps —
some in existing modules, some big enough to be their own module. Tracked here so
the backlog doesn't just live in someone's head.

Levels use the same scale as the rest of the repo: **L1 Beginner → L2 Novice →
L3 Intermediate → L4 Advanced → L5 Expert**.

---

## L1 · Beginner

- [ ] **Git & version control fundamentals** — branching models, merge vs. rebase,
  resolving conflicts, writing a good PR. Assumed knowledge everywhere else, taught
  nowhere.
- [ ] **Command line & Linux basics for engineers** — the shell, processes, permissions,
  piping/redirection, reading logs on a box you don't own.
- [ ] **Data structures & algorithms primer** — arrays, hash maps, trees, Big-O — the
  vocabulary `indexing.md` and `search-fundamentals.md` already assume the reader has.
- [ ] **HTTP fundamentals, standalone** — methods, status codes, headers, statelessness,
  cookies. Currently only implied inside `networking/how-the-internet-works.md`.
- [ ] **Basic logging & debugging practices** — log levels, what to log, reading a
  stack trace — precedes `observability-and-reliability` by a full stage.

## L2 · Novice

- [ ] **Docker Compose & local dev environments** — `containers-and-orchestration`
  jumps from Dockerfiles straight to Kubernetes; multi-container local dev is missing.
- [ ] **Dependency & package management** — semantic versioning, lockfiles, supply-chain
  basics (this predates `cicd-and-devops` pipelines that assume it).
- [ ] **Config & secrets basics** — env vars, `.env` files, config layering per
  environment — the on-ramp to the advanced secrets-management topic below.
- [ ] **General caching strategies** — cache-aside, write-through, TTLs, invalidation —
  `infrastructure/caching-redis.md` covers Redis specifics but not the underlying theory.
- [ ] **Input validation & the OWASP Top 10** — injection, XSS, SSRF at a beginner level;
  `architecture-patterns/security-by-design.md` assumes this and builds on top.
- [ ] **Structured logging & correlation IDs** — the practical companion to
  `observability-and-reliability/three-pillars.md`.

## L3 · Intermediate

- [ ] **gRPC, standalone deep-dive** — protobuf schemas, streaming modes, deadlines,
  interceptors. `api-design/api-styles.md` only compares it at a glance.
- [ ] **GraphQL, standalone deep-dive** — schema design, resolvers, the N+1 problem,
  federation. Same gap as gRPC.
- [ ] **Message brokers in depth** — RabbitMQ exchanges/bindings, SQS/SNS fan-out —
  `messaging-and-streaming` covers concepts but no broker gets a real walkthrough.
- [ ] **Infrastructure as Code, hands-on** — Terraform/Pulumi modules, state files,
  drift detection. `cicd-and-devops/gitops-and-iac.md` covers the *philosophy*, not
  the tool.
- [ ] **Secrets management** — Vault/KMS, rotation, least-privilege access patterns.
- [ ] **Feature flags & progressive delivery, deep-dive** — `deployment-strategies.md`
  mentions flags in passing; kill switches, targeting rules, and cleanup deserve a
  full chapter.
- [ ] **Reverse proxies in depth** — Nginx/Envoy config, not just the load-balancer
  concepts already in `infrastructure/`.
- [ ] **Background jobs on a single node** — a Sidekiq/Celery-style primer that comes
  *before* `distributed-job-schedular`, which already assumes distributed scale.
- [ ] **Distributed tracing, hands-on** — OpenTelemetry instrumentation, not just the
  concept mentioned in `observability-and-reliability/three-pillars.md`.

---

*More gaps (L4, L5, and whole missing modules) still being audited — see history for
updates.*
