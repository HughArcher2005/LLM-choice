# Handoff: Cheaper crons (build this next)

**Audience:** Cursor Desktop in this repo (`HughArcher2005/LLM-choice`), then a new dedicated product repo.  
**Date:** 18 October 2026  
**Status:** Planning + public explainer tab only. No product code yet.  
**Live site:** https://llm-choice-for-skillify.vercel.app → tab **Cheaper crons**  
**Notion (private draft):** https://app.notion.com/p/3fd24f14e1ca81e3aa2fdadcbb1a1fc1  

This file is the working brief. The website tab is the short public version. Prefer this file when implementing.

---

## One-line pitch

A proxy in front of OpenRouter that makes expensive, repeated cron / scheduled LLM jobs cheaper by shadow-testing lower-cost models (and eventually non-LLM paths), switching only when quality holds.

---

## Why this exists

Control Tower already scores crons for quality vs cost (Astra / Sol / Luna style work). Many scheduled jobs are routine. Teams still pin frontier models. OpenRouter gives **one API key** and you change the **model slug** across labs (Anthropic ↔ OpenAI ↔ others). No need for a separate key per company.

We want to productize that: watch traffic → prove a cheaper model is good enough → switch → show savings.

---

## What we are *not* building

- **Not an OpenRouter “plugin” for sale.** OpenRouter plugins are first-party request features (web, PDF, response healing, Pareto Router, etc.). There is no third-party paid plugin marketplace. “Become a provider” is for selling *inference*, not apps. Discovery = Awesome OpenRouter list + our own site/billing.
- **Not a 20% savings revenue-share in v1.** Hard to meter, dispute, and trust. Prefer ~£2/month (or similar low flat fee) first; revisit share-of-savings later.
- **Not rewriting Skillify’s privacy / ZDR stack in v1.** First product is a general OpenRouter-facing proxy. Dogfood on cron fleets that already use OpenRouter.

---

## Product shape (v1)

### User story

1. User has many crons hitting OpenRouter with expensive models.
2. They point those jobs at **our base URL** (OpenAI-compatible), keep using **their OpenRouter API key** (BYOK) or a key they mint for the product.
3. Week one: we **measure** and **shadow-run** cheaper candidates. Production model stays put.
4. When a candidate beats the quality gate for enough samples, we **promote** it.
5. Dashboard: per-cron model, candidates, quality trend, $ saved, one-click revert.

### Core loop

```
cron request
  → proxy (auth, cron id, logging)
  → primary completion (current model)
  → async shadow: cheaper model(s) on same input
  → score shadow vs primary (or vs gold / rubric)
  → if gate passes for N samples → switch primary
  → always emit usage + cost + quality events
```

### Must-have components

| Piece | Job |
| --- | --- |
| OpenAI-compatible proxy | Drop-in `base_url` swap; forward to `https://openrouter.ai/api/v1` |
| Cron / job identity | Header or path so we can learn per job (`X-Cron-Id`, API key hash + model, etc.) |
| Traffic log | Prompt fingerprint (not full secrets), tokens, model, latency, $ |
| Shadow runner | Parallel cheaper models; never block success path on shadow failure |
| Quality gate | Job-specific scorer; fail closed (stay expensive if unsure) |
| Policy engine | Allowlist of candidate models; max drop tiers; freeze list |
| Dashboard + API | Savings, quality, promote/revert |
| Billing | Flat subscription (Stripe etc.), external to OpenRouter |

### Nice-to-have (v1.5+)

- Classify “needs LLM” vs “replace with code/scrape/rules”
- Propose a non-LLM patch / script and require human approve
- Auto PR into customer repos (high trust; later)
- Share-of-savings billing with attested baselines

---

## Quality (non-negotiable)

If quality silently drops, the product is dead.

**Principles**

1. **Fail closed.** No switch without enough agreeing samples.
2. **Per-cron rubric**, not one global “chat quality” score. A triage digest ≠ a legal risk sweep ≠ JSON schema extraction.
3. **Shadow before switch.** Days of dual-run where possible.
4. **Revert in one click** (and automatic revert if post-switch score tanks).
5. **Never log raw secrets** from prompts (API keys, tokens, PII). Hash or redact.

**Scoring ideas (pick per job class)**

- Exact / fuzzy match on structured fields (JSON schema jobs)
- LLM-as-judge with a fixed rubric vs the expensive model’s answer as reference
- Customer-supplied gold fixtures for critical crons
- Control Tower–style blind score out of 10 (already familiar internally)

**Promotion rule (sketch)**

- ≥ N shadow samples (e.g. 20–50 depending on volume)
- Mean score ≥ primary − ε (e.g. 0.5 on a 10-scale) **and** no catastrophic fails
- Cost materially lower (e.g. ≥ 20% cheaper) or we don’t bother switching

Tune later; document whatever ships.

---

## OpenRouter facts (for implementers)

- One key, many providers; set `model` to `author/slug`.
- Fallbacks / `models` arrays exist; we still want *our* quality-aware routing, not only their cheapest route.
- Plugins array ≠ third-party app store.
- List community apps via Awesome OpenRouter when we have traction.
- Respect ZDR / `data_collection` / provider `only` flags if the customer sends them — pass through, don’t strip privacy constraints.

Docs worth keeping open:

- https://openrouter.ai/docs/guides/features/plugins  
- https://openrouter.ai/providers/apply  
- https://openrouter.ai/docs/guides/community/awesome-openrouter  
- https://openrouter.ai/docs (chat completions + models)

---

## Business model

| Option | When |
| --- | --- |
| **£2/mo (or similar) flat** | v1 default — easy to sell, no metering fights |
| Higher team tier | When fleets are large / support is real |
| ~20% of proven savings | Later; needs trusted baseline + dispute path |
| One-off self-host license | Possible; model tables go stale — not preferred |

Sell **outside** OpenRouter. We are a SaaS that *uses* OpenRouter.

---

## Suggested repo split (what Desktop should do)

**Now (this repo):** Keep the explainer site + this handoff. Do **not** grow a full backend here if it fights the static Vercel site. Small prototype scripts are OK if you want, but prefer a new repo ASAP.

**Next (new repo, name TBD):** e.g. `cheaper-crons` / `cron-router` / product name.

Suggested first milestones in the **new** repo:

1. **Skeleton proxy** — Node or Python; OpenAI-compatible `/v1/chat/completions`; forward to OpenRouter; env `OPENROUTER_API_KEY` or incoming `Authorization`.
2. **Request tagging** — `X-Job-Id` / `X-Cron-Id` required (or derived).
3. **SQLite/Postgres log** — one row per request + shadow.
4. **Shadow compare** — config map `job_id → [candidate models]`; score with a dumb metric first (JSON validity / key presence), then judge model.
5. **Manual promote** — API/UI to set `job_id → model` override.
6. **Auto promote** — gate from above.
7. **Minimal dashboard** — table of jobs, $, quality, buttons.
8. **Dogfood** — point 1–3 internal Control Tower / platform crons at it.

---

## Dogfood / internal context

Related work already lives in **Control Tower** (`HughArcher2005/Control-Tower`):

- Cron model ratings / costs / balance pages under `public/cron-model-*.html`
- Recent commits around scoring Astra / Sol / Luna vs cost

Use that as the first customer narrative and as a source of real cron names, costs, and quality scores — not as a hard dependency for the new product’s architecture.

Skillify’s live LLM path (OpenRouter + ZDR + Opus, etc.) is documented on the **The choice for Skillify** tab of this site. That path is privacy-sensitive; don’t casually route Skillify production through a half-built proxy.

---

## Naming

Product name is still open. Working titles: “Cheaper crons”, “Cron cost router”, etc. Don’t block engineering on branding.

---

## Open questions (decide while building)

1. Product name and new repo name  
2. Hosted-only vs allow self-host in v1  
3. BYOK only vs we also hold OpenRouter keys  
4. How strict the gate is for finance-shaped / legal-shaped crons  
5. Whether non-LLM rewrites are in MVP or explicitly later  
6. Whether Desktop starts coding in a **new empty repo** today (recommended) vs prototyping under this folder  

---

## Conversation decisions already made

- OpenRouter = one key, cross-lab model switch — confirmed.  
- Cannot sell as an OpenRouter plugin — confirmed.  
- Billing external; prefer low monthly fee over 20% savings for v1 — confirmed.  
- Public write-up lives on this site’s **Cheaper crons** tab — shipped.  
- Full plan for implementers = **this handoff** — you are reading it.  
- Actual product code → **new repo** (user intent); this repo stays the site + brief for now.

---

## Immediate next step for Cursor Desktop

1. Read this file and the **Cheaper crons** tab on the live site.  
2. Create a **new GitHub repo** for the product.  
3. Scaffold the OpenAI-compatible proxy + request log + one shadow path.  
4. Dogfood against one low-risk cron with a clear structured output.  
5. Only then wire auto-promote and billing.

If scope gets messy or multi-agent, Hermes-style packaging may help later; for a greenfield proxy, a single Cursor Desktop thread on the new repo is enough.
