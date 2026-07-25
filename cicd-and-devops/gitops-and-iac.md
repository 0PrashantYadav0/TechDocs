# GitOps and Infrastructure as Code

[< Back](./deployment-strategies.md) | [Index](./README.md) | [Next: None >](./README.md)

---

Clicking around the AWS console to provision servers is a recipe for disaster. It's unrepeatable, untrackable, and affectionately known as "ClickOps." We don't do that here.

## Infrastructure as Code (IaC)

IaC means writing code to define your infrastructure. You describe what you want, and a tool provisions it.

- **Declarative vs Imperative**: Declarative (Terraform, Pulumi, Kubernetes YAML) says "I want 3 servers." Imperative (Bash scripts) says "Run this command to create a server, then this one..." Always prefer declarative.
- **Immutable Infrastructure**: Never SSH into a server to update a package. If a server needs an update, destroy it and deploy a new one from a fresh image.

```hcl
# Example Terraform
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "HelloWorld"
  }
}
```

## Environment Parity

Dev, staging, and production should be as identical as possible. The "it works on my machine" excuse usually stems from environmental drift. IaC ensures you stamp out identical environments every time.

## What is GitOps?

GitOps takes IaC a step further. If infrastructure is code, it should be managed like code.

**GitOps Principles:**
1. **Declarative**: The entire system is described declaratively.
2. **Versioned**: The desired state is stored in Git (the single source of truth).
3. **Automated**: Approved changes to Git are automatically applied to the system.
4. **Self-healing**: Software agents ensure correctness and alert on divergence.

## Push vs Pull Model

Traditional CI/CD uses a **Push** model. The pipeline builds the artifact, gets credentials, and pushes the deployment to the cluster.

GitOps typically uses a **Pull** model, popularized by tools like **ArgoCD** or **Flux**.

```mermaid
flowchart LR
    Dev[Developer] -->|Merge| Git[Git Repo<br/>(Desired State)]
    
    subgraph Cluster[Kubernetes Cluster]
        Agent[GitOps Agent<br/>(ArgoCD / Flux)]
        App[Running App<br/>(Actual State)]
    end
    
    Agent -->|Pulls| Git
    Agent -->|Compares & Applies| App
```

Instead of the pipeline pushing into the cluster, an agent inside the cluster constantly watches the Git repository. When the repo changes, the agent pulls the changes and applies them.

- **Security**: The cluster doesn't need to expose ingress for the CI server. The CI server doesn't need cluster admin credentials.
- **Drift Detection**: If someone manually edits a resource in the cluster (a big no-no), the GitOps agent detects the drift and reverts it back to what's in Git.

## Secrets Management

You cannot store plain-text secrets (API keys, DB passwords) in Git. 
GitOps solves this by using solutions like **Sealed Secrets** (encrypting the secret so it's safe to store in Git) or integrating with external vaults (like HashiCorp Vault or AWS Secrets Manager) using tools like External Secrets Operator.

## Takeaways

- Stop clicking in cloud consoles. Use IaC like Terraform or Pulumi.
- Treat servers as cattle, not pets (Immutable Infrastructure).
- Git should be the single source of truth for your entire system state.
- Use a Pull model (GitOps) with tools like ArgoCD for better security and drift detection.
- Never commit plaintext secrets to Git.

---

[< Back](./deployment-strategies.md) | [Index](./README.md) | [Next: None >](./README.md)
