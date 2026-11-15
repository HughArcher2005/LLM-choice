# Cloud handoff

15 November 2026. Read this first. The desktop chat could not move to Cloud. This agent is the new one. The repo is `HughArcher2005/LLM-choice` on `main`.

## What this work is

Hugh is editing the Skillify Qwen so its answers sound like a portfolio manager, and less like a computer science graduate talking about finance. The concrete failure is the investment memo. The API writes one. It is bad. Gary and Niall edit it by hand before it goes to the user.

No training. No gradients. Astra edits a small slice of a copy of the weights. The morning file on the H100 stays as it is.

## Read these files

- `weight-space-plan.md` is the living plan. Add to it when a decision changes.
- `questions.md` and `questions.docx` are the 50 exam questions. Astra does not see them.
- `astra-handoff.md` is the prompt for the weight edit.
- `IDEAS.md` is the longer background.

## Where it stopped

The 50 questions are written and pushed. Each one is one paragraph, under 80 words. It asks for the market narrative and the trades. A single trade is enough. It has to be an asset-management decision taken from the Skillify heuristics.

The 50 API calls have not been sent. They go to `POST /api/decision-overlay` with `model.lane` set to `qwen3_8_27b`. A call without that lane uses the frontier model. The H100 has to be on. It is on for the morning books, then it is turned off. Do not turn it off with a plain stop. Do not overwrite `/usr/local/lib/qwen/qwen3.8-27b`.

Gary and Niall do not answer these 50. Their already-edited memos are the practice set Astra may see. The prompt in `astra-handoff.md` says to keep a weight change only if the practice books sound more like those edits.

## The eight steps

1. Fifty Skillify API calls on Qwen, before the edit. Record the answers.
2. Examples file: edited memos, transcripts, articles. Not the 50.
3. Astra edits a copy, using `astra-handoff.md`.
4. The same 50 calls after the edit, with the server pointed at the copy, then pointed back.
5. Shuffle the 100 answers. Keep the key in a separate file.
6. Gary, Niall, and a couple of models rank them blind.
7. Match the ranks to the key.
8. Analysis. That waits for the results.

## Who does what

Hugh leads the weight edit. Gary owns benchmarks and wants to drop into this agent from his phone. Niall edits memos with Gary. Ilyas owns the news fine-tune. That pilot is not this job. LeanCron is a separate project.

Gary uses Sol for real work. Grok is for small tasks. That rule is not in this repo yet.
