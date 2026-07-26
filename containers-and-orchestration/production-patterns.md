# Production Patterns

[< Back](./networking-and-storage.md) | [Index](./README.md) | [Next: Index >](./README.md)

---

Getting an app running in Kubernetes is the easy part. Keeping it highly available, secure, and resource-efficient in production requires applying established patterns.

## Health Probes

Kubernetes needs to know if your app is actually working, not just if the process is running.

- **Liveness Probe**: "Are you alive?" If it fails, K8s restarts the Pod. Fixes deadlocks.
- **Readiness Probe**: "Can you take traffic?" If it fails, K8s removes the Pod from Service endpoints. Use this when your app is booting or overloaded.
- **Startup Probe**: For legacy apps that take a very long time to start. Disables liveness/readiness checks until it succeeds.

```yaml
readinessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
```

## Resource Requests and Limits

Never deploy without defining resources. This prevents noisy neighbors from crashing nodes.

- **Requests**: What the Pod *needs*. The Scheduler uses this to find a Node with enough capacity.
- **Limits**: The hard cap. If a container exceeds its memory limit, it gets OOMKilled. If it exceeds CPU, it gets throttled (slower, but not killed).

> **Rule of thumb**: Set CPU requests, but leave limits off or high to allow bursting. Set Memory requests and limits to the same value to prevent unexpected OOMKills.

## Scaling and Updates

- **HPA (Horizontal Pod Autoscaler)**: Automatically increases/decreases the number of Pod replicas based on CPU, Memory, or custom metrics (like queue length).
- **VPA (Vertical Pod Autoscaler)**: Automatically adjusts the requests/limits of your containers based on historical usage.
- **Rolling Updates**: Deployments update Pods incrementally. You define `maxSurge` (how many extra pods to create) and `maxUnavailable` (how many can be down).
- **Pod Disruption Budgets (PDB)**: Prevents voluntary disruptions (like node upgrades) from taking down too many replicas of your app at once.

## The Broader Ecosystem

To manage complexity, the ecosystem has evolved patterns:

- **Helm**: The package manager for K8s. It templates your YAML files so you can install complex apps like Redis or Prometheus with a single `helm install` command.
- **Operators**: Software extensions that manage complex stateful applications. An Operator knows how to backup, upgrade, or heal a specific database (e.g., the Postgres Operator) natively inside K8s.
- **Service Mesh (Istio / Linkerd)**: A sidecar proxy added to every Pod to handle mTLS encryption, advanced traffic routing (canary deployments), and deep observability without changing application code.

## Security & Multi-tenancy

- **RBAC (Role-Based Access Control)**: Restrict what users and service accounts can do (e.g., "Developer can only read Pods in the `frontend` namespace").
- **Pod Security Standards**: Enforce rules at the cluster level (e.g., "No container can run as root").

## Takeaways
- Use **Probes** so K8s knows when to restart Pods or pull them from rotation.
- Always set **Resource Requests and Limits** to help the Scheduler and prevent node crashes.
- Automate scaling with **HPA** and protect availability during maintenance with **PDBs**.
- Use **Helm** for packaging and **Operators** for automating stateful application management.

---

[< Back](./networking-and-storage.md) | [Index](./README.md) | [Next: Index >](./README.md)
