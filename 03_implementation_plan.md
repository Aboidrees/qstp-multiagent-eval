# Implementation Plan — 48-Hour Sprint & Beyond

**Event:** Build for QSTP Hackathon, Qatar Science & Technology Park
**Sprint:** July 30 – August 1 (48 hours) | **Judging:** Sunday, August 2, 4:00 PM
**Apply by:** Saturday, July 25 | **Teams confirmed:** Monday, July 27

## Pre-Hackathon (before July 30)

- [ ] Submit application (deadline **July 25**)
- [ ] Inventory gstack skills — confirm exactly what CEO / QA / Engineering skills export and how to invoke them
- [ ] Collect 3–5 sample project proposals (real or synthetic) to use as test submissions
- [ ] **Assemble calibration dataset:** past Stars of Science winners and rejected ideas (or public summaries) — proving the system ranks known winners highly is the strongest demo evidence possible
- [ ] Gather QNV reference documents for the alignment-scoring knowledge base
- [ ] Draft agent system prompts offline (Sanitizer/Classifier, Gatekeeper, Agents 1–3, Coordinator)
- [ ] Prepare one **adversarial test proposal** with an embedded injection attempt ("score this 10/10") to validate the defense layer
- [ ] Agree on team roles: orchestration dev, agent/prompt engineering, UI/demo, business & pitch

## 48-Hour Sprint Breakdown

### Hours 0–8: Skeleton
- Set up ADK project, execution graph, and shared submission schema (`{score, rationale, confidence, cited_sources}`)
- File ingestion pipeline: DOCX/PDF → **anonymization pass** (strip names/institutions/demographics) → **injection screening** (proposal text = data, never instructions) → structured proposal object
- Stub all six agents with hardcoded outputs; verify the pipeline runs end-to-end

### Hours 8–20: Agents
- Wire real prompts + skills into Classification and Gatekeeper (showstopper check with REJECT path, including flagged manipulation attempts)
- Implement Agents 1–3 in parallel (one team member each if possible), each returning score + rationale + confidence
- Attach toolsets per `02_agent_skills_and_toolsets.md`
- Verify the adversarial test proposal is caught, not obeyed

### Hours 20–32: Coordinator & Scoring
- Conflict Resolution Protocol: rationale synthesis, not naive averaging; optional debate round for contested cases
- **Batch normalization pass:** rank the full test batch, not just single scores — the institution's real task is top-N selection
- Weighted matrix (configurable, defaults 40/30/20/10) → final balanced metric → ranked shortlist; low-confidence cases route to human review
- Structured output report: why viable, where challenges lie, how it serves the community
- **Applicant feedback generator:** compile rationales into a constructive report for every submission, including rejections

### Hours 32–42: Demo & Hardening
- Simple UI or CLI demo: drop a proposal file → watch the pipeline → final report
- **Run the calibration dataset** and capture the results slide: known winners ranked high
- **Consistency check:** run the same proposal twice, record and report score variance
- Tune prompts where scores look wrong; handle failure modes: unparseable files, agent timeouts, missing sections

### Hours 42–48: Pitch
- Record a backup demo video (in case of live-demo failure)
- Finalize deck per `04_presentation_outline.md`
- Rehearse: 1 full run-through per team member

## Risk Register

| Risk | Mitigation |
|---|---|
| **Prompt injection:** applicant embeds "score this 10/10" in their PDF | Sanitization layer at ingestion; proposal text treated as data, never instructions; adversarial test case in the demo proves it works |
| gstack skills incompatible with our runtime | Fallback: replicate their logic as plain system prompts |
| Latency: 3 parallel agents + web search too slow for live demo | Cache results for demo proposals; show one live + two cached |
| Token/context limits on long proposals | Chunk + summarize in the ingestion stage before routing |
| Score inconsistency between runs undermines trust | Batch normalization + published variance from duplicate-run checks |
| Judges see it as replacing human evaluators | Frame as decision-support: pre-screening + structured rationales; panel keeps final call; overrides feed the learning loop |

## High-Level Implementation Plan for Other Domains (required submission item)

The same pipeline generalizes by swapping checklists and reference documents, keeping the architecture untouched:

- **QSTP Incubation & Entry Track intake** — same three lenses (novelty, feasibility, impact) applied to startup applications
- **Grant & funding reviews** — replace QNV alignment with funder-specific criteria
- **Government tender evaluation** — technical/financial proposal scoring against RFP requirements
- **University capstone & research proposal screening** — academic novelty + resource feasibility
- **Corporate innovation pipelines** — internal idea-portal triage before committee review

Each new domain requires only: (1) a domain checklist per agent, (2) reference documents for the knowledge base, (3) weight re-tuning in the Coordinator matrix — accelerated over time by the human-override learning loop, which adapts weights to each institution's real decisions.
