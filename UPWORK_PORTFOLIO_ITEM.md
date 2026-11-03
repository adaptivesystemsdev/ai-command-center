# Upwork portfolio item — Adaptive Systems AI stack

**Title:** AI Receptionist, Website Chat & Lead Scoring — one config-driven, self-hosted engine

**Role:** Sole engineer — architecture, backend (Python + TypeScript), voice agent, data layer,
orchestration, infrastructure, security, testing

**Skills:** Python, TypeScript, FastAPI, LangGraph, Pydantic AI, RAG, pgvector, PostgreSQL, Redis,
n8n, ElevenLabs, Google Calendar API, Telegram Bot API, Postfix, Next.js, Docker, nginx, MCP

---

## Summary (~150 words)

A self-hosted AI engine that businesses configure instead of commissioning. Each client is a folder
of config files: hard facts (hours, prices, services), documents, scoring rules and reply templates.
From that, the engine answers customer questions with checkable citations and never invents a price
or opening time, books real appointments into the business's Google Calendar and emails the
confirmation, runs an ElevenLabs voice receptionist built from the same config (browser and the
business's own phone number), puts a chat widget
(with a call button) on any website with one script tag, runs the same assistant as a Telegram bot,
turns forwarded emails and contact forms into leads, and scores them with an LLM checked by a
deterministic TypeScript policy gate. The team works from one inbox across every channel, can take
over a chat live, and gets alerts, reminders and a signed webhook into any CRM (tested n8n recipes
for HubSpot and HighLevel). Every decision is
audit-logged per client. Security is tested, not assumed: injection detectors, tenant isolation
between every client pair, SSRF-safe ingestion, signed webhooks, per-visitor caps on anything that costs.

## Measured on the live system

- Lead qualification p50 3.0 s / p95 12 s on 281 real leads (audit log, 29 Oct – 1 Nov 2026), with a fallback chain and a review route instead of errors
- Deterministic policy gate ≈ 10 ms, no model call
- Voice tools: facts p95 38 ms, availability 354 ms, booking 971 ms (Google Calendar write included)
- Real voice call test 17/17 (docs question, two injection attempts, book + cancel, signed webhook stored)
- Chat turn 1–4 ms when code handles it, 1.3–3.7 s with the router model
- Published eval (2026-11-03, production model chain): 20/20 test leads decided right, 45/45 held-out
  support answers right, for 3 businesses
- Real phone call answered by our own agent on a US Twilio number (2026-11-03)
- 832 static checks, 101 per-client live tests, 42 chat, 15 forms, 5 calendar, 21 voice, 90 app checks

## Highlights for proposals

- Hard facts come from config, never from the model; out-of-scope questions are refused.
- Explainable decisions: score, per-gate pass/fail and reason codes for every lead.
- Adding a client is configuration, not development.
- Channels plug into what the business already has: one script tag, a form URL, an email forward,
  a Telegram bot, its own calendar and phone number (proven on a real US number).
- Human handoff: the owner replies live into the visitor's chat from one inbox.
- GDPR erasure by anonymisation; signed webhooks into any CRM, with tested n8n recipes for HubSpot,
  HighLevel (calendar included) and Google Sheets.
- Runs on the client's own server (installer with upgrades and rollback) or hosted; the client owns its data.

**Live:** live numbers https://adaptivesystems.dev/live · status page
https://status.adaptivesystems.dev/status/stack · walkthrough of the private app on request.
