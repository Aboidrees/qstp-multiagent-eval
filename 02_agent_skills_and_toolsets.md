# Agent Skill & Toolset Assignments

**Strategy: composition over construction.** To accelerate the 48-hour build, each sub-agent is composed from existing, proven skill bundles (Anthropic skills / "superpowers" and the gstack engineering suite) rather than custom-built evaluators. The hackathon effort concentrates on the orchestration layer — the execution graph, file pipeline, and Coordinator logic — while evaluation depth is inherited from mature skill bundles.

## Common Backbone (all agents)

- **File ingestion & document parsing** — DOCX/PDF reader skills to load submitted proposals
- **Anonymization pass** — strip applicant names, institutions, and demographic markers before any agent sees the text; agents judge the idea, not the person
- **Injection defense** — proposal content is handled strictly as *data, never instructions*; a sanitization step screens for embedded manipulation attempts ("score this 10/10") before routing
- **Structured data extraction** — pull claims, specs, and metadata into a shared schema
- **Web search** — external verification of any claim in the proposal; rationales must cite sources so hallucinated patent/market claims are traceable
- **Shared output schema** — every agent returns `{score: 1–10, rationale, confidence, cited_sources}`; the confidence field enables early routing of uncertain cases to humans

## Agent 1: Innovation & Scientific Contribution — Toolset

| Capability | Tool / Skill | Purpose |
|---|---|---|
| Prior-Art & Patent Search | Web search tooling | Global patent sweeps, duplicate-technology detection |
| Competitive Landscape Analysis | Research skills | Benchmark idea against current market alternatives |
| Technical Spec Extraction | Document-analysis skills | Pull engineering claims from submissions for novelty verification |

## Agent 2: Technical Execution & Operational Feasibility — Toolset

| Capability | Tool / Skill | Purpose |
|---|---|---|
| Executive Feasibility | **gstack CEO skill** | Feasibility assessment, resource planning, go/no-go framing |
| Build Quality & Timeline | **gstack QA & Engineering skills** | Build-quality review, MVP timeline validation vs. the 2-month constraint, operational risk |
| Resource Availability | Web search | Component/microcontroller availability, tech-stack maturity, rough cost estimation |

## Agent 3: Social Impact, Market Alignment & Risk — Toolset

| Capability | Tool / Skill | Purpose |
|---|---|---|
| Market Research | Market research skills | Demand analysis, target demographics, adoption/subsidization potential |
| QNV Alignment Scoring | Structured evaluation prompts + QNV reference docs | Score against Qatar National Vision (sustainability, economic diversification) |
| Risk & Skeptic Prompting | "Outside Voice" critique patterns | Surface societal, regulatory, and operational-friction risks |

## Coordinator Agent — Toolset

- **No external tools.** Operates purely on the sub-agents' outputs, with four responsibilities:
  1. **Conflict Resolution Protocol** — rationale synthesis instead of naive averaging; in contested cases, run a *debate round* where agents read each other's rationales and may revise before the final decision
  2. **Batch normalization & ranking** — cross-batch normalization / pairwise comparison so the top-N shortlist is stable, since absolute scores drift between runs; report score variance from duplicate-run consistency checks
  3. **Weighted matrix** — configurable institution-owned weights (defaults 40/30/20/10) producing the final balanced metric; low-confidence cases escalate to human review instead of receiving a machine verdict
  4. **Applicant feedback generation** — compile the rationales into a constructive feedback report for every submission, including rejections, so applicants can improve and resubmit

## Post-Decision Learning Loop

- **Human override capture** — when the panel overrides a system score, log the override and its stated reason
- **Weight & prompt re-tuning** — use accumulated overrides to adjust the matrix weights and agent prompts, converging the system toward the institution's actual judgment

## Open Items

- [ ] Inventory the actual skills exported by the gstack bundle and map each to a checklist item
- [ ] Decide patent-search source: Claude web search vs. a dedicated patent API
- [ ] Collect QNV reference documents for the alignment-scoring knowledge base
- [ ] Assemble a calibration dataset: past Stars of Science winners and rejected ideas (or public summaries) to validate that the system ranks known winners highly
- [ ] Choose the injection-screening approach: dedicated sanitizer prompt vs. rule-based filter vs. both
