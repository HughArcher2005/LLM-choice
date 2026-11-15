# New ideas

23 October 2026. From Hugh’s notes.

## The cut line

Skillify is everything that happens before a Skillify API output.

Mandate is everything that happens after a Skillify API output.

## Mandate right now

Mandate is the paper trading engine. An improvement to paper trading is a Mandate project.

## Product one: cheaper crons

Build this first. The test key lives in `leancron/.env`.

Leancron is an API key. A cron uses it where the OpenRouter key sat, and the calls get cheaper. Behind that key, the AI reads the workflow and names which of the seven lanes applies. The buyer pays for that AI and for the tokens.

Sell it, or open source it and promote Skillify. That choice waits until we see whether people will pay. The seven lanes stay as written in `HANDOFF.md`.

### What we keep

Looked at 23 October 2026.

- [TokenTrimmer](https://github.com/TokenTrimmer/tokentrimmer) Inspect and Plan. Scan the workflows, name the waste, and replay what the cheaper lane would have cost before a switch. Our scan assigns one of the seven lanes.
- [TokenMiser](https://github.com/openintelligence-labs/tokenmiser). An OpenAI-compatible connector, an exact cache, a cost ledger, and a shadow judge that switches only when the score holds.
- [RouteLLM](https://github.com/lm-sys/RouteLLM/). A confidence threshold: an easy call goes cheap, an unsure call stays on the expensive model. For a label, that number is Jev’s probability.
- [GPTCache](https://github.com/zilliztech/GPTCache/). An unchanged input returns the last answer. That is the skip lane. A near-match still has to pass the rubric.
- [LLMLingua](https://github.com/microsoft/LLMLingua/). A cousin of the shorter-prompt lane. In v1 the shorter prompt is written, such as the headline and the new yield.

The connector talks to OpenRouter. The product is the scan plus the seven lanes.

### Build order

The code goes in a new repo. This repo stays the explainer and these notes.

1. Scan one real cron workflow and name its lane.
2. Connector: OpenAI-compatible base URL, cron id, log, the OpenRouter key.
3. Skip an unchanged input. Then the shorter prompt.
4. Shadow a cheaper model. Switch only when the score holds.
5. Jev on one hike-or-cut cron. An unsure call goes to the expensive model.

## Idea two: source the GPU

We need an open-source model. Test it on a rented GPU. Buying a card comes after that test.

The buy is distressed GPU. A business that needs cash will sell cards cheap to pay debt. Example only: if a large owner such as CoreWeave had to sell in a hurry. Buy that stock, then use it or sell it on.

Reselling that GPU can be its own business. Scrap counts. Pull chips from old laptops, monitors, and printers, stack what still runs, and see what the pile can do.

Data-centre cards and chips from old machines are two piles. Both get tested, then used or sold.

Enough working GPU becomes a mini data centre. Sell the compute, or run our own models on it.

## Own hardware, if we switch

2 November 2026. Hugh’s note, after Gary said to stay on OVH because data leaks every other way. This is the layout if Skillify moves onto machines we own. The other path in that note is to encrypt what we already have.

The machines are €99,450 to €102,150 up front. Hugh marked that range as 95%.

| Item | Low | High |
| --- | --- | --- |
| One server with two H100 cards already in it | €98,000 | €98,000 |
| Two database computers | €1,100 | €3,600 |
| One battery for those two computers | €350 | €550 |
| Power for a year, cards on about 2 hours a day | €900 | €2,000 |
| First year, cards on about 2 hours a day | €100,350 | €104,150 |
| Power for a year if the cards are left on all day | €2,500 | €4,000 |
| First year if the cards are left on all day | €101,950 | €106,150 |

Bills that stop if those machines take the work:

| Bill you stop | Low per year | High per year |
| --- | --- | --- |
| Supabase | $0 | $0 |
| OpenRouter | €1,470 + $680 | €3,100 |
| Amazon Web Services | €750 + $3,900 | €12,300 |
| Google | $0 | $0 |
| Anthropic | €1,550 | €1,660 |
| xAI | €270 | €1,040 |
| The OVH plan you would not start | €1,000 | €2,000 |
| Total, same euro rate | €9,100 | €18,800 |

Each year, power of €900 to €2,000 comes off the €9,123 to €18,766 we stop paying. That leaves €7,123 to €17,866. In short: about €100,000 up front, Skillify runs better than it does now, the data stays on our machines, and about €7,000 to €18,000 a year stays in hand.

At a 4% discount rate, €100,000 comes back in 21.6 years on the €7,000 saving, and in 6.4 years on the €18,000 saving. The hardware is an asset. That payback gives it no rise in value. The saving also leaves out inflation in model costs, AWS, OVH, and OpenRouter.

That layout is the left column, up to €300,000. We did not take it.

## What we switched to

9 November 2026. The right column, under €5,000. The card is a confidential H100 on Azure. The database is encrypted. The key stays with us. The table is the earlier plan for that column. The live morning run is in "Where it stands."

| Leak | What we do | Cost |
| --- | --- | --- |
| Supabase can read the skills | Encrypt the skills. The key stays with us. | €0 |
| The API runs on someone else's server | Run it on the computer we already have. | €0 |
| OpenRouter sees the prompt | Stop using it. Rent one confidential H100 on Azure for the run, then turn it off. | About $270 to $540 a month. One hour a day stays under €5,000 for a year. |
| Bedrock or Google sees the prompt | Same confidential card. | No second bill. |
| A failed call goes to xAI | A second confidential H100 stays off. Start it only when the first call fails, then turn it off. If that copy also fails, stop. | One failed day is about an hour at $7. |
| OVH can read the disk | Do not use OVH. The Azure rental above is that disk. | Already in the rental. |
| The 600,000 words are uploaded to train | One confidential H100 for that train, then delete it. | A few hours, under €100. |

The left column was two office servers, so one can die, and an office H100 at €20,000 to €25,000 plus a second card for a failed call. That pair is the own-hardware layout above.

## Where it stands

9 November 2026. The rest of Hugh and Gary’s exchange, then Gary’s notes after a catchup with Ilyas.

### The cards are on

Gary confirmed the Azure confidential H100s are working. The first job is the Mandate decision API. It runs two hours every morning, and it serves only us. That is €15 a day, €3,800 a year. It is serving. It is not training, and it is not a fine-tune.

Hugh’s earlier year included every bill we pay, and the OVH plan we were not going to start. This morning run is only the decision API, so it is cheaper than that sheet. Moving onto our own machines is what cuts the rest of those bills. Gary agreed that office layout is still the hardware to work towards. On it, a 27 billion parameter model can be trained, a 70 billion parameter model can be run, and a 70 billion train can be a one-day rental. Electricity on that layout is about 1,000 a year. The other subscriptions, including OpenRouter, come off.

Mandate is also set to run two sets of requests at once: one Grok, one self-hosted Qwen.

### Training is a different machine

This morning card does not train. A train would be another Azure spin-up with more H100s. Gary’s first figure is 8 H100s, 1,500 every 24 hours, and about 10k for a train. He did not name the currency. Hugh’s view is that 8 cards is more than a 27 billion parameter model needs, and that a model that size can train in a couple of hours. They left the number for later, and the next step is smaller.

Hugh’s first use of a train, when it comes, is the Skillify API: sound better, and decide better from the transcripts. His view is that 600,000 words is enough for that first pass, if we have them.

### Weight space programming comes first

No training. A frontier model rewrites the weights, and that run is the baseline. Gary said Astra was the best of the models someone had already tried. A new round from OpenAI and Anthropic was expected the week of that exchange. If the method holds, the model in use can update from that use, and a full train matters less. Each person ends with a model shaped by their own use.

Hugh leads this work and applies it to the scheduled jobs. LeanCron is that job: daily answers from a frontier model, then a 7 billion parameter model. On the public page the Qwen 2.5 7B weights are still fixed. This is the next step, not a claim that those weights have already moved.

Ilyas, 9 November: stay with the 27B already running. A 1B can beat a large general model on a small closed task, such as tagging an entity. This job is a long set of skill cards in, and one valid trading book out. A 1B is weak at that, and news training would pull it further off. News training only nudges the 27B toward macro language. The trading judgment stays in the skill cards. One GPU already fits the 27B, and the product path is built for it. A 1B would be a separate system. Gary agreed. Ilyas has moved the data from S3 to Azure and expects to start the pilot within one or two days.

LeanCron is a separate project. Hugh’s week is Skillify. The 27B already running reads the skill cards and returns one valid trading book. The news pilot stays with Ilyas. It only nudges the 27B toward macro language. The trading judgment stays in the skill cards.

### What to hand Astra

10 November 2026. The method Gary named is the one in Takehi, Teoh, Zhang, and Khattab, MIT CSAIL, 2 November 2026: [Sparks of Weight-Space Programming](https://rikiyat.github.io/blog/weight-space-programming/). A later check of the same harness is [arXiv:2611.09382](https://arxiv.org/abs/2611.09382).

Astra does not receive the weights as a paste once the model is large. It receives a Python session with the weights loaded, and a separate worker that runs the model. The blog’s Qwen run used the training splits of GSM8K and MATH, never the test, and a budget of forward passes. The score moved at 50 passes, not at 10 or 25. One pass was the model answering up to 512 problems, or reading up to 1,024 texts. Gradients and training were banned. The later paper allows 50 successful forward requests and up to 300 Python analyses. Edits stay inside the transformer blocks. The embeddings, the final norm, the language-model head, and the architecture stay fixed.

The edit that moved the score subtracted one direction from 64 columns of `mlp.down_proj` in layers 15 and 19 of Qwen3.5-0.8B. That is 131,072 weights, 0.016% of the model. With thinking on, MATH-500 went from 7.9% to 48.1%, and the share of answers that hit the token limit fell from 93% to 33%. With thinking off, an independent run put the unedited model near 44% to 46% and the edited model near 43% to 44%. The edit removes a loop. On Gemma 3 270M, which rarely loops, the same ask moved MATH-500 from 6.8% to at most 7.7%. The authors’ line is that the edit can take away a fault that hides an ability, and it cannot add an ability the model lacks.

The follow-up ran 16 searches on Qwen3.5-0.8B and Qwen3.5-9B. Six searches kept the original weights. On the 9B, one math search gained about 30 points on the practice set and lost 0.35 points on the held-out test. The smaller model had more room to move. A model that is already strong is a harder edit. No published run uses a 27B.

Two older methods take a different packet. ROME and MEMIT take one fact, as a prompt, a subject, and a new object, and write a rank-one update. Text-to-LoRA, Sakana, is a hypernetwork trained to turn a task sentence into a LoRA. Astra in the MIT post is used as it is. It is not that hypernetwork.

The aim Hugh and Gary set is the voice. Skillify should sound like a portfolio manager, and less like a computer science graduate talking about finance.

12 November 2026. Gary: the API writes an investment memo, and the memo is bad. He and Niall edit it by hand, then send the edited memo to the user. Those pairs are the examples Astra may see while it edits: the memo Qwen wrote, and the memo they wanted. Gary and Niall will write a set of desired outputs. Hugh writes the Astra prompt on the weekend. The sealed 50 questions stay a different set. Astra does not see them.

The same 50 questions run before the edit and after it. The 100 answers are shuffled. Two blind scores, each without being told which answer is which. One score is a model. One score is Gary. Hugh holds the key and matches the scores back. Gary also named Finance 101 as the questions. That choice is still open. The failure he named is the investment memo.

15 November 2026. Hugh’s first prompt is the 50 questions themselves. Each one is a short scenario, one paragraph, and it asks for the market narrative and the trades. Portfolio construction, not a textbook definition. Simple enough that Gary can rank the answers, and open enough that the book is not obvious. The questions are drawn from the skills and heuristics already in the Skillify repo, and from what people said in the transcripts. The same 50 go to Qwen before the edit and after it. Astra does not see them. Hugh expects three prompts in all. The other two are not set.

The order is the eight steps Hugh wrote down. Steps 1 and 4 wait until the 50 questions exist. Step 1 is 50 calls on Qwen before the edit. Step 4 is the same 50 after the edit.

Steps 2 and 3 are one local file. It holds examples of how Qwen should talk, and a handoff prompt. Astra reads financial articles, and transcripts from Gary and other portfolio managers. The prompt then says what Astra is to do to the weights.

Step 5 is a prompt to Cursor. Shuffle the 100 answers, label them, and keep the unshuffled key in a separate file. Step 6 gives the shuffled file to Gary, Niall, and a couple of models. Each ranks blind. Step 7 brings those ranks back to Cursor, which matches them to the key before anyone reads the result. Step 8 is which side gave the better answers.

### Kimi

Kimi K3.1 Pro weights became public the week of that exchange. About 1 trillion parameters. Gary asked what it would cost to serve that model ourselves, as the OpenClaw strategy model and the Cursor coding model. He was talking about serving a model that already exists. A pretrain figure of about $100 million was Hugh citing another model, and Gary set that aside. A smaller model of our own, shaped for this work, is the long project.

### After Ilyas

Expert words. The set is 200,000 words from 16 people. WhatsApp voice notes add about 5,000 words a week. The target is 10 million to 15 million words, and that takes 3 to 6 months. Three people are building the collection line.

Macro. The article repository cost $10,000 to $15,000. The macro text is about 500 million words, about a tenth of a 5 billion word archive. The train is LoRA on Qwen, so most weights stay frozen. Frontier models still miss finance words in a trade discussion.

Infrastructure. The training pipeline is expected on Azure, because the data is encrypted. Serving a 27 billion parameter model is assumed to be one H100. Ilyas designs that pipeline, moves the data from AWS to Azure, and prices it.

Owners. Benchmarks for the macro model: Gary. Weight space programming: Hugh. Fine-tuning infrastructure: Ilyas.

### The outage was not LeanCron

LeanCron’s five-answer job called Grok, Opus, Astra, and Qwen from this PC through their own APIs. It did not start OpenClaw, take the gateway lock, or change weights. Gary later saw the failure continue and said it was not that job. The failure he described was the Control Tower watchdog running `openclaw status` inside the gateway and taking the state lock. He also asked whether a direct API replay is a fair stand-in for an OpenClaw cron that uses OpenClaw memory. That question is still open.

## Idea three: our open-source model, tested by paper trading

Build this soon. It sits after a Skillify API output, so it is Mandate.

Eight separate books, tracked for a few months:

1. OpenAI, no Skillify.
2. OpenAI, with Skillify.
3. Anthropic, no Skillify.
4. Anthropic, with Skillify.
5. Grok, no Skillify.
6. Grok, with Skillify.
7. Our open-source model on our own GPU, no Skillify.
8. Our open-source model on our own GPU, with Skillify.

Each book needs its own cash, positions, and fills. End-of-day prices are not enough. Fills, commissions, fees, and the spread have to come from actual quotes and orders.

IBKR attaches one paper account to a live account. That account reports commissions, and it fills from the top of the book. It has no deep book, and it skips some order types, including VWAP, auction, RFQ, and pegged-to-market. Eight models in that one account would net into a single book, so it cannot host this test. Use one IBKR paper account as the check on a single book.

For the eight books, use a simulator with a separate ledger each, an IBKR-style commission schedule, and fills off the live bid and ask. QuantConnect can run one project per book. Its default paper model charges $0.005 per share with a $1 minimum, and it uses the spread when it has the quote. Its default slippage is zero, and a market order fills immediately and in full. Confirm the live-node price before paying for eight nodes. Alpaca paper is free and fills off real-time quotes. Equity commission there is zero, and it skips regulatory fees, queue position, and market impact.

### Training data

We have 10 to 20 experts. Each interview is 45 minutes to an hour. At a normal speaking pace that is about 60,000 to 190,000 words. The count after Ilyas is in "Where it stands": 200,000 words from 16 people, and about 5,000 more a week.

That is enough to fine-tune an existing open model as a pilot. It is far too small to train a base model. A base model needs billions of words. Thousands of transcripts is the scale where the fine-tune can carry trading skill. One thousand hour-long interviews is on the order of 8 to 10 million words.

The heuristics already pulled out of these interviews are the part to train on first. A raw transcript mostly teaches phrasing.

Peer-reviewed financial, economic, and quantitative trading papers add breadth to that same fine-tune. A paper is often 5,000 to 12,000 words. Hundreds of them are a few million words. Train only on papers we have the right to use.

## What we will build

26 October 2026. Talk this through, then build it. It is Mandate. The eight books above stay the scoreboard. This is the signal those books can trade.

### Where it came from

The spark was a pile of earnings history. Take a company that has reported four times a year for about fifty years. That is about two hundred reports. Add the option prices, the macro conditions, the filings from before the report, the earlier earnings, and the path into the call. A model trained on that pile might beat a coin flip on the next earnings, and the gap might be alpha.

Two hundred reports on one company is too small a pile. The published version of the same hope pools every industrial firm. Cao and You, Financial Analysts Journal, April 2024, did that with accounting numbers only, and the hedge still paid. Their draft is dated 20 January 2021. The sample stops in fiscal 2019. Calls, news, options, futures, and macro stayed outside that training set. The six models below are those left-out piles, each with its own training, plus the filings model they did build.

A single model that swallows all of the piles at once, and still shows a published alpha, is still open. Gu, Kelly, and Xiu in 2020 came closest on numbers: trees and neural nets, about 94 stock traits plus eight macro series, about 30,000 stocks from 1957 to 2016. Momentum, liquidity, and volatility did the work. Funds stack feeds in private and publish no combined number. Averaging separate forecasts has a long record of beating the best single model, and Cao and You’s own mix of accounting models beat each model alone. So the build is one model per feed, then a vote. The list can grow. A feed joins when its own book has a hit rate and a positive alpha. Price and volume, analyst revisions, insider filings, and short interest are the next candidates. Price and volume are already the traits that carried Gu, Kelly, and Xiu.

### The trade

Rank the stocks into five groups. Own the best group and sell the worst group. That hedge is the whole strategy.

Cao and You, Financial Analysts Journal, April 2024, measured that hedge. The draft is dated 20 January 2021. The sample stops in fiscal 2019. One run paid 34 basis points a month. Another paid 77. Those are two sizings of the same hedge, after the usual stock-market risks and before trading costs. Equal weight, where every stock has the same say, is the generous end, and small stocks carry it. Value weight, where big companies have more say, is the strict end. A real book picks one sizing and receives one of those monthly results. A year of the strict gap is about 4%. A year of the generous gap is about 9%.

The models are a random forest, gradient boosting, and a small neural net on accounting lines. A newer chat model leaves that result standing. Positive alpha after 2019, and after the spread and the stock borrow, is still unproven. That is the test.

### Six models, scored alone, then combined

One model for SEC filings, in the Cao and You shape. One for calls. One for news. One for options. One for futures. One for macro. Six models. Each is trained on its own history, back as far as that history is clean.

Each model first runs its own book. Record the hit rate when it says long, the hit rate when it says short, and the alpha after the spread and the borrow. A model with no alpha on its own does not get a vote.

Then build a correlation matrix of the six scores. High correlation means two feeds are the same fact. Three feeds that repeat one earnings release will count as three votes if we skip this step.

Then try combinations, not only the full equal vote. One combination to test: calls, options, and futures, and only take the trade when those three agree. They sit on the short clock, around the earnings week and the days after. That agreement might be the book with the most alpha. It is a hypothesis. The matrix and the three-agree book are how we check it.

Other clocks stay in their own combinations. Filings vote for the quarter. Macro votes for months. News votes for days. Chicago news models predict a few days of return. A feed that has gone quiet, as options did after 2008, keeps its seat only while its own recent score holds.

### How much data each one trains on

Filings. The published set is about 140,000 firm-years and 56 numbers, a rolling ten-year window, tested from 1975 through fiscal 2019. Sharadar’s full history, from the late 1990s, is $69 a month on the personal plan, fundamentals and prices together. SEC filings are free. Clean XBRL numbers start in 2009. The text of the filings is a later reader, not this first hedge.

Calls. RavenPack dates a structured transcript archive from 2003, across more than 20,000 listed companies and seven kinds of call. The first test is the S&P 500 from 2010, the window of the 2023 call paper. That is a few tens of thousands of calls.

News. The RavenPack Dow Jones edition runs from 2000. On WRDS, as of 9 October 2026, that edition is about 361 GB. The model trains on a daily score per stock. It does not train on the raw archive.

Options. IvyDB US is every listed US option, every day, since January 1996, on more than 10,000 underlyings. The model trains on one row per stock per day: skew, spread, volume, open interest. The raw quote file is the large one, and it is an institutional license. A 2024 Robeco paper found the monthly return signal faded after 2008 once a timing bias was removed. The own-book test has to clear that.

Futures. Daily bars on the main index, rate, and commodity contracts go back to the 1980s. A handful of contracts over a few decades is on the order of a hundred thousand rows. That file is small. Tick history is a different purchase, and it waits until the daily book shows a hit rate.

Macro. Eight monthly series from Welch and Goyal, the set Gu, Kelly, and Xiu used. By itself that is a few hundred months, which is too short for a model of its own. Macro enters as a condition on the stock panel. The panel in that paper is about 30,000 stocks from 1957 to 2016.

### What Cao and You actually trained on

More statement lines helped. They stopped at 56 figures: the level and the yearly change of 28 accounts. Each forecast used only the prior ten years. They kept ordinary shares on the NYSE, Amex, and Nasdaq, priced above $1, and dropped banks and utilities. About 140,000 firm-years. Calls, news, options, and macro stayed outside. Current earnings carried most of the weight.

### Cost of the first model

The accounting model trains on a laptop. Sharadar’s full history is $69 a month on the personal plan, fundamentals and prices together. SEC filings from 2009 are free.

A rented GPU is the later filing-reader, not this hedge. One 4090 is $0.34 an hour. An evening on Qwen 3.8 27B is a few dollars. DeepSeek and Kimi at the size that leads the filing benchmarks need a pile of cards. We rent before we buy, as in idea two.

### Order of work

1. The filings hedge, one sizing, walk-forward, years after 2019. Long hit rate, short hit rate, alpha after the spread and the borrow.
2. The same card for calls, news, options, futures, and macro, each on its own book, as the file for that feed is in hand.
3. The correlation matrix of whatever has a score.
4. Combinations. The six-vote book. The three-agree book of calls, options, and futures. Any other cluster the matrix suggests.
5. A filing-reader on a rented GPU only as an extra filings vote, on the day of the filing.
