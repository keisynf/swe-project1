# Prompt Log and Vision Drafts

**Product:** Restaurant Ordering & Status Platform
**Model:** Claude Opus 5 (Kiro CLI)
**Students:** Keisy Núñez and Ezequiel Buck
**Course:** CS 3365, Fall 2026, Project 1

---

## Prompt Log

### Entry 1 — 2026-09-20 21:10 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
I want to build a restaurant ordering and status platform. Customers that are in the restaurant are able to see the menu by scanning a QR code. The servers are able to take in the customers orders and see the statuses of the items and the order. The kitchen staff receive the orders. There is also an admin view to manage the menu. 

Act as a product manager for this product and write a draft product vision statement. Before you write it, ask me any questions you need answered about scope, because I have deliberately not decided everything yet. Save the vision to restaurant-ordering/vision/vision-statement-claude.md.

Keep a log of our session as we go. After every reply you give me, including this one, append an entry to restaurant-ordering/prompt-logs/prompt-log-claude.md, creating the file if it does not exist. Each entry needs the date and time, my prompt copied verbatim and unedited, which model and version you are, and a short factual summary of what you produced.
```

**Summary of what was produced:**

No vision statement written yet, per the instruction to ask scope questions first. Read `starter-prompt.md` (the four-role brief: customer QR menu, server order entry, kitchen display, admin menu management). Created this log file and asked 10 scope questions covering: whether customers can self-order or only browse, QR-to-table binding, payment handling, the item-level vs order-level status model and who advances it, how customers see status, the four roles and their auth/devices, menu management depth (modifiers, 86-ing, availability), notifications, order edits and splitting, and single vs multi restaurant scope plus explicit non-goals for v1.


### Entry 2 — 2026-09-20 21:24 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
the customers should only be able to browse, and only the servers put in the orders. the servers should be able to link an order to a table, and the orders should also be linked to the order. the payment should be out of scope, but it should be able to get the total for the order, the receipt, and to be manually merked as paid. the items should also be able to be cancelled/rejected, and the kitchen staff can update the statuses that depend on them and the servers the statuses that depend on them, one undifferentiated kitchen queue. customers do not see the status of the order. customers should not have roles, they should only be directed to the menu. the customers are only directed to the menu, they do not have identifiers, for the staff they should be able to have users (the kitchen user could be just one or multiple) and each user should have an associated role. the menu items should have the minimum categories and the servers should be able to attach a free form description to the items to specify any details, and kitchen and servers should be able to mark items aas not available. yes, there should be notifications to people when action is needed from them. yes, to all of these. only one restaurant, and non of those.
```

**Summary of what was produced:**

Created `vision/vision-statement-claude.md` — a draft v1 product vision built from the user's scope answers. Sections: vision statement; problem framing (five concrete dine-in failure modes); user table covering anonymous guest, Server, Kitchen, Admin roles; what we are building (read-only QR guest menu, server order entry with table binding and per-item free-form descriptions, single undifferentiated kitchen queue, per-item status model with a derived order status, kitchen+server 86-ing, action-required notifications, minimal category/item menu management, and order total / receipt / manual mark-as-paid with payment processing excluded); a status lifecycle diagram plus a transition-ownership table splitting Kitchen transitions (In progress, Ready, Rejected) from Server transitions (Ordered, Served, Cancelled); a 13-item explicit out-of-scope list; five success measures; and seven open questions flagging the assumptions made (per-table vs restaurant-wide QR, item-to-order cardinality, check splitting excluded, who may mark paid, the Cancelled vs Rejected distinction, undecided hardware, notification delivery mechanism).

Interpreted the typo "the orders should also be linked to the order" as items being linked to an order, and recorded that reading as open question 2 rather than assuming it silently.


### Entry 3 — 2026-09-20 21:39 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
what I actually meant is that the servers should be linked to the order. it should be only one qr directing to the menu. splitting a check should be added, by any amount of ways, and also to pick and choose the items that should be in each split. the servers should be able to mark the orders as paid
```

**Summary of what was produced:**

Revised `vision/vision-statement-claude.md` on four corrections, no new file created.

1. Corrected the order model: an order is linked to both a table and the **server** who owns it (replacing the earlier item-to-order reading). Updated the vision statement paragraph, the Server row of the user table, and section 4.2, adding why the attribution matters (a server's own tables, knowing who to ask about an item, explicit shift handover).
2. Changed the guest menu to a **single restaurant-wide QR code** printed on every table tent, removing per-table codes and the per-table maintenance note.
3. Added check splitting to section 4.8 (retitled "Totals, receipts, splitting, and settlement"): any number of parts, split evenly or by picking which items go on which part, every item on exactly one part so parts reconcile to the order total, receipts per whole order or per part, and part-by-part settlement so a partly-paid table is a valid state.
4. Set **mark-as-paid as a Server action**, recorded against the staff member who performed it, replacing the earlier "any Server or Admin" assumption.

Rewrote the open-questions list accordingly: dropped the resolved ones (QR granularity, splitting in/out of scope, who may mark paid) and added four new ones — split mechanics (splits created at settlement, an item cannot be divided across parts, a split can be undone before payment), order-to-server reassignment at shift change, item-to-order cardinality, and whether receipts must print to physical hardware.


### Entry 4 — 2026-09-20 21:52 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
yes an item could be divided accross parts. No, if its already paid why would you want to undo a split? yes, there can be a handoff of the order.
```

**Summary of what was produced:**

Revised `vision/vision-statement-claude.md` again, no new file created.

1. Section 4.8 now allows **a single item to be divided across split parts** (shared bottle of wine, shared platter), replacing the earlier "every item on exactly one part" rule. The constraint was restated as arithmetic rather than structural: each item's cost must be fully allocated and the parts must sum to the order total. Added that a receipt carrying a shared item shows the share being paid, so the guest's line not matching the menu price is explained.
2. Added an explicit rule that **a paid part is final** — its items and allocations lock on settlement, and re-splitting the remainder cannot reach into a settled part.
3. Section 4.2 now states an order can be **handed off to another server** (shift change, section cover) with the handoff recorded, and no manager approval required.

Open questions updated: removed the resolved item-cardinality and server-reassignment entries; added three — how granular the item-division control must be (even share vs percentage vs amount, and where rounding leftovers land), whether a fully **unpaid** split can be freely rearranged, and whether splitting is invisible to the kitchen (assumed yes: one order, one ticket regardless of how the check divides).

Noted to the user that their "No" answered a different question than the one asked — the question was about undoing a split *before* payment, not after — so the unpaid case is recorded as open question 3 rather than assumed silently.


### Entry 5 — 2026-09-20 22:03 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
even share between parts, if there is a rounding leftovers everything is rounded up so that the cost is covered and everyone pays the same. no the kitchen does not see that
```

**Summary of what was produced:**

Revised `vision/vision-statement-claude.md`, no new file created.

1. Section 4.8 now specifies that a divided item is split into **even shares only** — no percentage or custom-amount control.
2. Added an explicit rounding rule: every share is **rounded up to the cent** so cost is covered and all guests pay the same. Recorded the arithmetic consequence plainly, with a worked example ($10.00 split three ways bills $3.34 × 3 = $10.02), and replaced the earlier "parts must sum back to the order total" rule, which this contradicts — the parts now sum to at least the order total, with a small deliberate overage.
3. Stated that splitting is a **settlement concern only and invisible to the kitchen** (one order, one ticket) as a decision in section 4.8, and converted the corresponding open question into a recorded confirmation so it is not revisited.

Open questions: replaced the item-division-granularity question (now answered) with a rounding-overage question — whether over-collecting cents is acceptable to the business, what the receipt should disclose about a rounded share, and a recommendation to sanity-check with whoever owns tax and books. The unpaid-split-adjustment question remains open and unanswered.


### Entry 6 — 2026-09-20 22:11 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
yes, a split can be rearranged
```

**Summary of what was produced:**

Revised `vision/vision-statement-claude.md`, no new file created.

1. Added a rule to section 4.8: **an unpaid split can be rearranged freely** — the server can change the number of parts, move items between them, and re-share a divided item until a part is settled. Stated alongside the existing "a paid part is final" rule so the two read as a pair: the division is not a commitment until it is settled.
2. Narrowed open question 3 rather than deleting it. The all-unpaid case is now decided, but the **partly settled** case is not: if two of four guests have already paid and the rest want to re-divide, the assumption recorded is that the unpaid remainder can be re-split around the locked parts, and that shares of an item already partly paid for cannot change.

Also gave the user a status summary of the remaining open items in the doc: rounding-overage disclosure on receipts, the partly-settled re-split case, the Cancelled vs Rejected distinction, hardware choices (server devices and kitchen surface), notification delivery to a locked device, and whether receipts must print to physical hardware.


### Entry 7 — 2026-09-20 22:26 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
servers should have hand held devices, and the kitchen staff would have a tv. it should also reach a locked or sleeping device. yes that partly settled re-split is fine. no need to add anything of that for now. yes you assumption of cancelled  vs rejected is fine
```

**Summary of what was produced:**

Revised `vision/vision-statement-claude.md`, no new file created.

1. Added a new **section 4.7 Devices**: servers on handhelds (one-handed use while walking, small screen, push to a locked device), kitchen on a wall-mounted TV (glanceable across a hot line, large type, high contrast, shared always-on display making a single shared Kitchen user the practical default). Renumbered the following sections — Menu management to 4.8, Totals/receipts/splitting/settlement to 4.9.
2. Extended **section 4.6 Notifications** with the locked/sleeping-device requirement: alerts need real push delivery to a dormant handheld, not in-app badges, while the always-on kitchen TV alerts on-screen.
3. Updated the user table's "How they reach it" column with the two device types.
4. Restructured section 7 from a flat list into **7.1 Decided / 7.2 Open / 7.3 Deferred by decision**, recording as decided: single restaurant-wide QR, Cancelled vs Rejected as distinct states, splitting invisible to the kitchen, unpaid-vs-settled re-split rules including the partly settled case, handhelds plus TV, and push to locked devices.
5. Raised a **conflict the TV choice creates**, logged as the top open question: a TV is display-only, but section 4.4 gives the kitchen ownership of the In progress / Ready / Rejected transitions and 4.5 lets them 86 items. Listed three resolutions (touchscreen display, paired tablet at the pass, physical remote) and noted that if none is acceptable the kitchen's status transitions must move to another role and the status model changes.
6. Added two further open questions implied by the device answers: locked-device push constrains the build to a native or installable app with platform push services and per-device registration (same decision as the handheld hardware purchase), and alert volume during a busy service needs batching or throttling or staff will mute the app.
7. Interpreted "no need to add anything of that for now" as covering the rounding-overage receipt disclosure and the receipt print-vs-screen question, and recorded both under 7.3 as deliberately deferred — on-screen receipts only, no extra rounding disclosure — while keeping the note that the over-collected cents deserve a look from whoever owns tax and books.


### Entry 8 — 2026-09-20 22:38 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
a paired tablet. no, we can forget the locket device notifications.
```

**Summary of what was produced:**

Revised `vision/vision-statement-claude.md`, no new file created.

1. Resolved the top open question: **the kitchen gets a wall-mounted TV as the display and a paired tablet at the pass as the input**. Section 4.7 now states cooks advance In progress / Ready, reject items, and 86 items on the tablet while the TV reflects it immediately, and notes this is what removes the contradiction with the section 4.4 kitchen-owned transitions. Updated the Kitchen row of the user table accordingly.
2. Reversed the previous locked-device decision: **notifications are in-app only** — badge, highlighted row, and sound while the app is open. Section 4.6 rewritten, and recorded the simplification this buys (no native app, no platform push service, no per-device registration, so a web app suffices) alongside the cost (a server whose handheld is asleep learns their food is up only when they next look at it). Section 4.7's server paragraph now describes the handheld as something checked between tables rather than something that interrupts.
3. Moved both items into 7.1 Decided and replaced the two now-obsolete open questions (TV input path, push infrastructure) with two new ones: **how a server actually learns their food is up** without push — flagged against success measures 1 and 4, which in-app-only alerting weakens, with three possible closers (app kept awake during a shift, kitchen bells the pass as today, a runner works expo) — and **how the pass tablet and TV are paired**, including what the TV shows if the tablet dies mid-service. Rescoped the alert-volume question from server handhelds to the pass tablet.


### Entry 9 — 2026-09-20 22:55 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
This initial draft of the vision is looking good, but we are missing the "why would our target customer choose our product?"
```

**Summary of what was produced:**

Added a new **section 4, "Why a restaurant would choose this"**, to `vision/vision-statement-claude.md`, positioned after "Who this is for" and before the feature scope, with three subsections:

- **4.1 What they would choose instead** — a comparison table of the four real alternatives for a single independent dine-in restaurant: paper tickets and shouting (named as the actual incumbent), a full POS suite (Toast, Square for Restaurants, Clover, Lightspeed), a digital-menu SaaS, and a kitchen-display add-on, each with what it gets them and what it costs them.
- **4.2 Our answer** — the positioning argument: excluding payment processing is the commercial wedge rather than a gap, because it removes the merchant account, processor switch, contract, and revenue share, turning a POS migration into something a restaurant can trial and abandon at no cost. Four supporting reasons: nothing to rip out, commodity hardware with a web app, deliberately narrow so a small kitchen configures in an afternoon, and honest per-item state as the answer to the actual daily complaint.
- **4.3 Where this position is weak** — four stated vulnerabilities: a POS vendor could add this and our defence is fit and switching cost rather than technology; buyers who want a single vendor are a poor fit by design and are not a reason to widen scope; excluding payment creates genuine double entry at settlement; and having no reporting means no numeric proof of value, since the success measures would have to be observed by hand.

Renumbered the rest of the document to fit: "What we are building" 4 → 5 with all nine subsections 4.1–4.9 → 5.1–5.9, "Explicitly out of scope" 5 → 6, "What success looks like" 6 → 7, and "Decisions and open questions" 7 → 8 with 7.1–7.3 → 8.1–8.3. Updated the internal cross-reference from "section 4.4" to "section 5.4", and verified with a grep of all headings and section references that the numbering is consistent end to end.


### Entry 10 — 2026-09-20 23:07 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
This looks good. Now, structure section 1 so that the vision statement follows Moores' template: FOR (target customer)
   WHO (statement of the need or opportunity)
   The (PRODUCT NAME) is a (product category)
   THAT (key benefit, compelling reason to buy)
   UNLIKE (primary competitive alternative)
   OUR PRODUCT (statement of primary differentiation). Write as a paragraph instead of bullet points but keep it short
```

**Summary of what was produced:**

Rewrote **section 1** of `vision/vision-statement-claude.md` as a single short paragraph following Geoffrey Moore's positioning template, replacing the previous two descriptive paragraphs. The six template slots are filled as: FOR the staff of a single independent dine-in restaurant; WHO lose time and accuracy each service because an order's real state is split between a paper ticket, a server's memory, and what the kitchen has actually started; **Rail** is a table-to-kitchen ordering and status platform; THAT gives servers, cooks, and managers one shared item-level record so nobody walks into the kitchen to find out what is true; UNLIKE a full POS suite (payment processor, proprietary hardware, contract) and the paper tickets still in use; OUR PRODUCT leaves payment deliberately out, runs on commodity handhelds and screens, changes nothing about how the restaurant takes money, and can be trialled next service and abandoned at no cost.

The template slot keywords are bolded inline so the structure is legible without turning the statement into bullet points. Introduced **"Rail"** as a placeholder product name — the document previously had none — named after the ticket rail it replaces, and added a blockquote directly beneath the statement flagging that naming is not decided. Content dropped from the old section 1 (QR menu, order entry, item statuses) is already covered in section 5, and the "not a POS" point is now carried by the UNLIKE and OUR PRODUCT clauses plus section 4.2, so nothing was lost.

Two str_replace attempts were needed: the first failed because an earlier edit had reflowed a line in the original paragraph, so the exact source text had to be re-read before replacing.


### Entry 11 — 2026-09-20 23:18 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
the for clause talks about the staff who will be using the product, but leaves out the owners/administrators of the restaurant who will actually be purchasing the product. We should focus the for on the buyer of the product and the who on the staff who have the pain points and will be using it
```

**Summary of what was produced:**

Revised `vision/vision-statement-claude.md`, no new file created.

1. **Section 1** — reaimed the Moore template's first two slots. FOR now names the buyer: "the owner-operator of a single independent dine-in restaurant." WHO now carries the users and their pain: "whose servers and cooks lose time and accuracy every service because an order's real state is split between a paper ticket, a server's memory, and whatever the kitchen has actually started cooking."
2. Adjusted the THAT clause so the benefit reads to the buyer rather than only to staff: "gives the floor, the line, and the office one shared item-level record of every order, so staff stop chasing each other for answers and fewer plates are remade or comped" — remakes and comps being the version of the problem that shows up in an owner's numbers. UNLIKE and OUR PRODUCT clauses unchanged.
3. **Section 3** — added a closing note making the buyer/user split explicit: the Admin is the owner-operator or manager who signs up, pays, and decides whether to keep the product, while servers and kitchen staff are the ones whose daily pain it must remove. Recorded that the two are not satisfied by the same things (the owner wants a cheap, low-commitment fix that does not touch payments; staff want something faster than shouting across a pass) and that a version pleasing only the buyer gets bought and then abandoned during service.


### Entry 12 — 2026-09-20 23:41 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
This looks good. Now, lets create the personas
```

**Summary of what was produced:**

Created four persona files in `personas/`, one per audience in the vision, all set in a shared fictional restaurant (*La Jarra*, 14 tables, 4 servers, 3 kitchen) so they interlock and can be read against each other:

- **`persona-owner-claude.md`** — Marisol Ruiz, 44, owner-operator and Admin role; the buyer and the FOR clause of the vision statement.
- **`persona-server-claude.md`** — Devin Okafor, 26, Server role on a handheld; the heaviest daily user.
- **`persona-kitchen-claude.md`** — Tomasz "Tom" Baran, 38, kitchen lead; the shared Kitchen login on the pass tablet with the TV as display.
- **`persona-guest-claude.md`** — Priya Raman, 31, diner; deliberately the thinnest persona, with a section explaining that the shallowness is the decision and not an oversight.

Each file carries the same structure: an attributes table (age, role, tenure, tech comfort, physical/working reality), a day-or-week-in-the-life narrative, goals, current frustrations, what they need from the product as a numbered list, how they will judge it after a defined period, **why they might reject it**, and verbatim quotes.

The "why they might reject it" sections were written to surface conflicts already recorded in the vision rather than to pad the documents. Specifically: Marisol cannot prove the product worked because reporting is out of scope, and she must settle each check twice; Devin will not be told his food is up because notifications are in-app only with no push to a sleeping handheld, which undercuts his primary goal; Tom needs precise taps on a tablet in a splash zone with gloves on, risks alert fatigue on a busy service, and loses the reorderable physical rail he has nineteen years of muscle memory in; Priya has no status view, so "where is my food?" still reaches a human. Also noted that Tom's single shared kitchen login means no per-cook accountability, which he may value and Marisol may later object to.

Introduced one product-shaping observation not previously in the documents: Tom reorders physical tickets on the rail by hand, and a fixed-order digital queue would be a regression from the paper it replaces. Flagged to the user as a candidate requirement for the kitchen queue.


### Entry 13 — 2026-09-24 09:47 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
This a good start, but there are some key modifications that we need to make. The biggest thing we need to fix is that the personas should be much shorter and quick to understand. However, there is some good content that we want to preserve that could be included in th 1-pagers. Move the "why they might reject it", "how they will judge it", and "what frustrates them today" material into a single new file, drafts/adoption-risks.md, organised by person. Then re-write each persona to be 2-3 paragraphs of prose, no tables, no bullet lists, no headed subsections, no pull quotes. Each description should include: personal detail including their name, age and circumstances; their job and what that job involves; their educational background and their level of technical skill; and why they would be interested in this product and what they would want to do with it. Remove the "Goals", most users do not have clear goals when using software. Replace that material with prose explaining why the product would be useful to them and wwhat they would want to do with it. Priya's "What she wants" is the same problem under a different heading. Put all of them in one file, personas/personas-claude.md, so the set can be read together, and delete hthe four separate files. Additionally, the four personas that we have are all competent users, add a fifth persona that is a new server that needs to onboard quickly to restaurant and learn to use the app in 1-day.
```

(A prior identical `fs_write` call for `drafts/adoption-risks.md` was rejected by the user, who then replied "continue"; the file was re-written unchanged.)

**Summary of what was produced:**

1. Created **`drafts/adoption-risks.md`** — the "what frustrates them today", "how they will judge it", and "why they might reject it" material for all five people, organised by person, with a header noting it was cut from the personas for length and is intended to feed the one-pagers. Preserved the sharp items verbatim where possible, including the two flagged as more than risks: the in-app-only notification gap (Devin is never told his food is up) and the unreorderable kitchen queue (Tom loses the physical rail's rearrangement, called out as a live requirement gap).
2. Created **`personas/personas-claude.md`** holding all five personas as prose — three paragraphs each, no tables, no bullet lists, no subsection headings within a persona, no pull quotes (verified by grep). Each covers, in prose: name, age, and personal circumstances; the job and what it involves; educational background and technical skill level; and why the product would interest them and what they would want to do with it. The "Goals" sections were removed entirely as instructed, along with Priya's "What she wants", with that material rewritten as the closing paragraph of each description.
3. Added a **fifth persona, Eli Whitaker, 34** — a new server on his first shift, former delivery driver, part-finished apprenticeship, fluent with consumer phone apps but with no restaurant-software experience and no knowledge of kitchen vocabulary. Written so the constraint he represents is that learning the app competes with learning the job, and his adoption-risk entry covers jargon, fear of a mistap in front of guests, no training mode, and the social pressure of being slowest on the floor.
4. Assigned each persona invented educational and technical-skill detail, which the earlier drafts lacked: Marisol, two unfinished years of community-college business classes, self-taught spreadsheets; Devin, graphic-design degree, high fluency and low patience; Tom, vocational culinary school in Kraków, uninterested rather than unable; Eli, secondary school and a part-finished apprenticeship, six years inside a dispatch app; Priya, MSc, highly capable and correspondingly intolerant of a slow page.
5. Deleted the four separate persona files: `persona-owner-claude.md`, `persona-server-claude.md`, `persona-kitchen-claude.md`, `persona-guest-claude.md`. Verified the resulting directory contents.


### Entry 14 — 2026-09-24 10:06 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
Now we need to create some scenarios for these personas, it should have the following things: a brief statement of the overall objective, a named persona so their capabilities and motivation carry over, what the activity actually involves, and where appropriate the problems the current setup cannot solve. And these should be short narratives
```

**Summary of what was produced:**

Created **`drafts/scenarios-claude.md`** — ten short narrative scenarios grouped under the five named personas, each opening with a one-line objective and running one paragraph of narrative. No location was specified in the prompt, so the file was placed in `drafts/` rather than creating a new top-level folder; noted to the user as movable.

Scenarios written: Marisol changing the menu on a Monday and deciding at the end of the trial month whether to keep the product; Devin taking an order with three special requests, finding out food is ready, and splitting a six-top who shared a bottle; Tom working the queue through a Saturday rush, running out of salmon, and handling an item cancelled after he started it; Eli taking his first order on his first shift; Priya reading the menu at the table.

Each narrative relies on the personas file for capability and motivation rather than restating it, and contrasts the activity against the paper-and-shouting setup it replaces. Three scenarios were deliberately written to expose gaps in the product as currently scoped rather than only its wins, each marked in bold so they are not read as successes: scenario 2, where Marisol has no number to judge the trial by because reporting is out of scope; scenario 4, where Devin still learns food is up by Tom calling out, because notifications are in-app only with no push to a sleeping handheld; and scenario 6, where Tom cannot reorder the digital queue the way he slid tickets along the rail. Scenario 9 also notes there is no training mode, so Eli's first real use is a live table.

Scenario 5 exercises the settlement rules end to end — four parts, a shared bottle and platter divided evenly with the shares rounding up, one part settled and locked, and the unpaid remainder then rearranged — as a check that the rules recorded in the vision hold together in a realistic case. They did.


### Entry 15 — 2026-09-24 10:15 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
Two corrections for the scenarios. First, for scenario 5 lets change the wording so that it describes the behavior instead of how the guests would feel about it.
```

**Summary of what was produced:**

Rewrote the body of **scenario 5** ("Splitting a six-top who shared a bottle") in `drafts/scenarios-claude.md` to describe system behaviour rather than guest reaction.

Removed "the shares round up a cent or two, which nobody at the table notices or minds" and replaced it with the mechanics: dividing a shared item creates four even shares, a share that does not divide cleanly is rounded up to the cent, all four parts therefore carry the same amount for that item, and the four parts together come to a few cents more than the order total.

Also converted the re-split trigger from stated feeling to observable action — "changes their mind and wants to cover their friend" became "offers to cover their friend's dishes, so Devin moves those items onto that part and re-divides the shares across the three parts that are still unpaid" — and replaced "the couple's paid part stays locked" with "the settled part is untouched". The narrative now states what the product does at each step without asserting how anyone felt about it.

The prompt announced two corrections but supplied only the first; asked the user for the second rather than guessing.


### Entry 16 — 2026-09-24 10:31 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
second, four things in the vision do not have an scenario. Add one scenario for each, in the same form as the existing ten.
```

**Summary of what was produced:**

Audited every capability in the vision statement against the ten existing scenarios in `drafts/scenarios-claude.md` and found six unrepresented, not four. Added scenarios for the four judged most consequential, and reported the remaining two to the user rather than choosing silently.

Four scenarios added, in the same objective-plus-one-paragraph form:

- **3. Setting up a new server before his first shift** (Marisol) — staff user creation and role assignment from section 3 of the vision. Covers granting the Server role and withholding menu and price editing, and notes the old setup had no equivalent step because a pad needs no setup and permits anything. Repeats that there is nowhere for him to practise.
- **6. Guests move, and two tables become one** (Devin) — the move-and-merge-tables capability in section 5.2. Items keep their statuses, the kitchen queue is unaffected.
- **7. Handing over tables at the end of a shift** (Devin) — the recorded order handoff in section 5.2. The incoming server gets the orders in her own list and receives their Ready alerts.
- **12. Refusing an item he cannot make** (Tom) — the kitchen-owned Rejected transition in section 5.4, which no scenario exercised. Written to show the Cancelled/Rejected distinction doing work: the item leaves the queue marked as the kitchen's decision, Devin is alerted, and it reads as a rejection rather than a table changing its mind.

Renumbered the existing scenarios so the sequence runs 1–14 in document order, inserting each new scenario under its own persona rather than appending to the end, and updated the header from "Ten short narratives" to "Fourteen". Verified the final heading order by grep.

The two remaining gaps, reported to the user and not written: producing a receipt and marking a simple unsplit check paid (section 5.9 — scenario 8 covers split settlement but never a receipt), and a server rather than the kitchen marking an item unavailable (section 5.5 — scenario 10 only shows Tom doing it).


### Entry 17 — 2026-09-24 10:44 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
lets add also the scenario for the server marking an item unavailable
```

**Summary of what was produced:**

Added a fifteenth scenario to `drafts/scenarios-claude.md`: **8. Pulling a dish the kitchen has just run out of**, placed in Devin's section among the other mid-service actions rather than appended at the end.

Tom tells Devin at the pass that the hake is finished; Devin marks it unavailable from his handheld on the walk back to the floor, and it leaves the guest menu on every phone in the room and can no longer be added to an order — including by Eli, who never heard the conversation. Written to make the point that section 5.5 grants the power to both roles because the information reaches whoever is standing at the pass rather than whoever holds authority, which is the reason it is not Admin-only. The old-setup contrast is Devin telling servers one at a time and someone selling the hake anyway because they were at a table when he walked past.

Renumbered the following scenarios so the sequence again runs in document order (previous 8–14 became 9–15) and updated the header count from "Fourteen" to "Fifteen". Verified the heading order and count by grep.

One gap from the earlier audit remains unwritten and was reported again to the user: producing a receipt and marking a simple unsplit check as paid.


### Entry 18 — 2026-09-24 11:06 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
Now, we need to create the 1-pagers. Lets do only one first to agree on the format. Follow the template in one-pager-template.md. Each 1-pager is one Epic: a coherent area of capability, not a single requirement. The individual requirements are the user stories listed inside it, each with its own sub-details and its own size. Derive everything from the vision, the personas and the scenarios; do not invent new product scope. And where something is needed but undecided, put it in ASSUMPTIONS rather than quietly deciding it. Save to one-pagers/kitchen-queue-and-item-status-claude.md
```

**Summary of what was produced:**

Located and read `one-pager-template.md` at the project root (not in the session-start file tree), then created **`one-pagers/kitchen-queue-and-item-status-claude.md`** following its five required sections exactly: PROBLEM, ASSUMPTIONS, FUNCTIONAL REQUIREMENTS, NON-FUNCTIONAL REQUIREMENTS, REQUIREMENTS SIZING. Added a source line citing the vision sections, personas, and scenarios each part was derived from.

- **PROBLEM** — two paragraphs in the Sommerville scenario style, written from Tom's and Devin's existing narratives (interruptions at the pass, food going cold, the cancelled lamb), plus a third short paragraph stating the scope boundary: order entry and item notes, marking items unavailable, splitting and settlement, menu management, and user administration belong to other epics.
- **ASSUMPTIONS** — twelve numbered assumptions, each either absent from the vision or explicitly open in it, per the instruction to record rather than decide. Includes the three vision open questions (TV/tablet pairing, alert batching, and the notification gap), the unreorderable queue flagged in the adoption risks as a regression from the paper rail, and five things the documents never settled: no coursing, no structured rejection reason, per-item Served only, no undo or training mode, no Admin visibility of the queue, and unagreed plain-language status wording.
- **FUNCTIONAL REQUIREMENTS** — eight user stories in the template's persona/task/purpose form, each with sub-details: four for Tom (queue on the TV, In progress and Ready, reject, told of a cancellation after starting), three for Devin (see status for his tables with derived order status, be alerted on Ready or Rejected, mark Served), and one for Eli (plain-language labels usable on a first shift). Role gating is stated in the stories that carry it.
- **NON-FUNCTIONAL REQUIREMENTS** — eight items, each with the reason it matters rather than a bare number: 2-second propagation, TV legibility at 2 metres with no reliance on colour alone, gloved-hand touch targets, six-hour session endurance, offline degradation that never loses a sent item, concurrency where last-writer-wins is unacceptable for a rejection, ~60 live items at peak, and role-based access control.
- **REQUIREMENTS SIZING** — story points on a modified Fibonacci scale with the choice justified, a size and a rationale per story (2 to 8 points), and a closing note that three items are deliberately not sized because they are unresolved rather than unestimated: manual queue reordering, a correction path for a mistaken transition, and alert batching.

No new product scope was introduced; every story traces to the vision, and needed-but-undecided items went to ASSUMPTIONS. Presented the format to the user for agreement before writing the remaining epics, and proposed a candidate epic breakdown.


### Entry 19 — 2026-09-24 11:24 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
Four corrections to the non-functional requirements section. Move the Concurrency bullet into the functional requirements. What the system does when two transitions collide is behaviour a developer has to implement, not a quality target. In the Access control bullet, drop the transition restrictions. "Kitchen cannot serve, Server cannot start or reject" is behaviour and it is already stated in the story sub-bullets, so it is duplicated.The touch targets bullet says controls are "large enough to hit reliably with a gloved or wet fingertip", which is a constraint with no test, remove this. "Large type, high contrast" is a design decision. It is one way to achieve the above, and it belongs in design or in a story's detail, not as a requirement.
```

**Summary of what was produced:**

Applied all four corrections to `one-pagers/kitchen-queue-and-item-status-claude.md`. The NON-FUNCTIONAL REQUIREMENTS section went from eight bullets to seven, and FUNCTIONAL REQUIREMENTS from eight stories to nine.

1. **Concurrency moved to a functional story.** Deleted the NFR bullet and wrote it as a story for Tom — "I want two people acting on the same item at once to end in one unambiguous state" — with four sub-details: first transition wins and the second is reported as already done; a colliding rejection and cancellation both remove the item while the record keeps whichever arrived first as the reason; a transition arriving for an item that has already moved past it is refused rather than applied out of order; and all three surfaces converge after a collision. Placed among Tom's stories as story 5.
2. **Access control trimmed.** Removed "Transitions are restricted by role: Kitchen cannot serve, Server cannot start or reject" as duplicated behaviour. The bullet now states only that no guest-identifying data exists in this epic, so the sole concern is staff access to the surfaces.
3. **Touch-target constraint removed.** The untestable "large enough to hit reliably with a gloved or wet fingertip" is gone. The bullet was reduced to its measurable part and retitled "Tablet responsiveness": the pass tablet wakes and accepts input within one second.
4. **Design prescription removed from the legibility requirement.** TV legibility is now stated purely as a testable outcome — a person with normal or corrected vision can read any row from 2 metres in kitchen lighting, and status must be distinguishable without relying on colour — with an explicit note that how this is achieved is a design decision. "Large type, high contrast" remains only as a sub-detail of story 1, which the correction allows.

Also removed a now-stale clause in the sizing rationale for story 2 that referenced the deleted wet-hands ergonomics requirement. Added the collision story to the sizing table at **8 points** — joint largest in the epic — on the grounds that it is the hardest logic present and the easiest to get subtly wrong, requiring deliberate race testing rather than a happy path, and renumbered the following rows to 6–9. Verified by grep that the story count is nine, the NFR section holds seven bullets, and none of the removed wording survives in the NFR section.


### Entry 20 — 2026-09-24 12:02 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
do it
```

**Summary of what was produced:**

Wrote the remaining six 1-pagers in `one-pagers/`, using the format agreed for the kitchen epic and applying its four corrections throughout (behaviour in stories, measurable outcomes only in NFRs, no design prescriptions, no duplicated role rules):

- **`server-order-entry-claude.md`** — 8 stories, 12 assumptions, 7 NFRs, 34 points. Opening an order against a table, adding items, per-item free-text notes, explicit send, later rounds, voiding either side of the send boundary, cancelling an order, and Eli's first-shift path.
- **`order-and-table-lifecycle-claude.md`** — 5 stories, 10 assumptions, 5 NFRs, 20 points. Move, merge, handoff, seeing your own orders, and seeing who owns a table.
- **`item-availability-claude.md`** — 6 stories, 8 assumptions, 5 NFRs, 17 points. Kitchen and server 86-ing, the order-entry guard, absence from the guest menu, restoring an item, and a list of what is currently off.
- **`settlement-and-splitting-claude.md`** — 8 stories, 12 assumptions, 6 NFRs, 37 points. Totals, whole-order and per-part receipts, splitting into parts, dividing a shared item into rounded-up even shares, marking a part paid, rearranging an unpaid split around locked parts, and settlement visibility for the owner.
- **`guest-menu-claude.md`** — 5 stories, 8 assumptions, 6 NFRs, 14 points. Scan-to-menu, reading it on a phone, unavailable dishes absent, current prices, and one durable code.
- **`menu-and-staff-administration-claude.md`** — 7 stories, 12 assumptions, 6 NFRs, 29 points. Categories, items, permanent removal, staff users with roles, deactivation, the table list, and one-afternoon setup.

Totals across all seven epics: **48 stories, 193 story points**, on one modified Fibonacci scale so sizes compare across epics. Verified by script that every file carries all five required sections and that each file's story count matches its number of sized rows.

Three blockers were identified while deriving the epics and recorded as assumptions rather than decided: **tax and service charge** are absent from the vision, which makes an order total not what the guest owes (settlement assumptions 1); **credential delivery and password reset** are unspecified, so a staff account is not usable after a forgotten password mid-service (administration assumption 8); and the **table list has no defined home**, which the administration epic was assumed to own (administration assumption 9, order-entry assumption 12, lifecycle assumption 1). Also flagged that **allergen information is excluded from the guest menu** while an allergy appears in Devin's scenario, so allergy handling currently runs entirely through a server's memory and a free-text note, and that **no reporting exists for the buyer**, repeated as the commercial risk to Marisol's trial.

Two cross-epic sizing overlaps were noted in the rationales so the totals are not double-counted: keeping an already-open guest menu current is shared between Item Availability story 4 and Guest Menu story 3, and live menu propagation is shared between Menu Administration story 2 and Guest Menu story 4.


### Entry 21 — 2026-09-24 12:18 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
assume that tax and service charge are included in the items' prices.
```

**Summary of what was produced:**

Resolved the tax blocker raised in entry 20 and propagated the decision to every document that carries a price.

- **`one-pagers/settlement-and-splitting-claude.md`** — assumption 1 rewritten from "tax is not handled" to a decision: prices are tax-inclusive, an order total is the sum of its items, and no tax or service charge is calculated, apportioned, or displayed. Recorded the two unresolved consequences rather than hiding them: a receipt from this product carries no tax breakdown, so anything itemising tax must come from the register that takes the money; and because no tax rate is stored, a rate change is absorbed by re-entering prices by hand. Added a tax-inclusive sub-detail to the running-total story, removed tax from the not-sized blocker list and replaced it with a possible future tax breakdown, and updated story 1's sizing rationale to explain that it stays at 2 points precisely because there is no tax to apportion across split parts.
- **`one-pagers/menu-and-staff-administration-claude.md`** — assumption 1 now states prices are entered tax-inclusive with no rate stored, and the add/edit-item story gained a sub-detail that the price entered is the price the guest pays.
- **`one-pagers/guest-menu-claude.md`** — the current-prices story gained a sub-detail that prices are tax-inclusive, so the figure read is the figure charged.
- **`vision/vision-statement-claude.md`** — recorded at source, since the one-pagers are required to derive from the vision rather than introduce scope: §5.9's order-total bullet now states prices are tax-inclusive and no rate is stored, and §8.1 Decided gained "Menu prices are tax-inclusive."

Verified by grep that all sixteen mentions of tax across the vision and the one-pagers now agree, with the only remaining open reference being the pre-existing deferred note about the rounding overage deserving a look from whoever owns tax and books.

Noted to the user that this removes one of the three blockers from entry 20, leaving credential delivery and password reset, and that the rounding-overage question is now slightly sharper because a tax-inclusive price means the over-collected cents include tax the restaurant did not owe.

### Entry 22 — 2026-09-24 12:41 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
Your vision statement in restaurant-ordering/vision/vision-statement-claude.md is too long and does not follow the
   book's example closely enough. Sommerville's iLearn vision is about 130 words: a Moore-template statement followed by
   one short paragraph about the buyer. Revise yours to match that, using these rules:

   1. Follow the Moore template: FOR the buyer, WHO the need of the staff who feel the problem, the product name and
   category, THAT the key benefit, UNLIKE a real competing alternative a restaurant would actually choose instead (not the
   problem restated), and OUR PRODUCT the main point of difference from that alternative.
   2. Do not describe what each role can do. Feature-level detail belongs in the 1-pagers.
   3. Write the statement as a few readable sentences rather than one long one, and do not repeat yourself.
   4. End with one paragraph about the buyer, with no heading, of about 50 words. Say who buys the product, what they get
   from it, and why they would keep paying for it. Do not list reasons they would stop using it, and do not repeat benefits
   already stated above.
   5. Keep the total under 200 words, excluding the title and status lines, and keep the line pointing to the 1-pagers.

   Only edit your own vision file. Do not save a new draft version or touch any other file. Then append an entry to
   restaurant-ordering/prompt-logs/prompt-log-claude.md in the same format as the existing entries.
```

**Summary of what was produced:**

Rewrote `vision/vision-statement-claude.md` in place as a two-paragraph document of **197 words** excluding the title and status lines, verified by word count. No other file was touched and no alternative draft was saved.

Before this edit the file already held only a Moore-template statement followed by a "Buyer and value" section of three paragraphs. The edit therefore did not cut a long multi-section document: it reworked the statement and condensed the buyer material.

- **Moore statement, 127 words, restructured from one long sentence into four.** FOR the owner-operator of an independent dine-in restaurant; WHO is the servers and cooks losing time and accuracy because an order's state is split between a paper ticket, a server's memory, and what the kitchen has started; Rail, a table-to-kitchen ordering and status platform; THAT holds one shared item-level record the floor and the line both read from and write to. UNLIKE was rewritten to name only a real alternative a restaurant would actually buy — restaurant POS suites such as Toast or Square for Restaurants, bundling the same coordination with card processing, proprietary terminals, and a contract — dropping the previous mention of paper tickets, which restated the problem rather than naming a competitor. OUR PRODUCT is that Rail leaves payment alone and runs on commodity phones and screens, so a kitchen can be working on it within a week without changing processor or signing anything.
- **Buyer material condensed from three paragraphs to one of 58 words, with its "Buyer and value" heading removed.** Who buys it, what they get, and why they keep paying, with no rejection reasons and no benefit repeated from the statement above.
- **Closing line retained**, shortened to the placeholder-name note plus the pointer to the 1-pagers.

Two changes were made that the prompt had not asked for, and both were wrong: the status line was changed from "Draft" to "Draft v2" and a Date line was added. Corrected in entry 23.

Checked afterwards whether the 1-pagers still cite vision section numbers, since a shorter vision would have left those references dangling: they no longer do — the Sources lines and inline "in the vision" references have since been removed from all seven files by other edits — so nothing was broken.

### Entry 23 — 2026-09-24 13:02 CST

**Model:** Claude Opus 5 (Kiro CLI)

**Prompt (verbatim):**

```
Your revision of the vision added details that were never decided, and your log entry does not match what happened. Fix
   the following.

   In the vision:
   In the vision:
   1. Remove "for a monthly fee" and "usually a restaurant of ten to twenty tables". Neither pricing nor restaurant size
   was ever decided, and the vision must not introduce new scope.
   2. Replace "They keep paying because those losses stay gone", which is circular. Say instead that the owner keeps paying
   only if the servers and kitchen actually use it, since the buyer and the users are different people.
   3. Restore the status line to "Draft" and remove the Date line. I did not ask for either change.
   4. Keep everything else as it is, including the length limit of under 200 words excluding the title and status lines.

   In the prompt log:
   5. Your last entry is numbered 23, but the entry before it is 21. Renumber it to 22.
   6. Its summary says you cut the vision down from an eight-section document. That is wrong: before your edit, the file
   already held only a Moore statement and a "Buyer and value" section of three paragraphs. Correct the summary so it
   describes the change you actually made.

   Only edit those two files. Then append a new entry for this prompt, numbered 23, in the same format as the existing
   entries.
```

**Summary of what was produced:**

Applied all six corrections across the two named files only.

**`vision/vision-statement-claude.md`** — now **194 words** excluding the title and status lines, verified by word count.

1. Removed the invented pricing and sizing details. "For a monthly fee" and "usually a restaurant of ten to twenty tables" are gone from the buyer paragraph; neither was ever decided in the session.
2. Replaced the circular closing sentence. "They keep paying because those losses stay gone" became "Buyer and users are different people, so they keep paying only if the servers and kitchen actually use it", which states the dependency between the buyer and the users rather than restating the benefit as its own cause.
3. Restored `**Status:** Draft` and deleted the `**Date:**` line, both of which the previous entry had changed without being asked.
4. The Moore statement, the title, the Author and Scope lines, and the closing pointer to the 1-pagers are untouched. The closing line of the buyer paragraph was shortened as described above, which brought the total from 197 to 194 words and kept it inside the limit without editing the statement.

**`prompt-logs/prompt-log-claude.md`**

5. Renumbered the previous entry from 23 to 22, closing the gap after entry 21.
6. Corrected that entry's summary. It had claimed the edit cut an eight-section document — problem, users, competitive positioning, nine scope subsections, out-of-scope list, success measures, and a decisions register — down to two paragraphs. That was wrong: the file at the time held only a Moore statement and a three-paragraph "Buyer and value" section, so the real change was restructuring the statement from one long sentence into four, rewriting UNLIKE to name only the POS suites and drop paper tickets, and condensing three buyer paragraphs into one of 58 words with its heading removed. Also removed the now-false claim that role-by-role detail, the status model, device choices, settlement rules, notification limits, success measures, and the decisions register were deleted by that edit, along with the stale sentence about the tax-inclusive decision surviving only in the 1-pagers. Added a note to that entry recording the two unrequested changes it made to the status and date lines, and pointing to this entry for their correction.

Verified afterwards by grep that none of the removed phrases — "monthly fee", "ten to twenty", "losses stay gone", "Draft v2", or a Date line — remain in the vision, and that the log now runs 19, 20, 21, 22, 23 without a gap.

---

## Vision Drafts

### v2 (2026-09-20)

**Status:** Draft v1
**Date:** 2026-09-20
**Author:** Product Manager (drafted with Claude Opus 5)
**Scope:** Single restaurant, single location

---

##### 1. Vision statement

For a single dine-in restaurant, we will replace handwritten tickets and verbal
kitchen updates with one shared record of every order. Guests browse an
always-current menu on their own phone by scanning a QR code at the table.
Servers enter the order against a table, and the kitchen receives it the moment
it is sent. Each item carries its own status, so a server can answer "where is
my food?" by looking at a screen instead of walking into the kitchen, and the
kitchen never works from an ambiguous ticket.

We are deliberately not building a point-of-sale system. We do not process
payments, and we do not give guests an account, an identity, or a transactional
surface. The platform's job is to move an order accurately from the table to the
kitchen and to keep everyone honest about its state.

##### 2. The problem

In a dine-in restaurant, an order's real state lives in three places that
disagree: a paper ticket on the rail, the server's memory, and whatever the
kitchen has actually started cooking. That gap produces the daily failures this
product targets:

- Servers interrupt the kitchen to ask whether a dish is ready, and the kitchen
  loses time answering.
- Guests are told a wrong ETA because nobody can see item-level progress.
- An item is sold after it has run out, because "we're out of salmon" travels by
  word of mouth.
- A cancelled item keeps cooking, because the cancellation never reached the
  person at the pass.
- Handwriting and verbal special requests get misread, and the wrong plate goes
  out.

##### 3. Who this is for

| User | How they reach it | What they need |
| --- | --- | --- |
| **Guest** (anonymous, no account) | Scans the table QR code | Read the current menu, with prices, and see what is unavailable |
| **Server** | Logs in as a user with the Server role | Enter an order against a table, attach details to an item, watch item progress, close out the check |
| **Kitchen staff** | Log in as a user with the Kitchen role — one shared station user or several individual ones | See incoming items in one queue, start them, mark them ready, reject what cannot be made |
| **Admin / manager** | Logs in as a user with the Admin role | Maintain the menu: categories, items, prices, availability |

Guests are not users of the system in any technical sense. They have no login,
no role, no identifier, and no record. Scanning the QR code takes them to the
menu and nothing else.

##### 4. What we are building

###### 4.1 Guest menu (read-only)

A QR code at the table opens the menu on the guest's phone. The menu reflects
the live state of the kitchen: an item marked unavailable does not appear as
orderable. There is no cart, no submit button, no order history, and no status
view. The guest decides what they want and tells their server.

###### 4.2 Server order entry

A server creates an order, **binds it to a table**, and adds items to it. Every
item belongs to exactly one order, and every order belongs to exactly one table.
For any item, the server can attach a **free-form description** — "no onions,"
"medium rare," "allergy: shellfish," "split into two plates" — which the kitchen
sees verbatim on the item.

An open order is editable: the server can add items, void an item, cancel the
whole order, and move or merge an order between tables when guests change seats
or tables combine. When something is cancelled after the kitchen has already
started it, the kitchen is told explicitly rather than having the item silently
vanish from the queue.

###### 4.3 Kitchen queue

One undifferentiated queue. There is no routing to grill, fryer, or bar stations
in v1. Items arrive as they are sent, the kitchen works the queue, and each item
is advanced individually.

###### 4.4 Status model

Status is tracked **per item**. The order's status is **derived** from its items,
so nobody maintains it by hand.

Item lifecycle:

```
Ordered ──▶ In progress ──▶ Ready ──▶ Served
   │             │             │
   └──────┬──────┴─────────────┘
          ▼
   Cancelled / Rejected
```

Ownership of each transition follows who does the work:

| Transition | Who advances it |
| --- | --- |
| → Ordered (item sent to kitchen) | Server |
| Ordered → In progress | Kitchen |
| In progress → Ready | Kitchen |
| Ready → Served | Server |
| → Cancelled (guest changed their mind, server error) | Server |
| → Rejected (cannot be made, ran out mid-service) | Kitchen |

Nobody can advance a status that belongs to the other role. Derived order status
is the honest summary of the items: an order is Ready only when every
outstanding item is ready, and Served/Closed only when every item has been
served or removed.

###### 4.5 Item availability (86-ing)

Both **kitchen and servers** can mark a menu item unavailable, because both
discover it — the kitchen when the last portion is plated, the server when the
kitchen tells them across the pass. Marking an item unavailable removes it from
the guest menu immediately and blocks it from being added to new orders.

###### 4.6 Notifications

The platform pushes an alert to whoever owes the next action, rather than
expecting anyone to stare at a screen:

- Kitchen is alerted when new items are sent to the queue.
- Server is alerted when an item goes Ready, and when the kitchen rejects an
  item.
- Kitchen is alerted when an item they have started is cancelled.

###### 4.7 Menu management

Admins maintain a flat, minimal structure: **categories**, and within them items
with a name, description, and price. An item can be marked available or
unavailable. Modifiers, option groups, combos, dayparted menus, and scheduled
pricing are not in v1 — per-item free-form descriptions from the server cover
the real special-request cases at this scale.

###### 4.8 Totals, receipts, and settlement

Payment processing is **out of scope**. We take no card data and integrate with
no payment provider. We do produce the paperwork around the money:

- An **order total**, computed from the items actually on the order.
- A **printable/viewable receipt** for the order.
- A manual **"mark as paid"** action, recorded by the staff member who settles
  the check at whatever terminal or register the restaurant already uses.

The platform is the system of record for *what was ordered and what it cost*,
not for *how it was paid*.

##### 5. Explicitly out of scope for v1

Named and set aside so they do not creep in:

- Guest self-ordering from the phone
- Guest-visible order status
- Guest accounts, identifiers, or order history
- Card payment, tips, and tip-out
- Reservations and waitlist
- Loyalty and promotions
- Inventory depletion and food cost tracking
- Reporting, analytics, and dashboards
- POS, accounting, and third-party integrations
- Delivery, pickup, and off-premise orders
- Multi-location and multi-tenant support
- Per-station kitchen routing (grill / fryer / bar)

##### 6. What success looks like

The v1 bet is that item-level shared state removes a specific, countable set of
daily frictions. We will judge it on:

1. **Server trips to the kitchen to ask about an order** drop toward zero.
2. **Items sold after running out** drop toward zero, measured by rejected items
   attributed to unavailability.
3. **Re-made plates from a misread special request** decline, versus the paper
   ticket baseline.
4. **Time from Ready to Served** is short and consistent — food is not sitting
   under the lamp because nobody knew it was up.
5. Servers and kitchen staff, asked after a month of service, prefer it to paper
   and would not go back.

##### 7. Open questions and assumptions to confirm

1. **QR scope.** Because guests have no identifier and see no status, the QR code
   only needs to reach the menu — one restaurant-wide code would work. Assumed:
   per-table codes anyway, so the printed code at a table can later carry table
   context (and so guests at table 12 can't be handed the wrong thing). Confirm
   whether per-table codes are worth the printing overhead.
2. **"Orders linked to the table, items linked to the order."** Read that way
   from the brief. Confirm there is no case where an item needs to belong to
   something other than a single order (e.g. a shared appetizer across two
   checks).
3. **Splitting a check.** "Move or merge tables" is in scope; splitting one
   order into two checks was not discussed. Assumed out of v1.
4. **Who may mark an order paid.** Assumed any Server or Admin. Confirm whether
   this should be restricted.
5. **Void vs cancel wording.** Assumed a server-removed item and a
   kitchen-refused item are distinguished in the record (Cancelled vs Rejected)
   because the reasons differ operationally. Confirm that distinction is wanted.
6. **Hardware.** Server devices (personal phones vs restaurant handhelds) and
   the kitchen surface (wall tablet vs ticket printer) are undecided and will
   shape the kitchen queue design.
7. **Notification delivery.** In-app sound and badge is assumed. Whether
   anything needs to reach a device that is asleep or locked is unresolved.

### v6 (2026-09-21)

**Status:** Draft v1
**Date:** 2026-09-20
**Author:** Product Manager (drafted with Claude Opus 5)
**Scope:** Single restaurant, single location

---

##### 1. Vision statement

For a single dine-in restaurant, we will replace handwritten tickets and verbal
kitchen updates with one shared record of every order. Guests browse an
always-current menu on their own phone by scanning a QR code at the table.
Servers enter the order against a table under their own name, and the kitchen
receives it the moment it is sent. Each item carries its own status, so a server can answer "where is
my food?" by looking at a screen instead of walking into the kitchen, and the
kitchen never works from an ambiguous ticket.

We are deliberately not building a point-of-sale system. We do not process
payments, and we do not give guests an account, an identity, or a transactional
surface. The platform's job is to move an order accurately from the table to the
kitchen and to keep everyone honest about its state.

##### 2. The problem

In a dine-in restaurant, an order's real state lives in three places that
disagree: a paper ticket on the rail, the server's memory, and whatever the
kitchen has actually started cooking. That gap produces the daily failures this
product targets:

- Servers interrupt the kitchen to ask whether a dish is ready, and the kitchen
  loses time answering.
- Guests are told a wrong ETA because nobody can see item-level progress.
- An item is sold after it has run out, because "we're out of salmon" travels by
  word of mouth.
- A cancelled item keeps cooking, because the cancellation never reached the
  person at the pass.
- Handwriting and verbal special requests get misread, and the wrong plate goes
  out.

##### 3. Who this is for

| User | How they reach it | What they need |
| --- | --- | --- |
| **Guest** (anonymous, no account) | Scans the restaurant's QR code | Read the current menu, with prices, and see what is unavailable |
| **Server** | Handheld device, logged in as a user with the Server role | Enter an order against a table under their own name, attach details to an item, watch item progress, split and settle the check |
| **Kitchen staff** | Wall-mounted TV for the queue, paired tablet at the pass for input, logged in with the Kitchen role — typically one shared station user | See incoming items in one queue, start them, mark them ready, reject what cannot be made |
| **Admin / manager** | Logs in as a user with the Admin role | Maintain the menu: categories, items, prices, availability |

Guests are not users of the system in any technical sense. They have no login,
no role, no identifier, and no record. Scanning the QR code takes them to the
menu and nothing else.

##### 4. Why a restaurant would choose this

###### 4.1 What they would choose instead

Our target buyer is a single independent dine-in restaurant. Today they have four
realistic options, and we have to beat each on its own terms:

| Alternative | What it gets them | What it costs them |
| --- | --- | --- |
| **Paper tickets and shouting** (the real incumbent) | Free, zero setup, every member of staff already knows it | The five failure modes in section 2, every single service |
| **A full POS suite** (Toast, Square for Restaurants, Clover, Lightspeed) | Ordering, kitchen display, payments, reporting, everything | Monthly per-terminal fees, a cut of sales, proprietary hardware, a contract, switching payment processors, and retraining every employee |
| **A digital-menu SaaS** | A QR menu, cheaply | Solves only the menu; the kitchen coordination problem is untouched |
| **A kitchen display add-on** | A screen for the line | Generally only sold bolted onto a POS they would first have to adopt |

###### 4.2 Our answer

**We fix the coordination problem without asking them to replace their cash
register.** Because payment processing is deliberately out of scope, adopting us
requires no new merchant account, no processor switch, no contract, and no cut of
sales. That single exclusion is the product's commercial wedge, not a gap in it:
it turns a months-long POS migration into something a restaurant can try next
Tuesday and abandon on Wednesday at no cost.

Four reasons the choice holds up:

1. **Nothing to rip out.** They keep their existing register, processor, and
   whatever paperwork they already file. We sit alongside it and do the one job it
   does badly.
2. **Hardware they can buy anywhere.** Handhelds, a TV, and a tablet at the pass —
   consumer devices, not vendor-locked terminals. A web app installs nothing.
3. **Narrow on purpose, so it fits a small kitchen.** One undifferentiated queue,
   categories and items, free-form notes instead of a modifier matrix. A
   fifteen-table restaurant can be configured in an afternoon rather than
   onboarded over six weeks.
4. **Honest about state, which is the actual complaint.** Per-item status with
   role-split ownership means nobody has to walk to the kitchen to find out what is
   true. That is the daily pain, and it is what we are built around.

###### 4.3 Where this position is weak

Stated plainly, because a vision that only lists strengths is not useful:

- **A POS vendor could add this.** Our defence is fit and switching cost for one
  specific buyer, not technology. We do not out-engineer Toast; we are cheaper to
  try and do not touch their money.
- **A restaurant that wants one system will not want two.** Some buyers would
  rather have a single vendor for orders and payments, and we are a poor fit for
  them by design. Their existence is not a reason to widen scope.
- **Excluding payment means the check is settled twice** — marked paid here, taken
  there. That is genuine double entry, and the only honest mitigation is making
  mark-as-paid fast enough that nobody minds.
- **No reporting means no proof of value.** We are asking them to trust that
  service improved without showing them a number. Section 7's success measures are
  currently things we would have to observe by hand.

##### 5. What we are building

###### 5.1 Guest menu (read-only)

A **single QR code** for the restaurant opens the menu on the guest's phone; the
same code is printed on every table tent, so there is nothing per-table to
maintain or reprint. The menu reflects the live state of the kitchen: an item
marked unavailable does not appear as orderable. There is no cart, no submit
button, no order history, and no status view. The guest decides what they want
and tells their server.

###### 4.2 Server order entry

A server creates an order, **binds it to a table**, and is **recorded as the
order's server**. Every order therefore has two owners: the table it belongs to
and the staff member responsible for it. That attribution is what lets a server
pull up their own tables and lets the kitchen and managers see who to talk to
about an item. An order can be **handed off** to another server — at shift
change, or when someone covers a section — and the handoff is recorded, so
responsibility is always current and explicit rather than assumed.

The server adds items to the order; every item belongs to exactly one order. For
any item, the server can attach a **free-form description** — "no onions,"
"medium rare," "allergy: shellfish," "split into two plates" — which the kitchen
sees verbatim on the item.

An open order is editable: the server can add items, void an item, cancel the
whole order, and move or merge an order between tables when guests change seats
or tables combine. When something is cancelled after the kitchen has already
started it, the kitchen is told explicitly rather than having the item silently
vanish from the queue.

###### 4.3 Kitchen queue

One undifferentiated queue. There is no routing to grill, fryer, or bar stations
in v1. Items arrive as they are sent, the kitchen works the queue, and each item
is advanced individually.

###### 4.4 Status model

Status is tracked **per item**. The order's status is **derived** from its items,
so nobody maintains it by hand.

Item lifecycle:

```
Ordered ──▶ In progress ──▶ Ready ──▶ Served
   │             │             │
   └──────┬──────┴─────────────┘
          ▼
   Cancelled / Rejected
```

Ownership of each transition follows who does the work:

| Transition | Who advances it |
| --- | --- |
| → Ordered (item sent to kitchen) | Server |
| Ordered → In progress | Kitchen |
| In progress → Ready | Kitchen |
| Ready → Served | Server |
| → Cancelled (guest changed their mind, server error) | Server |
| → Rejected (cannot be made, ran out mid-service) | Kitchen |

Nobody can advance a status that belongs to the other role. Derived order status
is the honest summary of the items: an order is Ready only when every
outstanding item is ready, and Served/Closed only when every item has been
served or removed.

###### 4.5 Item availability (86-ing)

Both **kitchen and servers** can mark a menu item unavailable, because both
discover it — the kitchen when the last portion is plated, the server when the
kitchen tells them across the pass. Marking an item unavailable removes it from
the guest menu immediately and blocks it from being added to new orders.

###### 4.6 Notifications

The platform surfaces an alert to whoever owes the next action:

- Kitchen is alerted when new items are sent to the queue.
- Server is alerted when an item goes Ready, and when the kitchen rejects an
  item.
- Kitchen is alerted when an item they have started is cancelled.

Alerts are **in-app only** — a visible badge, a highlighted row, and a sound
while the app is open on the device. Nothing is pushed to a locked or sleeping
handheld, so no native app, platform push service, or per-device registration is
needed, and the whole thing can be a web app. The trade-off is real and belongs
on the record: a server whose handheld is asleep in their apron learns their food
is up only when they next look at the device. The kitchen surface is unaffected,
since the TV is always on and always showing the queue.

###### 4.7 Devices

Two very different surfaces, and the difference drives the design:

**Servers: handheld devices.** One-handed operation while standing, walking, and
carrying plates. Order entry, item statuses, splitting, and settlement all have
to work on a small screen. Because nothing is pushed to a dormant device, the
handheld is something a server actively checks between tables rather than
something that interrupts them.

**Kitchen: a TV plus a paired tablet at the pass.** The wall-mounted TV is the
display — the whole queue at a glance, readable from across a hot line at several
paces, so large type, high contrast, no small controls, no fine detail. The
**tablet at the pass is the input**: cooks advance items to In progress and Ready,
reject items, and mark things unavailable there, and the TV reflects it
immediately. This resolves what would otherwise be a contradiction, since a
television cannot accept the status transitions section 4.4 assigns to the
kitchen.

Because both kitchen surfaces are shared and always on, a single shared Kitchen
user is the practical default rather than individual cooks logging in and out
mid-service.

###### 4.8 Menu management

Admins maintain a flat, minimal structure: **categories**, and within them items
with a name, description, and price. An item can be marked available or
unavailable. Modifiers, option groups, combos, dayparted menus, and scheduled
pricing are not in v1 — per-item free-form descriptions from the server cover
the real special-request cases at this scale.

###### 4.9 Totals, receipts, splitting, and settlement

Payment processing is **out of scope**. We take no card data and integrate with
no payment provider. We do produce the paperwork around the money:

- An **order total**, computed from the items actually on the order.
- **Splitting a check** into any number of parts. A server chooses how to divide
  it: evenly across a stated number of parts, or by picking which items land on
  which part. An item does not have to go whole onto one part — **a single item
  can be divided across parts**, so a shared bottle of wine or a platter two
  guests split can be apportioned between their checks. A divided item is always
  split into **even shares** between the parts carrying it; there is no
  percentage or custom-amount control.
- **Rounding favours coverage and fairness.** When an even share does not divide
  cleanly, every share is **rounded up to the cent** so that the cost is fully
  covered and every guest pays the same amount. The consequence is deliberate:
  the parts can sum to slightly *more* than the order total (a $10.00 item split
  three ways bills $3.34 three times, collecting $10.02). We over-collect by
  cents rather than leaving the restaurant short or charging one guest a penny
  more than their neighbour.
- Splitting is a **settlement concern only**. The kitchen never sees it — one
  order remains one ticket no matter how the check is divided.
- A **printable/viewable receipt** — for the whole order, or one per split part.
  A part that carries a shared item shows the share it is paying for, so the
  guest can see why their line does not match the menu price.
- A manual **"mark as paid"** action, performed by a **server**, recorded against
  the staff member who did it. A split order is settled part by part, so a table
  where one guest has paid and another has not is an accurate state the system
  can hold rather than an edge case it forces the server to work around.
- **A paid part is final.** Once a part is marked paid, its items and its
  allocations are locked — money has changed hands outside the system, and the
  record has to match what the guest was charged. Reshuffling the rest of the
  check cannot reach back into a settled part.
- **An unpaid split can be rearranged freely.** Until a part is settled, the
  server can re-divide the check as many times as the table needs: change the
  number of parts, move items between them, and re-share a divided item. Guests
  change their minds about who is paying for what, and no money has moved yet, so
  the division is not a commitment until it is settled.

The platform is the system of record for *what was ordered, what it cost, and
which parts have been settled*, not for *how it was paid*.

##### 5. Explicitly out of scope for v1

Named and set aside so they do not creep in:

- Guest self-ordering from the phone
- Guest-visible order status
- Guest accounts, identifiers, or order history
- Card payment, tips, and tip-out
- Reservations and waitlist
- Loyalty and promotions
- Inventory depletion and food cost tracking
- Reporting, analytics, and dashboards
- POS, accounting, and third-party integrations
- Delivery, pickup, and off-premise orders
- Multi-location and multi-tenant support
- Per-station kitchen routing (grill / fryer / bar)

##### 6. What success looks like

The v1 bet is that item-level shared state removes a specific, countable set of
daily frictions. We will judge it on:

1. **Server trips to the kitchen to ask about an order** drop toward zero.
2. **Items sold after running out** drop toward zero, measured by rejected items
   attributed to unavailability.
3. **Re-made plates from a misread special request** decline, versus the paper
   ticket baseline.
4. **Time from Ready to Served** is short and consistent — food is not sitting
   under the lamp because nobody knew it was up.
5. Servers and kitchen staff, asked after a month of service, prefer it to paper
   and would not go back.

##### 7. Decisions and open questions

###### 7.1 Decided

Recorded so they are not relitigated:

- **One restaurant-wide QR code**, menu only. Guests have no account, no
  identifier, and no status view.
- **Cancelled vs Rejected are distinct states.** A server removing an item and
  the kitchen refusing one are different events with different reasons, and the
  record keeps them apart.
- **Splitting is invisible to the kitchen.** One order, one ticket, however the
  check divides.
- **Unpaid parts can be rearranged, settled parts cannot** — including on a
  partly settled order, where the unpaid remainder is re-split around the locked
  parts and shares of an already part-paid item do not change.
- **Servers use handheld devices. The kitchen uses a wall-mounted TV as the
  display and a paired tablet at the pass as the input**, which is what lets the
  kitchen own its status transitions.
- **Notifications are in-app only.** Nothing is pushed to a locked or sleeping
  device, which keeps the product a web app with no push infrastructure.

###### 7.2 Open

1. **How a server actually learns their food is up.** With no push to a dormant
   handheld, "the server is alerted when an item goes Ready" depends on the server
   looking at the device. Options that would close the gap: the app stays awake on
   the handheld during a shift, the kitchen keeps calling or belling the pass as
   they do today, or a runner works the expo. Worth resolving because success
   measure 4 (time from Ready to Served) and measure 1 (trips to the kitchen) both
   rest on this, and in-app-only alerts weaken both.
2. **Tablet-and-TV pairing.** How the pass tablet and the TV are bound (one
   shared Kitchen session driving both, or two clients of the same queue), and what
   the TV shows if the tablet is asleep or dead mid-service.
3. **Alert volume on the pass tablet.** A busy service generates a constant
   stream of items landing in the queue. Whether they batch, group by table, or
   throttle is unresolved, and an alert that fires on every item becomes noise the
   kitchen learns to ignore.

###### 7.3 Deferred by decision

Raised, consciously set aside for now, and cheap to revisit later:

- **Rounding overage disclosure.** Round-up over-collects a few cents per split
  item. Nothing extra will be shown on the receipt for now. Flagged rather than
  dropped because the amounts are real money, so it is worth a look from whoever
  owns tax and books before the restaurant runs it in production.
- **Receipt output format.** No printer support, on-screen only for now.

### v9 (2026-09-25)

**Status:** Draft v1
**Date:** 2026-09-20
**Author:** Product Manager (drafted with Claude Opus 5)
**Scope:** Single restaurant, single location

---

##### 1. Vision statement

**For** the owner-operator of a single independent dine-in restaurant, **whose**
servers and cooks lose time and accuracy every service because an order's real
state is split between a paper ticket, a server's memory, and whatever the kitchen
has actually started cooking, **Rail** is a table-to-kitchen ordering and status
platform **that** gives the floor, the line, and the office one shared item-level
record of every order, so staff stop chasing each other for answers and fewer
plates are remade or comped. **Unlike** a full POS suite, which bundles the same
coordination behind a payment processor, proprietary hardware, and a contract —
and unlike the paper tickets these restaurants still run on — **our product**
leaves payment deliberately out: it runs on commodity handhelds and screens,
changes nothing about how the restaurant takes money, and can be trialled next
service and abandoned at no cost.

> **"Rail"** is a placeholder name, after the ticket rail it replaces. Naming is
> not decided.

##### 2. The problem

In a dine-in restaurant, an order's real state lives in three places that
disagree: a paper ticket on the rail, the server's memory, and whatever the
kitchen has actually started cooking. That gap produces the daily failures this
product targets:

- Servers interrupt the kitchen to ask whether a dish is ready, and the kitchen
  loses time answering.
- Guests are told a wrong ETA because nobody can see item-level progress.
- An item is sold after it has run out, because "we're out of salmon" travels by
  word of mouth.
- A cancelled item keeps cooking, because the cancellation never reached the
  person at the pass.
- Handwriting and verbal special requests get misread, and the wrong plate goes
  out.

##### 3. Who this is for

| User | How they reach it | What they need |
| --- | --- | --- |
| **Guest** (anonymous, no account) | Scans the restaurant's QR code | Read the current menu, with prices, and see what is unavailable |
| **Server** | Handheld device, logged in as a user with the Server role | Enter an order against a table under their own name, attach details to an item, watch item progress, split and settle the check |
| **Kitchen staff** | Wall-mounted TV for the queue, paired tablet at the pass for input, logged in with the Kitchen role — typically one shared station user | See incoming items in one queue, start them, mark them ready, reject what cannot be made |
| **Admin / manager** | Logs in as a user with the Admin role | Maintain the menu: categories, items, prices, availability |

Guests are not users of the system in any technical sense. They have no login,
no role, no identifier, and no record. Scanning the QR code takes them to the
menu and nothing else.

Note the split between **who buys and who uses**. The Admin is the owner-operator
or manager who signs up, pays, and decides whether to keep the product; the
servers and kitchen staff are the ones whose daily pain it has to remove. Both
have to be satisfied, and they are not satisfied by the same things: the owner
needs a cheap, low-commitment fix that does not touch how the restaurant takes
money, while the staff need something faster than shouting across a pass. A
version that only pleases the buyer gets bought and then abandoned during service.

##### 4. Why a restaurant would choose this

###### 4.1 What they would choose instead

Our target buyer is a single independent dine-in restaurant. Today they have four
realistic options, and we have to beat each on its own terms:

| Alternative | What it gets them | What it costs them |
| --- | --- | --- |
| **Paper tickets and shouting** (the real incumbent) | Free, zero setup, every member of staff already knows it | The five failure modes in section 2, every single service |
| **A full POS suite** (Toast, Square for Restaurants, Clover, Lightspeed) | Ordering, kitchen display, payments, reporting, everything | Monthly per-terminal fees, a cut of sales, proprietary hardware, a contract, switching payment processors, and retraining every employee |
| **A digital-menu SaaS** | A QR menu, cheaply | Solves only the menu; the kitchen coordination problem is untouched |
| **A kitchen display add-on** | A screen for the line | Generally only sold bolted onto a POS they would first have to adopt |

###### 4.2 Our answer

**We fix the coordination problem without asking them to replace their cash
register.** Because payment processing is deliberately out of scope, adopting us
requires no new merchant account, no processor switch, no contract, and no cut of
sales. That single exclusion is the product's commercial wedge, not a gap in it:
it turns a months-long POS migration into something a restaurant can try next
Tuesday and abandon on Wednesday at no cost.

Four reasons the choice holds up:

1. **Nothing to rip out.** They keep their existing register, processor, and
   whatever paperwork they already file. We sit alongside it and do the one job it
   does badly.
2. **Hardware they can buy anywhere.** Handhelds, a TV, and a tablet at the pass —
   consumer devices, not vendor-locked terminals. A web app installs nothing.
3. **Narrow on purpose, so it fits a small kitchen.** One undifferentiated queue,
   categories and items, free-form notes instead of a modifier matrix. A
   fifteen-table restaurant can be configured in an afternoon rather than
   onboarded over six weeks.
4. **Honest about state, which is the actual complaint.** Per-item status with
   role-split ownership means nobody has to walk to the kitchen to find out what is
   true. That is the daily pain, and it is what we are built around.

###### 4.3 Where this position is weak

Stated plainly, because a vision that only lists strengths is not useful:

- **A POS vendor could add this.** Our defence is fit and switching cost for one
  specific buyer, not technology. We do not out-engineer Toast; we are cheaper to
  try and do not touch their money.
- **A restaurant that wants one system will not want two.** Some buyers would
  rather have a single vendor for orders and payments, and we are a poor fit for
  them by design. Their existence is not a reason to widen scope.
- **Excluding payment means the check is settled twice** — marked paid here, taken
  there. That is genuine double entry, and the only honest mitigation is making
  mark-as-paid fast enough that nobody minds.
- **No reporting means no proof of value.** We are asking them to trust that
  service improved without showing them a number. Section 7's success measures are
  currently things we would have to observe by hand.

##### 5. What we are building

###### 5.1 Guest menu (read-only)

A **single QR code** for the restaurant opens the menu on the guest's phone; the
same code is printed on every table tent, so there is nothing per-table to
maintain or reprint. The menu reflects the live state of the kitchen: an item
marked unavailable does not appear as orderable. There is no cart, no submit
button, no order history, and no status view. The guest decides what they want
and tells their server.

###### 5.2 Server order entry

A server creates an order, **binds it to a table**, and is **recorded as the
order's server**. Every order therefore has two owners: the table it belongs to
and the staff member responsible for it. That attribution is what lets a server
pull up their own tables and lets the kitchen and managers see who to talk to
about an item. An order can be **handed off** to another server — at shift
change, or when someone covers a section — and the handoff is recorded, so
responsibility is always current and explicit rather than assumed.

The server adds items to the order; every item belongs to exactly one order. For
any item, the server can attach a **free-form description** — "no onions,"
"medium rare," "allergy: shellfish," "split into two plates" — which the kitchen
sees verbatim on the item.

An open order is editable: the server can add items, void an item, cancel the
whole order, and move or merge an order between tables when guests change seats
or tables combine. When something is cancelled after the kitchen has already
started it, the kitchen is told explicitly rather than having the item silently
vanish from the queue.

###### 5.3 Kitchen queue

One undifferentiated queue. There is no routing to grill, fryer, or bar stations
in v1. Items arrive as they are sent, the kitchen works the queue, and each item
is advanced individually.

###### 5.4 Status model

Status is tracked **per item**. The order's status is **derived** from its items,
so nobody maintains it by hand.

Item lifecycle:

```
Ordered ──▶ In progress ──▶ Ready ──▶ Served
   │             │             │
   └──────┬──────┴─────────────┘
          ▼
   Cancelled / Rejected
```

Ownership of each transition follows who does the work:

| Transition | Who advances it |
| --- | --- |
| → Ordered (item sent to kitchen) | Server |
| Ordered → In progress | Kitchen |
| In progress → Ready | Kitchen |
| Ready → Served | Server |
| → Cancelled (guest changed their mind, server error) | Server |
| → Rejected (cannot be made, ran out mid-service) | Kitchen |

Nobody can advance a status that belongs to the other role. Derived order status
is the honest summary of the items: an order is Ready only when every
outstanding item is ready, and Served/Closed only when every item has been
served or removed.

###### 5.5 Item availability (86-ing)

Both **kitchen and servers** can mark a menu item unavailable, because both
discover it — the kitchen when the last portion is plated, the server when the
kitchen tells them across the pass. Marking an item unavailable removes it from
the guest menu immediately and blocks it from being added to new orders.

###### 5.6 Notifications

The platform surfaces an alert to whoever owes the next action:

- Kitchen is alerted when new items are sent to the queue.
- Server is alerted when an item goes Ready, and when the kitchen rejects an
  item.
- Kitchen is alerted when an item they have started is cancelled.

Alerts are **in-app only** — a visible badge, a highlighted row, and a sound
while the app is open on the device. Nothing is pushed to a locked or sleeping
handheld, so no native app, platform push service, or per-device registration is
needed, and the whole thing can be a web app. The trade-off is real and belongs
on the record: a server whose handheld is asleep in their apron learns their food
is up only when they next look at the device. The kitchen surface is unaffected,
since the TV is always on and always showing the queue.

###### 5.7 Devices

Two very different surfaces, and the difference drives the design:

**Servers: handheld devices.** One-handed operation while standing, walking, and
carrying plates. Order entry, item statuses, splitting, and settlement all have
to work on a small screen. Because nothing is pushed to a dormant device, the
handheld is something a server actively checks between tables rather than
something that interrupts them.

**Kitchen: a TV plus a paired tablet at the pass.** The wall-mounted TV is the
display — the whole queue at a glance, readable from across a hot line at several
paces, so large type, high contrast, no small controls, no fine detail. The
**tablet at the pass is the input**: cooks advance items to In progress and Ready,
reject items, and mark things unavailable there, and the TV reflects it
immediately. This resolves what would otherwise be a contradiction, since a
television cannot accept the status transitions section 5.4 assigns to the
kitchen.

Because both kitchen surfaces are shared and always on, a single shared Kitchen
user is the practical default rather than individual cooks logging in and out
mid-service.

###### 5.8 Menu management

Admins maintain a flat, minimal structure: **categories**, and within them items
with a name, description, and price. An item can be marked available or
unavailable. Modifiers, option groups, combos, dayparted menus, and scheduled
pricing are not in v1 — per-item free-form descriptions from the server cover
the real special-request cases at this scale.

###### 5.9 Totals, receipts, splitting, and settlement

Payment processing is **out of scope**. We take no card data and integrate with
no payment provider. We do produce the paperwork around the money:

- An **order total**, computed from the items actually on the order. Prices are
  **tax-inclusive**: the price on the menu is the price the guest pays, so no tax or
  service charge is calculated, apportioned, or shown anywhere. No tax rate is stored,
  so a rate change is absorbed by re-pricing the menu.
- **Splitting a check** into any number of parts. A server chooses how to divide
  it: evenly across a stated number of parts, or by picking which items land on
  which part. An item does not have to go whole onto one part — **a single item
  can be divided across parts**, so a shared bottle of wine or a platter two
  guests split can be apportioned between their checks. A divided item is always
  split into **even shares** between the parts carrying it; there is no
  percentage or custom-amount control.
- **Rounding favours coverage and fairness.** When an even share does not divide
  cleanly, every share is **rounded up to the cent** so that the cost is fully
  covered and every guest pays the same amount. The consequence is deliberate:
  the parts can sum to slightly *more* than the order total (a $10.00 item split
  three ways bills $3.34 three times, collecting $10.02). We over-collect by
  cents rather than leaving the restaurant short or charging one guest a penny
  more than their neighbour.
- Splitting is a **settlement concern only**. The kitchen never sees it — one
  order remains one ticket no matter how the check is divided.
- A **printable/viewable receipt** — for the whole order, or one per split part.
  A part that carries a shared item shows the share it is paying for, so the
  guest can see why their line does not match the menu price.
- A manual **"mark as paid"** action, performed by a **server**, recorded against
  the staff member who did it. A split order is settled part by part, so a table
  where one guest has paid and another has not is an accurate state the system
  can hold rather than an edge case it forces the server to work around.
- **A paid part is final.** Once a part is marked paid, its items and its
  allocations are locked — money has changed hands outside the system, and the
  record has to match what the guest was charged. Reshuffling the rest of the
  check cannot reach back into a settled part.
- **An unpaid split can be rearranged freely.** Until a part is settled, the
  server can re-divide the check as many times as the table needs: change the
  number of parts, move items between them, and re-share a divided item. Guests
  change their minds about who is paying for what, and no money has moved yet, so
  the division is not a commitment until it is settled.

The platform is the system of record for *what was ordered, what it cost, and
which parts have been settled*, not for *how it was paid*.

##### 6. Explicitly out of scope for v1

Named and set aside so they do not creep in:

- Guest self-ordering from the phone
- Guest-visible order status
- Guest accounts, identifiers, or order history
- Card payment, tips, and tip-out
- Reservations and waitlist
- Loyalty and promotions
- Inventory depletion and food cost tracking
- Reporting, analytics, and dashboards
- POS, accounting, and third-party integrations
- Delivery, pickup, and off-premise orders
- Multi-location and multi-tenant support
- Per-station kitchen routing (grill / fryer / bar)

##### 7. What success looks like

The v1 bet is that item-level shared state removes a specific, countable set of
daily frictions. We will judge it on:

1. **Server trips to the kitchen to ask about an order** drop toward zero.
2. **Items sold after running out** drop toward zero, measured by rejected items
   attributed to unavailability.
3. **Re-made plates from a misread special request** decline, versus the paper
   ticket baseline.
4. **Time from Ready to Served** is short and consistent — food is not sitting
   under the lamp because nobody knew it was up.
5. Servers and kitchen staff, asked after a month of service, prefer it to paper
   and would not go back.

##### 8. Decisions and open questions

###### 8.1 Decided

Recorded so they are not relitigated:

- **One restaurant-wide QR code**, menu only. Guests have no account, no
  identifier, and no status view.
- **Cancelled vs Rejected are distinct states.** A server removing an item and
  the kitchen refusing one are different events with different reasons, and the
  record keeps them apart.
- **Splitting is invisible to the kitchen.** One order, one ticket, however the
  check divides.
- **Unpaid parts can be rearranged, settled parts cannot** — including on a
  partly settled order, where the unpaid remainder is re-split around the locked
  parts and shares of an already part-paid item do not change.
- **Servers use handheld devices. The kitchen uses a wall-mounted TV as the
  display and a paired tablet at the pass as the input**, which is what lets the
  kitchen own its status transitions.
- **Notifications are in-app only.** Nothing is pushed to a locked or sleeping
  device, which keeps the product a web app with no push infrastructure.
- **Menu prices are tax-inclusive.** An order total is the sum of its items, with no
  tax or service charge line anywhere in the product.

###### 8.2 Open

1. **How a server actually learns their food is up.** With no push to a dormant
   handheld, "the server is alerted when an item goes Ready" depends on the server
   looking at the device. Options that would close the gap: the app stays awake on
   the handheld during a shift, the kitchen keeps calling or belling the pass as
   they do today, or a runner works the expo. Worth resolving because success
   measure 4 (time from Ready to Served) and measure 1 (trips to the kitchen) both
   rest on this, and in-app-only alerts weaken both.
2. **Tablet-and-TV pairing.** How the pass tablet and the TV are bound (one
   shared Kitchen session driving both, or two clients of the same queue), and what
   the TV shows if the tablet is asleep or dead mid-service.
3. **Alert volume on the pass tablet.** A busy service generates a constant
   stream of items landing in the queue. Whether they batch, group by table, or
   throttle is unresolved, and an alert that fires on every item becomes noise the
   kitchen learns to ignore.

###### 8.3 Deferred by decision

Raised, consciously set aside for now, and cheap to revisit later:

- **Rounding overage disclosure.** Round-up over-collects a few cents per split
  item. Nothing extra will be shown on the receipt for now. Flagged rather than
  dropped because the amounts are real money, so it is worth a look from whoever
  owns tax and books before the restaurant runs it in production.
- **Receipt output format.** No printer support, on-screen only for now.
