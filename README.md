# PathPilot

**AI-guided study-abroad and travel workflows for service teams.**

PathPilot is an agentic **n8n** workflow prototype for a Nigerian study-abroad/travel agency
(Dextravl-like). It turns a raw customer enquiry into a structured lead → intent
classification → RAG-grounded recommendation → **human approval** → emailed response →
follow-up task → audit log + dashboard. The LLM reasons and drafts; humans approve anything
customer-facing.

## 🔗 Interactive walkthrough

A self-contained, clickable reconstruction of the full demo (real execution data, step
navigation, hotspots, narration) lives at [`demo/index.html`](demo/index.html). Published via
**GitHub Pages** (Settings → Pages → deploy from branch → **root**):

**→ https://fisayo-rm.github.io/path-pilot/demo**

## Status

| Phase | Status |
|---|---|
| **Phase 0 — Discovery & scope lock** | ✅ Complete |
| **Phase 1 — Foundations** | ✅ Complete (Supabase schema, WF1 intake, prompts) |
| **Phase 2 — Extraction & classification** | ✅ Complete (WF2, 8/8 classification — [`phase-2/results.md`](phase-2/results.md)) |
| **Phase 3+4 — RAG & recommendation** | ✅ Complete (WF3+WF7, KB ingested, recommendations generated — [`phase-3-4/results.md`](phase-3-4/results.md)) |
| **Phase 5 — Human approval & follow-up** | ✅ Complete (WF4 Gmail sendAndWait, WF5 scheduler — [`phase-5/results.md`](phase-5/results.md)) |
| **Phase 6 — Dashboard & demo prep** | ✅ Complete (Supabase views, WF8, demo script — [`phase-6/`](phase-6/)) |

## Locked stack (Phase 0)

n8n Cloud · **Claude (Anthropic)** reasoning · **Supabase (Postgres + pgvector)** data & RAG ·
OpenAI `text-embedding-3-small` embeddings *(default, confirm in Phase 3)* · **Gmail** for
customer email · web-form intake. Full rationale: [`phase-0/00-scope-lock.md`](phase-0/00-scope-lock.md).

## Repository map

```
PathPilot_PRD.md                     Product requirements
PathPilot_Roadmap.md                 6-week phased plan
PathPilot_Technical_Architecture.md  Architecture, workflows, data model

phase-0/
  00-scope-lock.md                   ⭐ Master Phase 0 decisions, scope, demo, metrics
  01-workflow-map.md                 End-to-end flow + 8 n8n workflows + phases
  02-risk-safeguard-checklist.md     Risks, safeguards, privacy/consent, responsible-AI

knowledge-base/
  README.md                          KB outline, metadata schema, governance, index
  countries/                         UK · Canada · Malta · Finland study profiles
  checklists/                        Undergraduate · Postgraduate · UK visit-visa
  guidance/                          IELTS/TOEFL · Budget planning
  service/                           Service packages · Escalation policy (internal)
  faq/                               General FAQ

sample-data/
  sample-enquiries.md                10 labelled test enquiries (human-readable)
  sample-enquiries.json              Same, machine-readable with ground-truth labels

db/
  schema.sql                         Supabase schema (7 tables + pgvector preview + seed)

prompts/                             Versioned Claude prompts (system, extraction, missing-info)

workflows/
  wf1-lead-intake.json               WF1 — intake + consent + dedup → Call WF2
  wf2-extract-classify.json          WF2 — Claude extract/classify → update lead

phase-2/
  results.md                         Phase 2 test results (8/8 classification)
```

## The demo (hero scenario)

A prospective Nursing undergraduate in Ibadan, WAEC results, no IELTS, limited budget,
undecided between UK/Canada/Malta/Finland. PathPilot extracts the details, asks for what's
missing, retrieves approved country + admission + IELTS guidance, drafts a next-step plan,
routes it to a counsellor, sends the approved email, and schedules a follow-up — all logged.

> ⚠️ Prototype using **synthetic sample data**. Knowledge-base figures are indicative only
> and must be verified against official sources. No real customer data; test data is deleted
> after evaluation.
