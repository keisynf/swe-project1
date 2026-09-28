# Prompt Log — OpenAI

## 2026-09-25 11:32:57 CST

**User prompt (verbatim):**

```text
I want to build a restaurant ordering and status platform. Customers that are in the restaurant are able to see the menu by scanning a QR code. The servers are able to take in the customers orders and see the
   statuses of the items and the order. The kitchen staff receive the orders. There is also an admin view to manage the menu.

   Act as a product manager for this product and write a draft product vision statement. Before you write it, ask me any questions you need answered about scope, because I have deliberately not decided everything
   yet. Save the vision to restaurant-ordering/vision/vision-statement-openai.md.

   Keep a log of our session as we go. After every reply you give me, including this one, append an entry to restaurant-ordering/prompt-logs/prompt-log-openai.md, creating the file if it does not exist. Each
   entry needs the date and time, my prompt copied verbatim and unedited, which model and version you are, and a short factual summary of what you produced.
```

**Model:** gpt-5.6-terra

**Summary:** Identified the key unresolved product-scope decisions and asked focused questions before drafting the product vision.

## 2026-09-25 11:33:27 CST

**User prompt (verbatim):**

```text
I want to build a restaurant ordering and status platform. Customers that are in the restaurant are able to see the menu by scanning a QR code. The servers are able to take in the customers orders and see the
   statuses of the items and the order. The kitchen staff receive the orders. There is also an admin view to manage the menu.

   Act as a product manager for this product and write a draft product vision statement. Before you write it, ask me any questions you need answered about scope, because I have deliberately not decided everything
   yet. Save the vision to restaurant-ordering/vision/vision-statement-openai.md.

   Keep a log of our session as we go. After every reply you give me, including this one, append an entry to restaurant-ordering/prompt-logs/prompt-log-openai.md, creating the file if it does not exist. Each
   entry needs the date and time, my prompt copied verbatim and unedited, which model and version you are, and a short factual summary of what you produced.
```

**Model:** gpt-5.6-terra

**Summary:** Asked focused questions about the product’s target restaurant type, customer ordering rights, operating model, integration boundaries, and success measures before drafting the vision.

## 2026-09-25 11:43:55 CST

**User prompt (verbatim):**

```text
1. just one casual restaurant. 2. they should only view the QR menu 3. yes, the servers should be the one creating the orders not the guests 4. yes, the orders should have an status of placed and an status of ready when they are done, they could also be canceld/rejected. 5. the menu should also have availability of the item, some modifiers, categories. 6. standalone, with no integration to a POS, payment processor, inventory system, or third-party kitchen-display system. 7. one shared and accurate view of what is actually happening with every order.
```

**Model:** gpt-5.6-terra

**Summary:** Created the draft product vision, including the agreed single-restaurant scope, role-specific workflows, menu-management scope, order statuses, initial exclusions, and intended outcome.

## 2026-09-28 09:19:13 CST

**User prompt (verbatim):**

```text
there should be no distinction of QRs per table. for the statuses, do you think those are enough? and also I want the product to have some kind of bill, even if it does not handle payment processing.
```

**Model:** gpt-5.6-terra

**Summary:** Confirmed that QR codes should not identify tables, recommended a clearer item and order status model, and asked focused questions about the bill’s audience and contents before revising the vision.

## 2026-09-28 09:29:04 CST

**User prompt (verbatim):**

```text
we should also have an status indicating that the item and order have been delivered to the customer
```

**Model:** gpt-5.6-terra

**Summary:** Incorporated delivered as a post-ready status in the recommended item and order workflows, while preserving the remaining bill-scope questions needed before revising the vision.

## 2026-09-28 09:35:58 CST

**User prompt (verbatim):**

```text
only servers see and generate the bill, the items already inlcude the taxes, no tip, and show the total
```

**Model:** gpt-5.6-terra

**Summary:** Revised the product vision to specify server-only bill generation, tax-inclusive item prices, no tip suggestions, and a displayed total. The revision also incorporates generic non-table QR codes and delivered status for items and orders.

## 2026-09-28 10:34:28 CST

**User prompt (verbatim):**

```text
Your conversational replies had decisions that did not make it into the revised vision. Restore them:

   1. The `closed` order status, with your own reasoning that it separates food service completion from bill completion.
   Say what closes an order.
   2. Your derivation rule, that an order is `ready` only once every non-canceled item is ready, in place of "the order
   status gives a summary of its items." Give the equivalent rule for each order status.
   3. Who owns each transition. You said the kitchen rejects an item it cannot fulfill and the server cancels it. Put that
   in the document, and cover the other transitions too.

   Also, use one term for the kitchen-working state. Items say `preparing` and orders say `in progress`.
```

**Model:** gpt-5.6-terra

**Summary:** Revised the vision to restore the closed order status and its billing-completion rationale, define every order-status rule, state transition ownership for each item state, and use preparing as the kitchen-working term for both items and orders.

## 2026-09-28 17:20:43 CST

**User prompt (verbatim):**

```text
Revise thoroghly the derivation table, there are some ordinary cases where it breaks. For example: drinks are delivered and the mains are ready. ready requires every fulfillable item to be ready, and a delivered item isn't. preparing matches because at least one item is ready. So the order shows preparing even though the kitchen has finished everything. This is probably the most common state a table is in.
```

**Model:** gpt-5.6-terra

**Summary:** Reworked the order-status derivation table into mutually exclusive, precedence-ordered rules. The ready rule now treats ready and delivered items as kitchen-complete, so delivered drinks with ready mains show ready; mixed active states remain preparing only when outstanding kitchen or delivery work exists.
