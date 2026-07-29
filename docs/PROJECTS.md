<p align="center">
  <img src="../assets/card-projects.svg" width="70%" alt="Projects" />
</p>

<a href="../README.md">← back to profile</a>

<img src="../assets/divider.svg" width="100%" alt="" />

# Projects

Selected work, grouped by sector. Client names are withheld. Each section below is collapsible,
click a sector to expand it. Every project carries a deployment tag
(![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624)
![cloud](https://img.shields.io/badge/cloud-30363D?style=flat-square&logo=microsoftazure&logoColor=2088D4))
and is described as Problem, Solution, Architecture and Contribution.

<img src="../assets/divider.svg" width="100%" alt="" />

<details>
<summary><b>Securities</b> &nbsp;·&nbsp; market-making platform</summary>

<br/>

#### Market-making platform &nbsp; ![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624)

Automated market making / designated liquidity provision on an emerging equity exchange.

- **Problem:** meet exchange liquidity-provider obligations (max spread, minimum size, presence time) throughout the session without accumulating unhedgeable inventory, at low latency.
- **Solution:** a GLFT / Stoikov microprice quoting engine (tick-volatility and liquidity estimators, inventory skew, intraday regime schedules, end-of-day flattening); Bayesian walk-forward calibration with Optuna, tracked in MLflow.
- **Architecture:** a React / TypeScript operator dashboard over a FastAPI backend, with a Redis pub/sub control plane coordinating one engine per symbol and an exchange-gateway connector over STOMP/TLS, fronted by HAProxy with a JWT auth API. The whole stack runs on Docker Swarm on-premise, with high availability via HAProxy, Redis Sentinel and Patroni-managed PostgreSQL.
- **Contribution:** built the full stack, from the calibration research system (backtester, walk-forward, experiment tracking) to the operator platform (multi-symbol engine, gateway, analytics, audit).

`Python · FastAPI · Optuna · MLflow · Redis Sentinel · PostgreSQL / Patroni · MinIO · Vault · HAProxy · Docker Swarm · React`

</details>

<details>
<summary><b>Asset Management</b> &nbsp;·&nbsp; portfolio intelligence & agentic-AI assistant</summary>

<br/>

#### Portfolio intelligence & agentic-AI assistant &nbsp; ![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624)

Decision-support platform for discretionary equity portfolio managers moving off spreadsheets.

- **Problem:** no centralised monitoring, quantitative risk analytics or alerting; a manual, reactive workflow.
- **Solution:** a quantitative risk engine (VaR / CVaR by historical, parametric and Monte-Carlo methods, drawdown, correlation, efficient frontier, attribution, stress) and an enhanced-indexing optimiser (SLSQP under tracking-error and sector / cardinality constraints), paired with an agentic-AI assistant that emits typed artifacts (trade tickets, daily pulse, risk reports, macro memos) with real-time web context.
- **Architecture:** a React SPA acting as a pure renderer over a FastAPI backend that owns all data, computation, configuration and the AI proxy, over a PostgreSQL + Redis data layer.
- **Contribution:** built the platform: firm-wide and per-portfolio dashboards, a configurable alert engine, the full risk suite, benchmark-relative performance, and an agentic analysis hub with persisted theses and per-client restructuring assessments.

`Python · FastAPI · SciPy · pandas · agentic LLM · React · TypeScript · Recharts · Docker`

</details>

<details>
<summary><b>Investment Banking</b> &nbsp;·&nbsp; treasury automation, Shariah screening, agentic advisory</summary>

<br/>

#### Treasury middle-office automation &nbsp; ![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624)

On-premise AI risk-intelligence layer for a bank's treasury middle office (market-risk and limit monitoring).

- **Problem:** the daily risk pipeline ran manually on fragile, disconnected tooling, prices arriving as emailed spreadsheets, reconciliation on brittle Excel formulas, swap valuations (MTM, VaR, CVaR) hand-exported with no audit trail, and limit structures in a single unversioned desktop database. Analysts lost hours a day, and tracing why VaR moved meant following files by hand.
- **Solution:** an on-premise RAG assistant plus automated reporting. A scheduled end-of-day pipeline ingests positions, prices and valuations, runs deterministic reconciliation and a data-quality gate, and loads a four-store knowledge layer. A retrieval orchestrator classifies each natural-language question and routes it across the four stores; a hybrid LLM router keeps any query touching sensitive identifiers (ISINs, positions, counterparties) on on-premise open-source models and sends only anonymised, non-sensitive reasoning to a private cloud endpoint, logging every routing decision. A React dashboard replaces the Excel workflow with a market-risk and limit view, an evidence-cited Q&A chat, a live news / market-events feed, and human-in-the-loop report drafting that auto-distributes approved reports to the risk department.
- **Integrations:** market data from **Bloomberg** (illiquid-bond pricing, interest-rate-swap MTM / VaR / CVaR, streaming prices) and **Refinitiv / LSEG** (FX and equities), with lightweight REST backups; the treasury front-to-back trading system and the existing BI data-warehouse (kept as system of record) over REST APIs; news and macro feeds (Bloomberg, Reuters, central-bank RSS and open sources) fed to an event classifier that links news to affected instruments; report distribution over Microsoft Teams and email, with PDF / Excel export.
- **Architecture:** five layers, data sources → ingestion / ETL (a scheduled EOD DAG: reconcile-by-ISIN, data-quality validation, warehouse write-back, news embedding) → a four-store knowledge layer (a **knowledge graph** for desk → limit → instrument → counterparty attribution, a **vector DB** for news, policy docs and per-analyst memory, a **relational warehouse** for numeric risk data, and a **time-series store** for price / VaR history) → a RAG orchestrator with three-tier model routing → a FastAPI backend (REST + WebSocket) and React SPA. On-premise GPU inference serves the open-source models; Docker Compose / Swarm deployment with a deterministic PII pre-filter and a full audit log.
- **Contribution:** designed the end-to-end architecture: the four-store retrieval design, the sensitivity-classification and tiered on-prem / cloud routing for compliance, the market-data and news integrations, the automated EOD pipeline, and the phased roadmap.

`Python · FastAPI · LangChain · Ollama · ChromaDB · FalkorDB · TimescaleDB · PostgreSQL · Prefect · Bloomberg / Refinitiv · React · Docker`

<br/>

#### Shariah-compliance screening &nbsp; ![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624)

Screening and monitoring of publicly listed equities for equity research.

- **Problem:** standard screening reduces to a few static balance-sheet ratios and ignores whether the financials are trustworthy or whether firm conduct is drifting.
- **Solution:** fuses a quantitative accounting-anomaly track (Benford, Zipf, a reduced M-score, threshold-proximity, cross-statement coherence, peer-group Hotelling T-squared) with statistical calibration and false-discovery control, and a qualitative LLM / NLP track (zero-shot NLI plus multilingual sentiment over filings, news and social feeds) into a composite compliance-intelligence score.
- **Architecture:** a FastAPI backend with a React / TypeScript dashboard (plus a Streamlit analytics client) over PostgreSQL and object storage, with Prefect orchestrating the ingestion and scoring pipelines and JWT auth.
- **Contribution:** built the end-to-end platform, from ingestion and panel-build to the detector library, the NLP cascade, backend, dashboard and an accompanying research paper.

`Python · scikit-learn · Transformers · litellm · FastAPI · PostgreSQL · MinIO · Prefect · React`

<br/>

#### Agentic investment-advisory platform &nbsp; ![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624)

Platform for a Sharia-compliant investment, advisory and research firm (portfolio management, buy-side M&A, compliance).

- **Problem:** core workflows are manual and slow, due diligence spans months, Shariah screening is a periodic bolt-on, and portfolio managers lack real-time monitoring, risk alerting and automated reporting across fragmented data.
- **Solution:** an agentic-AI and quant platform in three pillars: an investment copilot of LLM / SLM agents (real-time flagging, automated briefs, VaR / drawdown / stress, rebalancing); a deterministic AI due-diligence pipeline (RAG plus OCR and NLP, forensic / Benford analytics, DCF, multiples and Monte-Carlo valuation, human-in-the-loop Go / No-Go synthesis); and a Shariah-compliance engine (daily screening, AAOIFI rating, manipulation detection).
- **Architecture:** a RAG dashboard over ETL, backtesting and paper-trading pipelines with multi-portfolio orchestration; on-premise deployment.
- **Contribution:** designed the end-to-end architecture and the three-pillar platform.

`Agentic RAG · LLM / SLM · OCR · NLP · MLflow · Monte Carlo · HRP · forensic analytics`

</details>

<details>
<summary><b>Insurance</b> &nbsp;·&nbsp; drought-damage assessment, motor-claims automation</summary>

<br/>

#### Drought-damage claims assessment &nbsp; ![cloud](https://img.shields.io/badge/cloud-30363D?style=flat-square&logo=microsoftazure&logoColor=2088D4)

Regulated drought-subsidence building-damage claims, computer vision plus vision-LLM.

- **Problem:** experts manually inspect large seasonal volumes of field photographs (~150k per season) and hand-fill a standardised damage schedule, which is slow and subjective.
- **Solution:** a CV + vision-LLM pipeline: text-prompted SAM3 segmentation (distilled into a fine-tuned YOLO detector for efficient inference), then a vision LLM grounded on reference cases and the regulated methodology drafts the standardised assessment, returned for expert validation; the AI-draft versus expert-final archive feeds continuous model improvement.
- **Architecture:** an asynchronous FastAPI machine-to-machine service (job lifecycle, callback with retry) with an operator SPA dashboard (FR / EN i18n); a single Docker image deploys to Azure (Key Vault, Blob Storage, Container Apps on a T4 GPU), with a local-parity mode (Vault, MinIO, MLflow) for development.
- **Contribution:** built the end-to-end backend, the integration API, a versioned output-assembly engine, the operator dashboard, and full Azure deployment automation.

`Python · SAM3 · YOLO · PyTorch · Azure OpenAI · Azure ML Studio · FastAPI · MLflow · Vault · MinIO · Azure Container Apps`

<br/>

#### Motor-claims automation & fraud detection &nbsp; ![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624)

Motor (and broader) claims automation for a Takaful insurer.

- **Problem:** manual, fragmented claims handling caused slow turnaround, inconsistent decisions, fraud leakage and high operational cost.
- **Solution:** a human-in-the-loop AI claims platform with omnichannel intake, computer vision that detects, segments and scores vehicle damage and reconciles it against the repair parts list, image-and-metadata fraud flags (staged accidents, pre-existing damage, duplicates), and an LLM that drafts a standardised assessment report.
- **Architecture:** omnichannel intake into a shared data lake feeding pluggable engines, behind an expert-review and governance gate; async job orchestration, machine-to-machine auth, a managed secrets vault, role-based access and full audit / archive; on-premise deployment to keep claims and personal data in-house.
- **Contribution:** designed the claims platform and its phased scope (motor, then credit-life document AI, then medical anomaly detection), reusing components from a prior insurance computer-vision system.

`Computer vision · LLM report generation · OCR · anomaly detection · on-prem · RBAC / audit`

</details>

<details>
<summary><b>Fintech</b> &nbsp;·&nbsp; transaction-fraud detection</summary>

<br/>

#### Transaction-fraud detection &nbsp; ![cloud](https://img.shields.io/badge/cloud-30363D?style=flat-square&logo=microsoftazure&logoColor=2088D4)

Fraud detection for an online payments / transaction-processing operator.

- **Problem:** detect fraudulent or anomalous transactions in real time across a large, evolving transaction network, without relying on scarce labelled fraud examples.
- **Solution:** a graph neural network over the transaction graph performing label-free anomalous sub-graph detection, flagging structural outliers (synchronised timing, implausible account-age distributions, over-clustered patterns, near-duplicate bursts) into a risk-scoring pipeline.
- **Architecture:** a GNN scoring service over the transaction graph feeding a real-time flagging pipeline, on GPU compute.
- **Contribution:** built a GNN-based fraud-scoring capability on the live transaction graph; the architecture proved transferable and was later reused for coordinated-campaign detection.

`PyTorch Geometric · GPU · unsupervised graph anomaly detection`

</details>

<details>
<summary><b>B2B Trade & Procurement</b> &nbsp;·&nbsp; sourcing & tender-intelligence platform</summary>

<br/>

#### Sourcing & tender-intelligence platform &nbsp; ![cloud](https://img.shields.io/badge/cloud-30363D?style=flat-square&logo=microsoftazure&logoColor=2088D4)

Procurement-intelligence platform for an international B2B sourcing / import-export intermediary, with customs HS-code-driven supplier matching and tender monitoring.

- **Problem:** tender-watch and supplier data are scattered across internal spreadsheets and dozens of external portals; monitoring is manual, data is re-keyed by hand, opportunities are found late, and there is no single source of truth for scoring offers against specs, norms and price.
- **Solution:** a deterministic-first decision layer where RPA enriches specs against norms and certifications, weighted rules and an ML model score supplier offers, AI control agents flag mismatches (they never decide), and a RAG chatbot answers natural-language queries; a human arbitrates.
- **Architecture:** a five-layer, fully managed, GPU-free cloud design: per-source connectors with scheduled and event-driven ingestion normalise data and attach HS codes into a PostgreSQL source of truth plus object storage and a vector index; a unified UI (analytics dashboard, pipeline tracker, alert center, embedded chatbot).
- **Contribution:** designed the target five-layer architecture, positioned as a decision-support platform where AI assists and humans retain control.

`PostgreSQL · vector search · RPA · classical ML scoring · agentic AI · RAG · managed cloud`

</details>

<details>
<summary><b>Government / Strategic Communications</b> &nbsp;·&nbsp; narrative-monitoring platform</summary>

<br/>

#### Narrative-monitoring platform &nbsp; ![on-prem](https://img.shields.io/badge/on--prem-30363D?style=flat-square&logo=linux&logoColor=FCC624) ![cloud](https://img.shields.io/badge/cloud-30363D?style=flat-square&logo=microsoftazure&logoColor=2088D4)

National-scale information-integrity and narrative monitoring for a public institution, multilingual.

- **Problem:** detect hostile narratives and false claims early across social, news and messaging channels, predict virality before critical mass, and respond at the highest-leverage points, under strict evidence and policy governance.
- **Solution:** a three-stage funnel: cheap multilingual ingestion with velocity / burst detection, a claim-triage classifier, then two deep streams on accelerating narratives only, a graph neural network forecasting forward propagation and ranking intervention nodes, and a RAG plus constrained-LLM verification engine producing cited verdicts; a deterministic policy engine fuses spread, probability-of-false and severity into tiered responses.
- **Architecture:** a modular streaming platform (Kafka ingestion, a Neo4j graph, a vector store, containerised services on Kubernetes with Prometheus / Grafana / Loki observability), deployable to cloud or fully on-premise / air-gapped.
- **Contribution:** designed the end-to-end architecture, the three-stage funnel, and a dual cloud / on-premise deployment.

`Python · PyTorch Geometric · multilingual transformers · vLLM / Azure OpenAI · Neo4j · Kafka · Qdrant · Kubernetes`

</details>
