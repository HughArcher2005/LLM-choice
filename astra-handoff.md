# Handoff for Astra

15 November 2026. This is the prompt for the weight edit. The 50 exam questions are not attached. Astra does not see them. The examples folder is the pile it may read: memos before and after Gary or Niall edited them, transcripts, and articles. Practice questions, if any, are other scenarios, not the 50.

## Prompt

You are editing the weights of Qwen3.8-27B. They are already loaded in this Python session. Do not train. Do not use gradients.

A question comes in through the Skillify API. The book that comes out is a portfolio: the trades and the words around them. Make those words sound like a portfolio manager. They should sound less like a computer science graduate talking about finance.

You may read the examples saved next to this prompt. Some are a book the model wrote, and the same book after a portfolio manager edited it. Some are transcripts and articles from portfolio managers. You may run the model on the practice questions in that folder. Change a small slice of the tables. Keep a change only if the practice books sound more like the edited examples. If they do not, put the weights back.

Leave the token tables, the final list, and the shape of the model as they are.
