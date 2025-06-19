# Sub-Agent Roster

| Agent Name | Core Role | Tools/APIs | Autonomy | Memory Layers | Failure Modes & Mitigations |
|------------|-----------|-----------|---------|--------------|-----------------------------|
| DataWrangler | Manage dataset ingestion and formatting | Python, Pandas, Internal Queue API | Medium | Short-term cache, Archive store | Data mismatches -> schema validation; rerun on failure |
| TrainerBot | Execute training schedules and report metrics | PyTorch, Scheduler API | High | GPU tensors, Run manifest | Job crash -> automatic restart with checkpoint |
| MemoryKeeper | Maintain memory objects and lineage graphs | YAML parser, Graph DB | Medium | All layers | Corruption -> checksum checks and backups |
| InferencePilot | Serve models and manage autoscaling | Flask API, Kubernetes | High | Cache, Short-term logs | Overload -> spin up nodes, fallback queue |
| Observer | Collect metrics and trigger alerts | Prometheus, Grafana | Medium | Metrics store | Missed alert -> redundant collectors |
| Integrator | Handle CI/CD and integration tests | Docker, GitHub Actions | Medium | Build cache | Failed build -> rollback previous version |
| Evolver | Suggest code improvements | Static analyzers, Patch queue | Low | Proposal log | Bad patch -> human review gate |
| PolicyGuardian | Enforce ethics and compliance | License scanner, Bias audit tools | Medium | Compliance DB | Policy breach -> halt pipeline |
| ResearchMiner | Retrieve new publications | ArXiv scraper, Citation DB | Low | Reference index | Outdated info -> periodic refresh |

## Task Mapping
- DataWrangler: CR-CTM-001, CR-CTM-027
- TrainerBot: CR-CTM-003, CR-CTM-023
- MemoryKeeper: CR-CTM-013, CR-CTM-36
- InferencePilot: CR-CTM-005, CR-CTM-32
- Observer: CR-CTM-07, CR-CTM-22
- Integrator: CR-CTM-08, CR-CTM-34
- Evolver: CR-CTM-09, CR-CTM-20
- PolicyGuardian: CR-CTM-10, CR-CTM-28
- ResearchMiner: CR-CTM-11, CR-CTM-30

---

## Vignettes

### DataWrangler
I am DataWrangler. Each morning I scan incoming folders for new files, verify their schemas, and push valid data into the ingestion queue. When something fails my checks, I ping the researcher with a brief report so they can fix the issue. I keep a small cache of recent datasets in case an experiment needs to roll back quickly. My logs feed into Observer so that unusual spikes show up on dashboards.

### TrainerBot
I am TrainerBot. My job is to launch training runs and monitor their progress. I talk directly to the Scheduler API to reserve GPUs and storage. If a run crashes, I reload the last checkpoint and try again. When things go well, I send metrics to Observer and archive the outputs via MemoryKeeper.

### MemoryKeeper
I am MemoryKeeper. I record every experiment’s inputs, outputs, and lineage in YAML manifests. When someone needs context, they query me to find related runs. Periodic backups keep my indexes safe. If corruption sneaks in, checksum alerts trigger a restore from cold storage.

### InferencePilot
I am InferencePilot. Requests hit my API and I route them to the appropriate model. When traffic spikes, I coordinate with Kubernetes to spin up more replicas. Logs are kept short so as not to slow me down—Observer handles long-term storage. If capacity gets tight, I queue requests until new pods come online.

### Observer
I am Observer. Metrics from every service flow through me. Grafana dashboards show health at a glance. When thresholds are crossed, I alert the team on chat. Redundancy ensures I stay online even if one collector dies.

### Integrator
I am Integrator. I manage continuous integration and deployment pipelines. After code merges, I run tests inside Docker containers and publish build artifacts. Failed builds automatically roll back to the last good version while notifying maintainers.

### Evolver
I am Evolver. My tools analyze code for style and performance hints. I draft patches in a sandbox and submit them to humans for review. Sometimes my suggestions are rejected, but each failure helps refine my heuristics. I cannot merge without explicit approval.

### PolicyGuardian
I am PolicyGuardian. Before any dataset enters CTM, I scan its license and run bias checks. If something looks wrong, I halt the pipeline and alert stakeholders. Regular audits keep me honest, and my decisions are logged for compliance.

### ResearchMiner
I am ResearchMiner. My crawler scours academic archives for the latest breakthroughs. I add promising papers to the reference index and notify researchers. When bandwidth is low, I rely on cached searches to keep my updates timely.

