<p align="center">
  <img src="../assets/card-engineering.svg" width="70%" alt="Engineering" />
</p>

<a href="../README.md">← back to profile</a>

<img src="../assets/divider.svg" width="100%" alt="" />

# Engineering

Leading a team of five researchers and engineers at Dimtech, building production systems for
financial institutions across trading, treasury, insurance and Islamic finance.

## Production ML & AI

Market-making calibration and execution, retrieval-augmented LLM assistants, and
computer-vision pipelines running under real latency and data-privacy budgets.

| Area | Stack |
|---|---|
| Modelling | PyTorch · TensorFlow · Optuna · scikit-learn |
| Serving | FastAPI · Redis · PostgreSQL · Kafka · WebSocket |
| Orchestration | MLflow · Airflow · n8n · MCP · CrewAI |
| Delivery | Docker · AWS · Azure · GitLab CI |

## Selected builds

- **End-to-End Market Making** — self-hosted high-availability quoting suite (Docker Swarm,
  Pacemaker, Redis Sentinel) for The Group Securities on the Qatar Stock Exchange.
- **Doha Bank treasury RAG** — on-premise LLM pipeline for the treasury middle office with 100%
  data privacy.
- **prospectAI** — computer-vision + LLM drought/incident assessment for the Eurexo-CED Group
  (YOLO and SAM3 distillation).
- **ShariahSentinel / GhostAlpha / beholy / ouihost** — SaaS platforms across Islamic-finance
  screening, portfolio replication, source-grounded RAG research and rental management.

## Self-hosted infrastructure

Nginx and Cloudflare at the edge, PostgreSQL, Redis, Kafka, n8n, Ansible provisioning,
Grafana/Loki/Prometheus monitoring and Portainer-managed containers behind a Tailscale mesh,
with Vault/Authentik/Passbolt for secrets and access.
