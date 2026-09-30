# Starter prompt

The opening prompt given to each model. Replace `<model>` in the two filenames with the model's
short name before pasting, so each run writes to its own files: `-claude` for the first run,
`-openai` for the second. Everything else stays word for word, which is what makes the two runs
comparable.

```
I want to build a restaurant ordering and status platform. Customers that are in the restaurant are able to see the menu by scanning a QR code. The servers are able to take in the customers orders and see the statuses of the items and the order. The kitchen staff receive the orders. There is also an admin view to manage the menu. 

Act as a product manager for this product and write a draft product vision statement. Before you write it, ask me any questions you need answered about scope, because I have deliberately not decided everything yet. Save the vision to restaurant-ordering/vision/vision-statement-<model>.md.

Keep a log of our session as we go. After every reply you give me, including this one, append an entry to restaurant-ordering/prompt-logs/prompt-log-<model>.md, creating the file if it does not exist. Each entry needs the date and time, my prompt copied verbatim and unedited, which model and version you are, and a short factual summary of what you produced.
```
