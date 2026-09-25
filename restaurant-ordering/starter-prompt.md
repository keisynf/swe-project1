# Starter prompt: OpenAI run

The same opening prompt used for the first model, word for word, with only the two filenames
changed so this run writes to its own files. Keeping the prompt identical is the point: it is
what makes the two runs comparable.

Paste as the first message.

---

```
I want to build a restaurant ordering and status platform. Customers that are in the restaurant are able to see the menu by scanning a QR code. The servers are able to take in the customers orders and see the statuses of the items and the order. The kitchen staff receive the orders. There is also an admin view to manage the menu. 

Act as a product manager for this product and write a draft product vision statement. Before you write it, ask me any questions you need answered about scope, because I have deliberately not decided everything yet. Save the vision to restaurant-ordering/vision/vision-statement-openai.md.

Keep a log of our session as we go. After every reply you give me, including this one, append an entry to restaurant-ordering/prompt-logs/prompt-log-openai.md, creating the file if it does not exist. Each entry needs the date and time, my prompt copied verbatim and unedited, which model and version you are, and a short factual summary of what you produced.
```

---

## Notes for running this

This directory is a separate git worktree on the branch `openai-restaurant`, checked out from
before the first model's work existed. Nothing that model produced is present here, so this
session cannot read its vision, personas, scenarios, or 1-pagers.

Answer its scope questions consistently with the decisions already made, otherwise the two runs
describe different products and the comparison says nothing. Its questions will not match the
first model's, so expect to map the same answers onto different questions, and note in the log
where the questions differed, since that is itself a finding.

Later deliverables follow the same naming: `personas/personas-openai.md`,
`one-pagers/<epic>-openai.md`, and drafts under `drafts/`.

`one-pager-template.md` is the required 1-pager format, copied verbatim from the project README.
