# Networking for Backend Engineers

If you think networking is just for IT ops and you can just build your APIs and ignore it, you're in for a rough awakening. Understanding networking is absolutely non-negotiable for backend engineers. When your service inevitably goes down, or latency spikes mysteriously, or connections are dropped, you can't just throw your hands up and blame "the network." You need to know how packets move, how names resolve, and how traffic is routed and cached. The network is the foundation of everything we build, and ignorance here turns trivial bugs into multi-day outages.

## The Modules

| # | Chapter | Level | What you'll learn |
|---|---------|-------|-------------------|
| 1 | [How the Internet Works](./how-the-internet-works.md) | Basic | The practical 4-layer model, IP addressing, subnets, NAT, HTTP lifecycle, traceroute |
| 2 | [DNS Deep Dive](./dns-deep-dive.md) | Intermediate | Resolution flow, record types, TTL, authoritative vs recursive, load balancing, DNSSEC |
| 3 | [CDNs and the Edge](./cdns-and-edge.md) | Intermediate → Advanced | Caching, anycast routing, edge compute, DDoS protection, BGP basics |
