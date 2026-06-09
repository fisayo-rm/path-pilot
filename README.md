# PathPilot

**An agentic study-abroad & travel concierge** that turns a raw customer enquiry into a
human-approved, source-grounded plan — built on n8n, Claude, and Supabase for a Nigerian
study-abroad/travel agency.

## Try it

- ▶ **Live console** — triggers the real workflows and proves each step against the live database:
  **https://pathpilot-demo-console.vercel.app**
- 🎬 **Interactive walkthrough** — a narrated, no-setup tour of the full journey (with a button into the live console):
  **https://fisayo-rm.github.io/path-pilot/demo**

Both run on **synthetic sample data** — no real customers.

## What it does

A customer enquiry flows through an agentic pipeline, with a human gate before anything reaches a customer:

1. **Intake** — a web form (or webhook) captures the enquiry behind a consent gate.
2. **Extract & classify** — Claude turns free text into structured fields, a service intent, and a 0–100 lead score.
3. **Recommend** — for a qualified lead, a similarity search over an approved knowledge base (pgvector) grounds a drafted staff summary and customer message — flagged `safe_to_send: false`.
4. **Human approval** — a counsellor approves or declines; only on approval is the customer email sent.
5. **Follow-up & dashboard** — a follow-up task is scheduled and pipeline metrics update.
6. **Audit** — every system, AI, and staff action is appended to an immutable log.

The model reasons and drafts; **humans approve anything customer-facing**, and guidance is drawn
only from approved, dated sources — never invented.

## Stack

**n8n** (orchestration) · **Claude / Anthropic** (reasoning) · **Supabase** Postgres + **pgvector**
(data & retrieval) · **OpenAI** embeddings · **Gmail** (customer email).

## In this repo

- [`workflows/`](workflows/) — the n8n workflow definitions as version-controlled JSON, importable into n8n.
- [`demo/index.html`](demo/index.html) — the source of the interactive walkthrough.

> ⚠️ Prototype on synthetic data. Knowledge-base figures are indicative only and must be verified
> against official sources. Not a guarantee of admission, a visa, or a scholarship.
