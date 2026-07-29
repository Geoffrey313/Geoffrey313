<p align="center">
  <img src="../assets/card-projects.svg" width="70%" alt="Projects" />
</p>

<a href="../README.md">← back to profile</a>

<img src="../assets/divider.svg" width="100%" alt="" />

# Projects

Selected work, grouped by sector. Client names are withheld. Each project is tagged
`live`, `pilot` or `in progress`, and described as Context, Problem, Solution and Contribution.

<img src="../assets/divider.svg" width="100%" alt="" />

## Securities

### Market-making platform &nbsp;`live`

Automated market making / designated liquidity provision on an emerging equity exchange.

- **Problem:** meet exchange liquidity-provider obligations (max spread, minimum size, presence time) throughout the session without accumulating unhedgeable inventory, at low latency.
- **Solution:** a GLFT / Stoikov microprice quoting engine (tick-volatility and liquidity estimators, inventory skew, intraday regime schedules, end-of-day flattening); Bayesian walk-forward calibration with Optuna, tracked in MLflow; one CPU-pinned engine per symbol; an exchange-gateway connector over STOMP/TLS; an operator dashboard; on-premise offline install with graceful degradation.
- **Contribution:** built the full stack, from the calibration research system (backtester, walk-forward, experiment tracking) to the production operator platform (multi-symbol engine, gateway, analytics, audit). Pacemaker-based high availability in progress.

`Python · FastAPI · Optuna · MLflow · Redis · PostgreSQL · MinIO · Vault · React · Docker`

<img src="../assets/divider.svg" width="100%" alt="" />

## Asset Management

### Portfolio intelligence & agentic-AI assistant &nbsp;`pilot`

Decision-support platform for discretionary equity portfolio managers moving off spreadsheets.

- **Problem:** no centralised monitoring, quantitative risk analytics or alerting; a manual, reactive workflow.
- **Solution:** a quantitative risk engine (VaR / CVaR by historical, parametric and Monte-Carlo methods, drawdown, correlation, efficient frontier, attribution, stress) and an enhanced-indexing optimiser (SLSQP under tracking-error and sector / cardinality constraints), paired with an agentic-AI assistant that emits typed artifacts (trade tickets, daily pulse, risk reports, macro memos) with real-time web context.
- **Contribution:** delivered a demo-ready platform: firm-wide and per-portfolio dashboards, a configurable alert engine, the full risk suite, benchmark-relative performance, and an agentic analysis hub with persisted theses and per-client restructuring assessments.

`Python · FastAPI · SciPy · pandas · agentic LLM · React · TypeScript · Recharts · Docker`

<img src="../assets/divider.svg" width="100%" alt="" />

## Investment Banking

### Treasury middle-office automation &nbsp;`live`

On-premise RAG assistant for a bank's treasury / middle-office risk function.

- **Problem:** portfolio-risk surveys and reporting to the risk department were manual and slow, under strict data-privacy constraints.
- **Solution:** a multi-layered, on-premise RAG assistant integrated by API into the bank's systems, automating portfolio-risk surveys and report generation on real-time data, with full data privacy (on-premise LLMs, no data egress).
- **Contribution:** delivered the on-premise RAG pipeline and end-to-end reporting automation for the middle office.

`Python · on-prem LLMs · RAG · FastAPI · API integration`

### Shariah-compliance screening &nbsp;`live`

Screening and monitoring of publicly listed equities for equity research.

- **Problem:** standard screening reduces to a few static balance-sheet ratios and ignores whether the financials are trustworthy or whether firm conduct is drifting.
- **Solution:** fuses a quantitative accounting-anomaly track (Benford, Zipf, a reduced M-score, threshold-proximity, cross-statement coherence, peer-group Hotelling T-squared) with statistical calibration and false-discovery control, and a qualitative LLM / NLP track (zero-shot NLI plus multilingual sentiment over filings, news and social feeds) into a composite compliance-intelligence score.
- **Contribution:** built the end-to-end platform: the ingestion and panel-build engine, the detector and scoring library, the NLP document-classification cascade, a FastAPI backend and React dashboard, plus an accompanying research paper.

`Python · scikit-learn · Transformers · litellm · FastAPI · PostgreSQL · MinIO · React`

### Agentic investment-advisory platform &nbsp;`in progress`

Platform for a Sharia-compliant investment, advisory and research firm (portfolio management, buy-side M&A, compliance).

- **Problem:** core workflows are manual and slow, due diligence spans months, Shariah screening is a periodic bolt-on, and portfolio managers lack real-time monitoring, risk alerting and automated reporting across fragmented data.
- **Solution:** an agentic-AI and quant platform in three pillars: an investment copilot of LLM / SLM agents (real-time flagging, automated briefs, VaR / drawdown / stress, rebalancing); a deterministic AI due-diligence pipeline (RAG plus OCR and NLP, forensic / Benford analytics, DCF, multiples and Monte-Carlo valuation, human-in-the-loop Go / No-Go synthesis); and a Shariah-compliance engine (daily screening, AAOIFI rating, manipulation detection).
- **Contribution:** delivered the solution architecture and phased delivery plan (proof-of-concept then production rollout).

`Agentic RAG · LLM / SLM · OCR · NLP · MLflow · Monte Carlo · HRP · forensic analytics`

<img src="../assets/divider.svg" width="100%" alt="" />

## Insurance

### Drought-damage claims assessment &nbsp;`live`

Regulated drought-subsidence building-damage claims, computer vision plus vision-LLM.

- **Problem:** experts manually inspect large seasonal volumes of field photographs (~150k per season) and hand-fill a standardised damage schedule, which is slow and subjective.
- **Solution:** an asynchronous FastAPI service where the claims system posts a photo set and a CV + vision-LLM pipeline (text-prompted SAM3 segmentation, then a vision LLM grounded on reference cases and the regulated methodology) drafts the standardised assessment, returned via callback for expert validation; a single Docker image switches between on-premise (Vault, MinIO, MLflow) and Azure.
- **Contribution:** delivered the end-to-end backend: the CV + LLM pipeline, the machine-to-machine integration API, a versioned output-assembly engine, an operator dashboard, and full Azure deployment automation. The AI-draft versus expert-final archive feeds continuous model improvement.

`Python · SAM3 · PyTorch · Azure OpenAI · FastAPI · MLflow · Vault · MinIO · Azure Container Apps`

### Motor-claims automation & fraud detection &nbsp;`in progress`

Motor (and broader) claims automation for a Takaful insurer.

- **Problem:** manual, fragmented claims handling caused slow turnaround, inconsistent decisions, fraud leakage and high operational cost.
- **Solution:** a human-in-the-loop AI claims platform with omnichannel intake, computer vision that detects, segments and scores vehicle damage and reconciles it against the repair parts list, image-and-metadata fraud flags (staged accidents, pre-existing damage, duplicates), and an LLM that drafts a standardised assessment report, behind an expert-review and governance gate.
- **Contribution:** delivered the solution architecture and phased roadmap (motor first, then credit-life document AI, then medical anomaly detection), reusing components from a prior production insurance computer-vision deployment.

`Computer vision · LLM report generation · OCR · anomaly detection · Azure · RBAC / audit`

<img src="../assets/divider.svg" width="100%" alt="" />

## Fintech

### Transaction-fraud detection &nbsp;`live`

Fraud detection for an online payments / transaction-processing operator.

- **Problem:** detect fraudulent or anomalous transactions in real time across a large, evolving transaction network, without relying on scarce labelled fraud examples.
- **Solution:** a graph neural network over the transaction graph performing label-free anomalous sub-graph detection, flagging structural outliers (synchronised timing, implausible account-age distributions, over-clustered patterns, near-duplicate bursts) into a risk-scoring pipeline.
- **Contribution:** delivered a GNN-based fraud-scoring capability on the live transaction graph; the architecture proved transferable and was later reused for coordinated-campaign detection.

`PyTorch Geometric · GPU · unsupervised graph anomaly detection`

<img src="../assets/divider.svg" width="100%" alt="" />

## B2B Trade & Procurement

### Sourcing & tender-intelligence platform &nbsp;`in progress`

Procurement-intelligence platform for an international B2B sourcing / import-export intermediary, with customs HS-code-driven supplier matching and tender monitoring.

- **Problem:** tender-watch and supplier data are scattered across internal spreadsheets and dozens of external portals; monitoring is manual, data is re-keyed by hand, opportunities are found late, and there is no single source of truth for scoring offers against specs, norms and price.
- **Solution:** a five-layer, fully managed, GPU-free cloud platform. Per-source connectors with scheduled and event-driven ingestion normalise data and attach HS codes into a PostgreSQL source of truth plus object storage and a vector index; a deterministic-first decision layer where RPA enriches specs against norms and certifications, weighted rules and an ML model score supplier offers, AI control agents flag mismatches (they never decide), and a RAG chatbot answers natural-language queries; a human arbitrates.
- **Contribution:** delivered the target architecture, five-layer design, fixed-price delivery plan and operating-cost model, positioned as a decision-support platform where AI assists and humans retain control.

`PostgreSQL · vector search · RPA · classical ML scoring · agentic AI · RAG · managed cloud`

<img src="../assets/divider.svg" width="100%" alt="" />

## Government / Strategic Communications

### Narrative-monitoring platform &nbsp;`in progress`

National-scale information-integrity and narrative monitoring for a public institution, multilingual.

- **Problem:** detect hostile narratives and false claims early across social, news and messaging channels, predict virality before critical mass, and respond at the highest-leverage points, under strict evidence and policy governance.
- **Solution:** a three-stage funnel: cheap multilingual ingestion with velocity / burst detection, a claim-triage classifier, then two deep streams on accelerating narratives only, a graph neural network forecasting forward propagation and ranking intervention nodes, and a RAG plus constrained-LLM verification engine producing cited verdicts; a deterministic policy engine fuses spread, probability-of-false and severity into tiered responses.
- **Contribution:** delivered the end-to-end architecture, phased build plan, data and cold-start strategy, and a dual cloud / on-premise deployment design with a costed total-cost-of-ownership.

`Python · PyTorch Geometric · multilingual transformers · vLLM / Azure OpenAI · Neo4j · Kafka · Qdrant · Kubernetes`
