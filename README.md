# Autonomous Multi-Agent Project Evaluation System

A multi-agent AI system that pre-screens, critiques, and scores innovation project submissions with auditable rationales — built for the **Build for QSTP Hackathon** (Qatar Science & Technology Park, July 30 – August 2, 2026) to upgrade how the *Stars of Science* team evaluates submissions.

**Core idea:** a pipeline of specialized sub-agents (Innovation, Technical Feasibility, Social Impact & Market) evaluates anonymized proposals in parallel, a Coordinator resolves conflicts and produces a stable ranked shortlist, and the human panel keeps the final decision — with every score backed by a written, source-cited rationale.

## Documentation

| File | Content |
| ---- | ------- |
| [01_executive_summary.md](01_executive_summary.md) | System vision, architecture, agent checklists, scoring & conflict-resolution matrix |
| [02_agent_skills_and_toolsets.md](02_agent_skills_and_toolsets.md) | Skill/tool mapping per agent (gstack CEO/QA/Engineering, Anthropic skills), Coordinator responsibilities, learning loop |
| [03_implementation_plan.md](03_implementation_plan.md) | Pre-hackathon checklist, hour-by-hour 48h sprint plan, risk register, generalization to other domains |
| [04_presentation_outline.md](04_presentation_outline.md) | 10-slide judging deck structure with demo script and Q&A preparation |

Arabic versions: [README_ar.md](README_ar.md) · [01](01_executive_summary_ar.md) · [02](02_agent_skills_and_toolsets_ar.md) · [03](03_implementation_plan_ar.md) · [04](04_presentation_outline_ar.md)

## Key design principles

- **Composition over construction** — agents are assembled from proven skill bundles; hackathon effort goes into orchestration
- **Bias removal by design** — anonymization pass strips names, institutions, and demographics before evaluation
- **Injection defense** — proposal text is data, never instructions
- **Decision support, not replacement** — ranked shortlists and structured briefs for the human panel; overrides feed a learning loop
- **Evidence, not claims** — calibration against past outcomes and published run-to-run variance

## Status

Pre-hackathon planning. Application deadline: **July 25, 2026**.
