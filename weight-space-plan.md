# Weight space plan

15 November 2026. This is the living plan. Add to this file as Hugh talks.

The aim is the voice. Skillify should sound like a portfolio manager, and less like a computer science graduate talking about finance. The failure Gary named is the investment memo: the API writes one, it is bad, and Gary and Niall edit it by hand before it goes to the user.

No training. Astra edits a copy of the Qwen weights. The morning file stays as it is. The 50 calls need the Azure computer on. The edit happens after that window, with the server stopped.

## Before the eight steps

Make the 50 questions. Each one is a short scenario, one paragraph. It asks for the market narrative and the trades. Portfolio construction, not a textbook definition. Simple enough that Gary and Niall can rank the answers, and open enough that the book is not obvious.

Example shape: the rate of GDP growth is increasing, and so is inflation. What is the current market narrative, and what trades would you take?

Draw the 50 from the skills and heuristics in the Skillify repo, and from what people said in the transcripts. The same 50 go to Qwen before the edit and after it. Astra does not see them.

15 November 2026. The Supabase key is in `C:\Users\user\Skillify\.env`, not in the Skillify API repo. That key opens a live database. The skill text there is plain text, with no cipher. Every schema was checked. The tables are market and trade tables. There is no skills table and no heuristics table. The 47 trade rows have skill-response columns, and those are empty. The routed skill cards live in the API code. The interview heuristics are stored in `Skillify API/data/heuristic-library-seed.json` and the other `data/*-inspect-v*-library.json` files. The local sqlite at `.skillify/heuristic-library.sqlite` is empty until the server seeds it. The routed decision skills are the card files in `lib/capability-registry`.

Hugh expects three prompts. The first is these 50 questions. The second is the examples file and the handoff, in steps 2 and 3. The third is not set.

Gary also named Finance 101 as the questions. Hugh's scenarios are the set being written.

15 November 2026. The draft of the 50 is in `questions.md`. Each one is a single paragraph under 80 words. They ask for the market narrative and the trades. They cover FX and macro, FX options, equities and a commodity, convertibles, funding, and the shape of the book. Hugh reviews them before they are used. Astra does not see the file. A single trade is enough. It does not have to be a full allocation. It does have to be an asset-management decision, and it has to come from the Skillify heuristics.

## The eight steps

1. Call the Skillify API 50 times, one question after another, before any weight edit. Each call is `POST /api/decision-overlay` with `model.lane` set to `qwen3_8_27b`, so Qwen is the backend and the skills still run. A call without that lane would hit the frontier model. Record each question and the API answer in one file. This needs the Azure computer on. Do not send the 50 while it is off.

2. Make a local file of examples of how we want Qwen to talk. Astra reads financial articles, and transcripts from Gary and other portfolio managers. Gary and Niall's hand-edited memos are examples of the memo they wanted. This file is the pile Astra may see. It is not the 50. A portfolio manager does not answer the 50. Those stay the exam. The published edits gave Astra practice answers from a different set, and the exam stayed unseen.

3. The handoff prompt is in `astra-handoff.md`. Astra edits a small slice of a copy. No gradients. No training. It keeps a change only if the practice books sound more like the edited examples.

4. Call the Skillify API again with the same 50 questions after the edit, same lane. Ask Gary to point the server at the copy for these calls, then point it back at the original. Record those answers in a second file. The edit is meant to make that API answer sound like a portfolio manager.

5. Prompt Cursor to shuffle the 100 answers, label them, and write the unshuffled key in a separate file.

6. Give the shuffled file to Gary, Niall, and a couple of models. Each ranks blind. None of them is told which answer is before and which is after.

7. Hugh brings the ranks back to Cursor. Cursor matches them to the key.

8. Analysis. This depends on the results.

## How Gary joins

15 November 2026. Gary has switched his own work to Sol. Grok stays for small tasks. He will copy that rule in from another repo when it is settled. It is not in this repo yet.

He wants this chat moved to a cloud agent, and the link sent to him. That is how he drops in while Hugh is away, including from his phone. The word Claude in his note is that cloud move. The conversation goes with the move. The question files, the handoff, and this plan are still only on this PC. Commit them first if he needs the files. He also needs access to this repo.
