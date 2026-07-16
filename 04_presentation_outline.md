# Presentation Outline — Judging Deck (~10 slides)

**Audience:** QSTP judges & Stars of Science team | **Judging:** Sunday, August 2, 4:00 PM
**Golden rule:** Frame as *decision-support that augments the human judges* — pre-screening, structured rationales, bias reduction — never as replacing evaluators.

## Slide 1 — Title
- Project name + one-line value proposition: "An autonomous multi-agent system that pre-screens and scores project submissions with auditable rationales"
- Team names & roles

## Slide 2 — The Problem
- Stars of Science / QSTP receive large volumes of submissions per cycle
- Manual screening: slow, expensive, inconsistent between reviewers, prone to fatigue and bias
- Strong ideas can be missed; weak ones consume expert panel time; rejected applicants get no feedback

## Slide 3 — The Solution
- Multi-agent evaluation pipeline: Sanitize & Anonymize → Classify → Showstopper Gate → 3 parallel specialist agents → Coordinator
- Output: a **stable ranked shortlist** (not just isolated scores) + structured report explaining *why* viable, *where* the challenges are, *how* it serves the community
- Human panel receives ranked, pre-audited submissions — final decision stays human, and panel overrides feed a learning loop

## Slide 4 — Architecture
- Pipeline diagram (from `01_executive_summary.md` §4)
- Highlight: anonymization + injection defense at ingestion, parallel review, early rejection gate conserves resources, conflict resolution instead of naive averaging, low-confidence cases escalate to humans

## Slide 5 — The Three Lenses
- Agent 1: Innovation & Scientific Contribution (novelty, IP, value-add)
- Agent 2: Technical Execution & Feasibility — the CEO/Engineering perspective (gstack skills)
- Agent 3: Social Impact, Market & Risk — the "Outside Voice" (QNV alignment)
- Every agent output: score + written rationale + confidence + cited sources

## Slide 6 — Composition Over Construction
- Built from proven skill bundles (Anthropic skills, gstack CEO/QA/Engineering) — not evaluators from scratch
- Our 48 hours went into orchestration, scoring logic, and the Coordinator
- This is why it works in 48 hours *and* why it's maintainable after adoption

## Slide 7 — LIVE DEMO
- Drop a real proposal file → pipeline runs → final report appears
- Show one contested case: agents disagree, debate round, Coordinator resolves via rationales
- **Calibration moment:** past Stars of Science winners run through the system rank at the top — evidence, not claims
- **Security moment:** the adversarial proposal with an embedded "score this 10/10" injection gets caught and flagged, not obeyed
- (Backup: pre-recorded video)

## Slide 8 — Scoring, Trust & Safety
- Weighted matrix — **configurable, institution-owned** (defaults: 40% innovation / 30% feasibility / 20% market & risk / 10% social impact)
- Every score carries a written rationale with cited sources — fully auditable, no black box
- **Anonymization:** agents never see names, institutions, or demographics — bias removal by design, not by promise
- **Measured consistency:** same proposal run twice, variance reported — we tested our own reliability
- Showstopper gate: fatal flaws rejected early with explicit justification

## Slide 9 — Beyond Stars of Science
- Same architecture, swap the checklists: incubation intake, grant reviews, tender evaluation, capstone screening
- Implementation cost per new domain: checklist + reference docs + weight tuning only
- **Applicant feedback reports turn rejections into resubmissions** — the system grows the ecosystem, not just filters it

## Slide 10 — Ask & Roadmap
- Pilot with the Stars of Science team on next cycle's real submissions
- Roadmap: Arabic-language submissions, human-override learning loop re-tuning weights from real panel decisions, reviewer dashboard, applicant feedback portal
- Team contact info

## Q&A Prep

| Likely question | Answer angle |
|---|---|
| "Are you replacing our judges?" | No — pre-screening + structured briefs; panel time shifts to the best candidates; overrides re-tune the system |
| "What if applicants try to manipulate the AI?" | Injection defense at ingestion — proposal text is data, never instructions; we demo a live caught attempt |
| "What about AI bias?" | Anonymization pass + explicit checklists + auditable rationales; weights set by the institution; human final call |
| "How do we know the scores mean anything?" | Calibration against past outcomes: known winners rank highly; consistency variance measured and published |
| "Hallucinated patent/market claims?" | Web-search verification per claim; rationales cite sources; confidence field flags uncertainty for human review |
| "Cost per evaluation?" | Estimate token cost per submission; compare vs. expert-hours per manual screen |
| "Arabic submissions?" | Roadmap item; Claude handles Arabic natively, checklists are language-agnostic |
