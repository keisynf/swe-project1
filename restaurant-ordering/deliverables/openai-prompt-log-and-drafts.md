# Prompt Log and Vision Drafts

**Product:** Restaurant Ordering & Status Platform
**Model:** gpt-5.6-terra
**Students:** Keisy Núñez and Ezequiel Buck
**Course:** CS 3365, Fall 2026, Project 1

---

## Prompt Log

### 2026-09-25 11:33:27 CST

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

### 2026-09-25 11:43:55 CST

**User prompt (verbatim):**

```text
1. just one casual restaurant. 2. they should only view the QR menu 3. yes, the servers should be the one creating the orders not the guests 4. yes, the orders should have an status of placed and an status of ready when they are done, they could also be canceld/rejected. 5. the menu should also have availability of the item, some modifiers, categories. 6. standalone, with no integration to a POS, payment processor, inventory system, or third-party kitchen-display system. 7. one shared and accurate view of what is actually happening with every order.
```

**Model:** gpt-5.6-terra

**Summary:** Created the draft product vision, including the agreed single-restaurant scope, role-specific workflows, menu-management scope, order statuses, initial exclusions, and intended outcome.

### 2026-09-28 09:19:13 CST

**User prompt (verbatim):**

```text
there should be no distinction of QRs per table. for the statuses, do you think those are enough? and also I want the product to have some kind of bill, even if it does not handle payment processing.
```

**Model:** gpt-5.6-terra

**Summary:** Confirmed that QR codes should not identify tables, recommended a clearer item and order status model, and asked focused questions about the bill’s audience and contents before revising the vision.

### 2026-09-28 09:29:04 CST

**User prompt (verbatim):**

```text
we should also have an status indicating that the item and order have been delivered to the customer
```

**Model:** gpt-5.6-terra

**Summary:** Incorporated delivered as a post-ready status in the recommended item and order workflows, while preserving the remaining bill-scope questions needed before revising the vision.

### 2026-09-28 09:35:58 CST

**User prompt (verbatim):**

```text
only servers see and generate the bill, the items already inlcude the taxes, no tip, and show the total
```

**Model:** gpt-5.6-terra

**Summary:** Revised the product vision to specify server-only bill generation, tax-inclusive item prices, no tip suggestions, and a displayed total. The revision also incorporates generic non-table QR codes and delivered status for items and orders.

### 2026-09-28 10:34:28 CST

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

### 2026-09-28 17:20:43 CST

**User prompt (verbatim):**

```text
Revise thoroghly the derivation table, there are some ordinary cases where it breaks. For example: drinks are delivered and the mains are ready. ready requires every fulfillable item to be ready, and a delivered item isn't. preparing matches because at least one item is ready. So the order shows preparing even though the kitchen has finished everything. This is probably the most common state a table is in.
```

**Model:** gpt-5.6-terra

**Summary:** Reworked the order-status derivation table into mutually exclusive, precedence-ordered rules. The ready rule now treats ready and delivered items as kitchen-complete, so delivered drinks with ready mains show ready; mixed active states remain preparing only when outstanding kitchen or delivery work exists.

### 2026-09-28 17:45:56 CST

**User prompt (verbatim):**

```text
This looks good. Now, lets create the personas
```

**Model:** gpt-5.6-terra

**Summary:** Created personas for the guest, server, kitchen staff member, and restaurant administrator. Each persona documents its goals, needs, frustrations, success conditions, and permitted product workflows.

### 2026-09-28 18:02:04 CST

**User prompt (verbatim):**

```text
Your personas describe needs the vision doesn't support, and neither document says so. Some examples: Daniel serves "several tables," but the vision never attaches an order to a table. Priya wants to stop
   cooking canceled items, but the vision doesn't alert the kitchen when an item is canceled. Daniel wants to know why an item was rejected, but the vision records no rejection reason. Maya wants dietary
   information, but it isn't in the menu scope.

   Check each persona against the vision and find every mismatch like these, not only the ones I listed. For each mismatch, don't change the vision. Either adjust the persona so it fits the product as scoped, or
   keep the need and add it to a numbered open questions section at the end of the personas file, saying what the vision would need to add. Tell me which you did for each one.
```

**Model:** gpt-5.6-terra

**Summary:** Audited each persona against the unchanged vision. Removed unsupported table-based and preparation-note assumptions, and added seven numbered open questions for retained needs that require vision scope decisions.

### 2026-09-28 18:57:05 CST

**User prompt (verbatim):**

```text
Here are the answers. They're decisions, so update both the vision and the personas to match, and list every change you make to each file.

   Tables: I'm reversing the persona change. An order is always attached to exactly one table. The QR code stays generic and identifies nothing; the server picks the table from a list when creating the order. The
   admin maintains that list. Each table has a unique label, is deactivated rather than deleted, and has no seat-capacity attribute. Put Daniel's tables back.

   1. Show item descriptions on the guest menu, managed by the admin. Dietary information is out of scope for this release.
   2. Yes. The guest menu shows prices, and the admin maintains them. Prices include tax and service, so there's no tax rate anywhere in the system.
   3. Yes, add a non-functional requirement for the QR menu on a phone. Propose a measurable target and mark the number as an assumption.
   4. Yes, block it. Both kitchen staff and servers can mark an item unavailable during service. Marking it unavailable removes it from the guest menu immediately and stops it being added to new orders. If an
   item is already on an order when it becomes unavailable, it stays on the order, and the kitchen rejects it if it can't be made.
   5. Yes, with an optional free-text reason that the server can see.
   6. Yes. When a server cancels an item the kitchen has already started, the kitchen gets an alert. Alerts are in-app only; nothing is pushed to a locked or sleeping device.
   7. Roles are Server, Kitchen, and Admin, and each is a login. The kitchen uses one shared station login. Guests have no account and no login. Only the Admin role can use the admin view, except for the
   availability toggle in answer 4.
```

**Model:** gpt-5.6-terra

**Summary:** Updated the vision and personas with the confirmed table model, expanded menu content and pricing rules, mobile performance assumption, availability behavior, rejection reasons, cancellation alerts, and role-based access. Removed the resolved persona open questions.

### 2026-09-29 20:40:47 CST

**User prompt (verbatim):**

```text
This a good start, but there are some key modifications that we need to make. The biggest thing we need to fix is that
   the personas should be much shorter and quick to understand. However, there is some good content that we want to
   preserve that could be included in the 1-pagers. Move the "Frustrations" and "Success looks like" material into a single
   new file, drafts/adoption-risks-openai.md, organised by person. Then re-write each persona to be 2-3 paragraphs of
   prose, no tables, no bullet lists, no headed subsections, no pull quotes. Each description should include: personal
   detail including their name, age and circumstances; their job and what that job involves; their educational background
   and their level of technical skill; and why they would be interested in this product and what they would want to do with
   it. Remove the "Goals" and "Needs", most users do not have clear goals when using software. Replace that material with
   prose explaining why the product would be useful to them and what they would want to do with it. A persona describes a
   person, not the product, so do not restate scope, statuses, or requirement targets from the vision in them. Remove the
   persona-to-workflow summary table as well. Keep all of them in personas/personas-openai.md. Additionally, the four
   personas that we have are all competent users, add a fifth persona that is a new server that needs to onboard quickly to
   the restaurant and learn to use the app in 1-day.
```

**Model:** gpt-5.6-terra

**Summary:** Rewrote the persona file as five concise two-paragraph biographies and created an adoption-risk draft that preserves frustrations and success signals by person. Added a new-server persona with a one-day onboarding need.

### 2026-09-29 20:59:05 CST

**User prompt (verbatim):**

```text
The personas are now too abstract. Keep the format, but in each "why interested" paragraph say concretely what they
   would do with this product during their shift or visit, in plain language rather than status names or requirement
   numbers. For Marcus, say what about the product he would find hard to learn on day one. Make each personal circumstance
   something that affects how they would use the product, or cut it.
```

**Model:** gpt-5.6-terra

**Summary:** Kept the prose-only persona format while replacing abstract adoption statements with concrete visit and shift actions. Tied relevant personal circumstances to product use, removed an unrelated detail, and described Marcus's first-day learning challenges.

### 2026-09-29 21:17:09 CST

**User prompt (verbatim):**

```text
The people who use this product aren't the ones who buy it, and the vision doesn't say who decides to adopt and pay for
   it or what they get as a business. Add a short final paragraph to the vision covering that.

   Then make Elena that buyer: the owner-operator, not a hired manager. She decides whether the restaurant keeps the
   product and also uses the admin view herself. Keep the same prose format, and say what would convince her it's worth
   adopting and what would make her drop it.
```

**Model:** gpt-5.6-terra

**Summary:** Added a final vision paragraph naming the owner-operator as buyer and defining the business value and retention decision. Recast Elena as the owner-operator buyer who uses the administrator view and has explicit adoption and drop criteria.

### 2026-09-29 21:20:38 CST

**User prompt (verbatim):**

```text
In the vision, refer to "the owner-operator" rather than Elena, give the buyer paragraph its own heading, and include
   the owner-operator in the opening "For" sentence.
```

**Model:** gpt-5.6-terra

**Summary:** Updated the vision opening to include the owner-operator and replaced the named buyer paragraph with a dedicated Business Buyer and Value section that uses the owner-operator role consistently.

### 2026-09-29 21:25:52 CST

**User prompt (verbatim):**

```text
Now, we need to create the 1-pagers. Lets do only one first to agree on the format. Follow the template in
   one-pager-template.md. Each 1-pager is one Epic: a coherent area of capability, not a single requirement. The individual
   requirements are the user stories listed inside it, each with its own sub-details and its own size. Derive everything
   from the vision and the personas; do not invent new product scope. And where something is needed but undecided, put it
   in ASSUMPTIONS rather than quietly deciding it. Save to one-pagers/kitchen-queue-and-item-status-openai.md
```

**Model:** gpt-5.6-terra

**Summary:** Created the Kitchen Queue and Item Status epic one-pager using the required template, source-backed user stories, documented assumptions, non-functional constraints, and story-point sizing.

### 2026-09-29 21:29:13 CST

**User prompt (verbatim):**

```text
Good format. Before writing the others, fix these in this one: write each story as a named persona (Priya, Daniel,
   Marcus, etc.) rather than a role, and add a Marcus story where a first-day server needs something from this epic. Keep
   only non-functional requirements that are quality attributes with a way to test them; move rules about who can do what
   into the functional requirements. For sizing, keep Fibonacci but define one point as a day or less of well-understood
   work. And canceling an item that is ready should alert the kitchen too, not only one that is preparing.
```

**Model:** gpt-5.6-terra

**Summary:** Revised the kitchen epic with named personas and a Marcus story, testable quality requirements, functional role rules, a one-point Fibonacci definition, and kitchen alerts for canceled preparing or ready items.

### 2026-09-29 21:38:16 CST

**User prompt (verbatim):**

```text
Two things are still off. The Marcus story is the delivery story renamed; add a separate story for what makes this epic
   hard on a first day, and give Daniel the delivery story back. Re-estimate every story under the one-point-per-day
   definition instead of keeping the old numbers, and drop the "not elapsed-time commitments" hedge. For the shared-state
   NFR, propose an update-time target as an assumption instead of requiring a reopen.
```

**Model:** gpt-5.6-terra

**Summary:** Added a separate Marcus first-day guidance story, restored Daniel’s delivery story, re-estimated all kitchen-epic stories, and moved the shared-state target into assumptions.

### 2026-09-30 11:08:08 CST

**User prompt (verbatim):**

```text
Good. Now write the remaining 1-pagers, enough to cover every requirement the vision and personas imply, in the same
   format. Before writing them, list the epics you plan and which stories from this one-pager, if any, belong elsewhere, so
   nothing is counted twice.
```

**Model:** gpt-5.6-terra

**Summary:** Proposed the remaining epics and mapped the vision and persona requirements to them. Identified the kitchen availability-toggle story as belonging in the menu and availability epic, so it will be moved rather than duplicated. Paused for the user’s review before writing the remaining one-pagers.

### 2026-09-30 11:11:06 CST

**User prompt (verbatim):**

```text
do it
```

**Model:** gpt-5.6-terra

**Summary:** Moved availability ownership from the kitchen epic to the new Guest Menu and Availability epic. Wrote the four approved remaining epics for guest menu and availability, table administration and role access, server order entry, and service completion and billing. Verified the five epics use the required sections, named-persona stories, testable quality requirements, and non-duplicated availability ownership.

### 2026-09-30 11:15:37 CST

**User prompt (verbatim):**

```text
Three gaps to decide. Elena can create and deactivate staff accounts and assign each one a role, so a new server can log
   in on day one; put that in the table administration and role access epic. A server can add items to an order that is
   already open, and they go to the kitchen as new placed items. An order whose items are all canceled or rejected can be
   closed without a bill. Update the affected epics and their sizing, and remove "with a trainer's help" from the Marcus
   billing story.
```

**Model:** gpt-5.6-terra

**Summary:** Updated the affected epics with Elena-managed staff accounts and role assignment, open-order item additions that create placed kitchen items, and bill-free closure for canceled or rejected orders. Added or revised the affected Fibonacci estimates and removed the trainer-help qualifier from Marcus’s billing content.

### 2026-09-30 11:26:25 CST

**User prompt (verbatim):**

```text
Adding items after a bill is generated makes that bill stale. Decide it this way: the bill can be regenerated any time
   before closing and always reflects the current items, and closing requires a bill generated after the last item change.
   Update the billing epic and remove it from the assumptions.
```

**Model:** gpt-5.6-terra

**Summary:** Replaced the unresolved bill-regeneration assumption with functional requirements: bills can be regenerated before closure, reflect current order items, and must be generated after the final item change before closing a delivered order. Updated integrity tests and the related Fibonacci estimates.

### 2026-09-30 11:29:23 CST

**User prompt (verbatim):**

```text
The bill story at 13 is inflated; the stale-bill rule is a timestamp
   comparison. Re-estimate it.
```

**Model:** gpt-5.6-terra

**Summary:** Re-estimated the bill generation and regeneration story from 13 to 8 Fibonacci points. The revised rationale treats stale-bill detection as a timestamp comparison within the existing bill workflow.

### 2026-09-30 11:39:48 CST

**User prompt (verbatim):**

```text
The 1-pagers now carry the detailed scope, so cut the vision back to what a product vision should be. First save the
   current full version to restaurant-ordering/drafts/vision-versions-openai/v3_<date>_<time>_full.md and add a row for it
   in that folder's README. Then rewrite restaurant-ordering/vision/vision-statement-openai.md as the Moore-style vision
   statement plus the Business Buyer and Value section, a few hundred words in total, with a line pointing to the 1-pagers
   for the detail. Only change your own vision and that drafts folder; do not touch any other file.
```

**Model:** gpt-5.6-terra

**Summary:** Archived the full OpenAI vision as a timestamped v3 draft, added its progression-table entry, and replaced the active vision with a concise Moore-style statement, Business Buyer and Value section, and a link to the detailed 1-pagers.

### 2026-09-30 20:32:02 CST

**User prompt (verbatim):**

```text
The vision statement in restaurant-ordering/vision/vision-statement-openai.md is too long and does not follow the
      book's example closely enough. Sommerville's iLearn vision is about 130 words: a Moore-template statement followed by
      one short paragraph about the buyer. Revise yours to match that, using these rules:

      1. Follow the Moore template: FOR the buyer, WHO the need of the staff who feel the problem, the product name and
      category, THAT the key benefit, UNLIKE a real competing alternative a restaurant would actually choose instead (not
   the
      problem restated), and OUR PRODUCT the main point of difference from that alternative.
      2. Do not describe what each role can do. Feature-level detail belongs in the 1-pagers.
      3. Write the statement as a few readable sentences rather than one long one, and do not repeat yourself.
      4. End with one paragraph about the buyer, with no heading, of about 50 words. Say who buys the product, what they
   get
      from it, and why they would keep paying for it. Do not list reasons they would stop using it, and do not repeat
   benefits
      already stated above.
      5. Keep the total under 200 words, excluding the title and status lines, and keep the line pointing to the 1-pagers.

      Only edit your own vision file. Do not save a new draft version or touch any other file. Then append an entry to
      restaurant-ordering/prompt-logs/prompt-log-openai.md in the same format as the existing entries.
```

**Model:** gpt-5.6-terra

**Summary:** Rewrote the OpenAI vision as a concise Moore-template statement with a real POS-suite alternative and a differentiated lightweight operational focus. Replaced the headed buyer section with one short buyer paragraph and retained the link to the detailed 1-pagers.

### 2026-09-30 20:38:37 CST

**User prompt (verbatim):**

```text
Your revised vision follows the structure, but it has become too abstract. Apart from the title, a reader cannot tell
   what the product does. Fix these, keeping the same structure and staying under 200 words:

   1. The WHO clause should name the problem the staff have today, not only what they need. Say what goes wrong with how
   orders and menu changes are handled now.
   2. The THAT clause should state the concrete benefit, not "keeps service coordination accurate and visible". Say what
   the platform does for the floor and the kitchen, and what that changes during service.
   3. Remove "as the restaurant grows". The product is for one restaurant and growth was never part of the scope.
   4. Replace vague phrases such as "dependable shared record", "lightweight operational view", and "retaining direct
   control over the restaurant information it relies on" with plain, specific wording.

   Read the current file from disk before editing. Only edit your own vision file. Then append an entry to
   restaurant-ordering/prompt-logs/prompt-log-openai.md in the same format as the existing entries.
```

**Model:** gpt-5.6-terra

**Summary:** Replaced abstract wording with the current paper-ticket, verbal-update, and separate-menu-record problem, plus concrete shared order and availability information for the floor and kitchen. Removed the unsupported growth reference and made the buyer paragraph specific to one restaurant.

---

## Vision Drafts

### v1 (2026-09-25)

**Status:** Draft  
**Restaurant context:** One casual-dining restaurant

##### Vision Statement

For guests, servers, kitchen staff, and restaurant administrators at a casual-dining restaurant, the Restaurant Ordering and Status Platform provides one shared, accurate view of the current menu and every in-progress order. Guests can scan a QR code to browse the latest available menu, while servers create and manage orders and kitchen staff update their progress from **placed** to **ready**, **canceled**, or **rejected**. Unlike disconnected paper tickets, verbal updates, or separate manual tracking tools, the platform keeps menu availability and order status current for every role, helping the restaurant coordinate service with fewer misunderstandings about what has been ordered and what is ready.

##### Product Scope for the Initial Release

###### In scope

- A QR-code-accessible, view-only digital menu for guests.
- Server-created orders.
- An item and order workflow using the statuses **placed**, **ready**, **canceled**, and **rejected**.
- A kitchen view that receives server-created orders and updates their statuses.
- A server view for entering orders and checking current item and order statuses.
- An administrator view for managing menu categories, items, availability, and modifiers.
- A standalone application for one restaurant.

###### Out of scope

- Guest-initiated ordering.
- Payment processing.
- POS, inventory, or third-party kitchen-display-system integrations.
- Multi-location or multi-restaurant management.

##### Product Principles

1. **One current operational record.** A status change must be visible to the relevant restaurant roles without relying on verbal handoffs or duplicate tracking.
2. **Menu accuracy at the point of browsing.** Guests should see the same current availability, categories, and modifiers that staff use when taking orders.
3. **Role-appropriate workflows.** Guests browse, servers create and monitor orders, kitchen staff update preparation outcomes, and administrators maintain the menu.
4. **Simple initial operations.** The first release prioritizes clear order coordination for one restaurant rather than external integrations or advanced enterprise capabilities.

##### Intended Outcome

Restaurant staff can reliably answer, at any moment, what each guest ordered and whether each item is placed, ready, canceled, or rejected.

### v2 (2026-09-28)

**Status:** Draft  
**Restaurant context:** One casual-dining restaurant

##### Vision Statement

For guests, servers, kitchen staff, and restaurant administrators at one casual-dining restaurant, the Restaurant Ordering and Status Platform provides one shared, accurate view of the current menu and every order. Guests use a generic QR code to browse the latest available menu; the code does not identify a table or a guest. Servers create and manage orders, generate bills, and confirm delivery. Kitchen staff receive orders and manage preparation. Unlike disconnected paper tickets, verbal updates, or separate manual tracking tools, the platform keeps menu availability, order progress, delivery completion, and bill totals current for the staff who need them, reducing uncertainty about what was ordered, what is ready, and what has reached the guest.

##### Product Scope for the Initial Release

###### In scope

- A generic, QR-code-accessible, view-only digital menu for guests. QR codes do not distinguish tables or identify guests.
- Server-created and server-managed orders. Guests cannot create or modify orders.
- Item statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, and **rejected**.
- Order statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, **rejected**, and **closed**.
- A kitchen view that receives server-created orders and updates item preparation states.
- A server view for entering orders, monitoring item and order statuses, confirming delivery, generating bills, and closing orders.
- A server-only bill that lists ordered items, selected modifiers, quantities, and the total. Item prices are tax-inclusive, so the bill does not show a separate tax amount. The bill does not include tip suggestions and does not process payments.
- An administrator view for managing menu categories, items, availability, and modifiers.
- A standalone application for one restaurant.

###### Out of scope

- Guest-initiated ordering, order changes, or bill access.
- QR codes that identify a table, guest, or order.
- Payment processing.
- Separate tax calculations or tip suggestions on bills.
- POS, inventory, or third-party kitchen-display-system integrations.
- Multi-location or multi-restaurant management.

##### Order Lifecycle

###### Item states and transition ownership

| Item status | Meaning | Who can set it |
|---|---|---|
| **placed** | The item has been added to an order and is awaiting kitchen work. | A server creates the item in this status. |
| **preparing** | The kitchen has started work on the item. | Kitchen staff move a placed item to this status. |
| **ready** | The kitchen has completed the item and it can be taken to the guest. | Kitchen staff move a preparing item to this status. |
| **delivered** | The item has reached the guest. | A server moves a ready item to this status. |
| **canceled** | The item will not be fulfilled because the server canceled it. | A server can cancel an item before it is delivered. |
| **rejected** | The item cannot be fulfilled by the kitchen. | Kitchen staff reject an item they cannot fulfill before it is delivered. |

The standard item path is **placed** → **preparing** → **ready** → **delivered**. **Canceled** and **rejected** are terminal exceptions. A server may cancel an item before it is delivered; kitchen staff may reject an item before it is delivered when the kitchen cannot fulfill it.

###### Order status derivation and closure

The system derives each order status from its items, rather than requiring staff to set the order status separately. In these rules, a *fulfillable item* is an item that is neither canceled nor rejected.

| Order status | Derivation or closure rule |
|---|---|
| **placed** | Every fulfillable item is **placed**. |
| **preparing** | At least one fulfillable item is **preparing** or **ready**, but the order does not yet meet the rule for **ready**. This is the single kitchen-working state for orders and items. |
| **ready** | Every fulfillable item is **ready**. An order becomes ready only once every non-canceled item that remains fulfillable is ready. |
| **delivered** | Every fulfillable item is **delivered**. |
| **rejected** | Every item in the order is **rejected**. |
| **canceled** | Every item is terminal (**canceled** or **rejected**) and at least one item is **canceled**. |
| **closed** | A server closes a **delivered** order after generating its final bill. Closing is a deliberate server action and does not mean that payment was processed. |

**Closed** separates food-service completion from bill completion. An order is **delivered** when every fulfillable item has reached the guest. It becomes **closed** only when a server has generated the final bill and marks the delivered order as closed, even though payment remains outside the product scope.

##### Product Principles

1. **One current operational record.** Staff should see status changes without relying on verbal handoffs or duplicate tracking.
2. **Menu accuracy at the point of browsing.** Guests should see current categories, available items, and modifiers before a server takes their order.
3. **Role-appropriate workflows.** Guests browse the menu; servers create and manage orders, confirm delivery, generate bills, and close orders; kitchen staff manage preparation and report rejection; administrators maintain the menu.
4. **Clear completion signals.** **Ready** means an item can leave the kitchen. **Delivered** means it has reached the guest. **Closed** means the server has completed billing work without implying payment was collected.
5. **Simple initial operations.** The first release prioritizes coordinated service for one restaurant rather than payments, integrations, or enterprise capabilities.

##### Intended Outcome

Restaurant staff can reliably answer, at any moment, what each guest ordered, whether each item is placed, preparing, ready, delivered, canceled, or rejected, whether the order is ready, delivered, or closed, and what the tax-inclusive total is for a server-generated bill.

### v3 (2026-09-30)

**Status:** Draft  
**Restaurant context:** One casual-dining restaurant

##### Vision Statement

For guests, servers, kitchen staff, administrators, and the owner-operator at one casual-dining restaurant, the Restaurant Ordering and Status Platform provides one shared, accurate view of the current menu and every order. Guests use a generic QR code to browse the latest available menu; the QR code identifies neither a table nor a guest. Servers select a table when creating an order, manage service progress, generate bills, and confirm delivery. Kitchen staff receive orders, manage preparation, and report unfulfillable items. Administrators maintain menu and table data. Unlike disconnected paper tickets, verbal updates, or separate manual tracking tools, the platform keeps menu availability, order progress, delivery completion, and bill totals current for the staff who need them, reducing uncertainty about what was ordered, what is ready, and what has reached the guest.

##### Product Scope for the Initial Release

###### In scope

- A generic, QR-code-accessible, view-only digital menu for guests. QR codes do not distinguish tables or identify guests.
- Guest menu categories, item names, descriptions, tax- and service-inclusive prices, availability, and modifiers. Dietary information is not included in this release.
- Server-created and server-managed orders. Each order is attached to exactly one table selected by the server from the active table list. Guests cannot create or modify orders.
- A table list managed by administrators. Each table has a unique label, has no seat-capacity attribute, and is deactivated rather than deleted. A deactivated table cannot be selected for a new order but remains identifiable on its existing orders.
- Item statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, and **rejected**.
- Order statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, **rejected**, and **closed**.
- A kitchen view that receives server-created orders and updates item preparation states.
- A server view for selecting a table, entering orders, monitoring item and order statuses, confirming delivery, generating bills, and closing orders.
- A server-only bill that lists ordered items, selected modifiers, quantities, and the total. All menu prices include tax and service; the system stores no tax rate and the bill shows no separate tax or service amount. The bill does not include tip suggestions and does not process payments.
- Menu availability controls for administrators, servers, and kitchen staff. Marking an item unavailable immediately removes it from the guest menu and blocks it from being added to new orders. An item already on an order remains on that order; kitchen staff reject it if it cannot be prepared.
- A kitchen rejection workflow with an optional free-text reason visible to the server.
- An in-app kitchen alert when a server cancels an item that is already **preparing**. Alerts are not pushed to locked or sleeping devices.
- Login-based roles: **Server**, **Kitchen**, and **Admin**. Servers and administrators use their role login; kitchen staff use one shared kitchen-station login. Guests have no account or login. Only **Admin** can access the administrator view. Servers and kitchen staff can use the availability toggle from their own views without gaining administrator-view access.
- An administrator view for managing menu categories, item names, descriptions, prices, availability, modifiers, and the table list.
- A standalone application for one restaurant.

###### Out of scope

- Guest-initiated ordering, order changes, or bill access.
- QR codes that identify a table, guest, or order.
- Dietary information.
- Payment processing, tip suggestions, tax calculations, service-charge calculations, or tax-rate storage.
- Device or lock-screen push notifications for cancellation alerts.
- POS, inventory, or third-party kitchen-display-system integrations.
- Multi-location or multi-restaurant management.

##### Order Lifecycle

###### Item states and transition ownership

| Item status | Meaning | Who can set it |
|---|---|---|
| **placed** | The item has been added to an order and is awaiting kitchen work. | A server creates the item in this status. |
| **preparing** | The kitchen has started work on the item. | Kitchen staff move a placed item to this status. |
| **ready** | The kitchen has completed the item and it can be taken to the guest. | Kitchen staff move a preparing item to this status. |
| **delivered** | The item has reached the guest. | A server moves a ready item to this status. |
| **canceled** | The item will not be fulfilled because the server canceled it. | A server can cancel an item before it is delivered. If the item is **preparing**, the kitchen receives an in-app alert. |
| **rejected** | The item cannot be fulfilled by the kitchen. | Kitchen staff reject an item they cannot fulfill before it is delivered and may provide an optional free-text reason visible to the server. |

The standard item path is **placed** → **preparing** → **ready** → **delivered**. **Canceled** and **rejected** are terminal exceptions. A server may cancel an item before it is delivered; kitchen staff may reject an item before it is delivered when the kitchen cannot fulfill it.

###### Order status derivation and closure

The system derives each order status from its items, rather than requiring staff to set the order status separately. In these rules, a *fulfillable item* is an item that is neither canceled nor rejected. The system evaluates the following rules in the stated order. The first matching rule determines the order status, except that **closed** is a server-set final state that overrides the derived status.

| Order status | Derivation or closure rule |
|---|---|
| **closed** | A server explicitly closes an order only after it is **delivered** and the server has generated its final bill. A closed order cannot receive further item changes. |
| **rejected** | No fulfillable items remain, and every item is **rejected**. |
| **canceled** | No fulfillable items remain, every item is terminal (**canceled** or **rejected**), and at least one item is **canceled**. |
| **delivered** | At least one fulfillable item exists, and every fulfillable item is **delivered**. |
| **ready** | At least one fulfillable item is **ready**, and every fulfillable item is either **ready** or **delivered**. This means kitchen work is complete even when a server has already delivered some items. For example, delivered drinks and ready mains produce an order status of **ready**. |
| **placed** | At least one fulfillable item exists, and every fulfillable item is **placed**. |
| **preparing** | The order did not match any earlier rule and has at least one fulfillable item. This covers any mixed active state, including an item that is **preparing**, or a combination of **placed**, **preparing**, **ready**, and **delivered** items that still has outstanding kitchen or delivery work. **Preparing** is the single kitchen-working term for both items and orders. |

These rules are mutually exclusive when evaluated in precedence order. In particular, an order that contains only **ready** and **delivered** fulfillable items is always **ready**, not **preparing**. **Closed** separates food-service completion from bill completion: an order is **delivered** when every fulfillable item has reached the guest, then becomes **closed** only when a server generates the final bill and marks the delivered order as closed. Closing does not mean that payment was processed.

##### Non-Functional Requirements

- **Mobile QR-menu performance.** **Assumption:** At the 95th percentile, a supported phone on a stable 4G or Wi-Fi connection renders the guest menu's available categories and items within **2 seconds** of opening the QR-code URL. The **2-second** target is an initial assumption to validate with the restaurant and representative devices and networks.

##### Product Principles

1. **One current operational record.** Staff should see status, availability, and table changes without relying on verbal handoffs or duplicate tracking.
2. **Menu accuracy at the point of browsing and ordering.** Guests and servers should see current categories, item descriptions, tax- and service-inclusive prices, available items, and modifiers. Unavailable items cannot be added to new orders.
3. **Role-appropriate workflows.** Guests browse without an account; servers select tables and manage orders and bills; kitchen staff manage preparation, availability, and rejection; administrators maintain menu and table data.
4. **Clear completion signals.** **Ready** means an item can leave the kitchen. **Delivered** means it has reached the guest. **Closed** means the server has completed billing work without implying payment was collected.
5. **Simple initial operations.** The first release prioritizes coordinated service for one restaurant rather than payments, integrations, or enterprise capabilities.

##### Intended Outcome

Restaurant staff can reliably answer, at any moment, what each table ordered, whether each item is placed, preparing, ready, delivered, canceled, or rejected, whether the order is ready, delivered, or closed, and what the tax- and service-inclusive total is for a server-generated bill.

##### Business Buyer and Value

The owner-operator is the business buyer. The owner-operator decides whether to adopt and pay for the platform and whether to keep it after launch. The restaurant should gain fewer avoidable order and availability mistakes, less manual coordination between servers and the kitchen, faster onboarding for new staff, and more consistent service. The owner-operator will continue paying only if those operating benefits outweigh the product's cost and the effort of keeping it current.
