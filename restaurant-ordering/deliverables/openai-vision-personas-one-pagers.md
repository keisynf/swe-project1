# Product Vision, Personas, and 1-Pagers

**Product:** Restaurant Ordering & Status Platform
**Model:** gpt-5.6-terra
**Students:** Keisy Núñez and Ezequiel Buck
**Course:** CS 3365, Fall 2026, Project 1

---

## Product Vision

For the owner-operator of an independent casual-dining restaurant, whose staff now reconcile paper tickets, verbal updates, and separate menu records that leave orders and availability out of sync, the Restaurant Ordering and Status Platform is a standalone restaurant-operations application. It gives the floor and kitchen current orders and menu availability in one place, so they can prepare, deliver, and complete service with fewer avoidable handoffs and mistakes. Unlike a full point-of-sale suite, which a small independent restaurant may choose for payments and back-office tools, our product focuses on daily order and service coordination without payment processing or unrelated POS complexity.

The owner-operator buys the platform to standardize service without paying for a broader point-of-sale system the restaurant does not use. They keep paying because new staff can learn it quickly, menu and table information is straightforward to maintain, and its cost remains proportionate to one restaurant’s needs.

---

## Personas

Maya Patel is a 29-year-old marketing coordinator who meets friends for casual dinners after work and often checks a restaurant's menu before the server reaches the table. She has a bachelor's degree in communications and is comfortable using everyday mobile apps for travel, shopping, and restaurant research, though she does not consider herself technical. After a full workday, Maya wants to make a choice quickly rather than spend the start of a meal asking staff for basic information.

Maya would use the product by scanning the restaurant's QR code before ordering, then looking through the categories, reading dish descriptions, checking prices and options, and seeing what is currently available. She wants to settle on an order before the server arrives so that she can spend more time with her friends and less time comparing choices aloud at the table.

---

Daniel Ruiz is a 35-year-old career server who supports his partner and young child by working busy lunch and dinner shifts at the restaurant. His job involves welcoming guests, coordinating their requests with the kitchen, keeping track of several tables, delivering food, and bringing bills at the end of service. Daniel completed a community-college hospitality certificate and is highly comfortable with point-of-sale terminals, phones, and workplace software because he uses them throughout every shift. Reliable tools help him finish busy shifts on time and avoid carrying preventable mistakes into his family time.

Daniel would use the product to choose a table when he starts an order, add the dishes and options a guest requests, see when food can be taken out, and record that it reached the guest. During service, he would use it to take unavailable dishes off the menu, understand why the kitchen cannot make an item, cancel a mistaken request, and create the final bill. He wants one place to check these details instead of switching between memory, paper tickets, and questions to the kitchen.

---

Priya Nair is a 42-year-old line cook who has worked in casual restaurants for nearly two decades. Her job involves preparing dishes during busy service periods, following requests from the front of house, coordinating with other cooks, and communicating when the kitchen cannot fulfill a request. Priya completed a culinary certificate after high school and has practical, moderate technical skill: she is comfortable with phones and common workplace devices but expects technology to be direct, durable, and quick to use while cooking.

Priya would use the shared kitchen screen to see the next dishes to make and the options attached to each one, then update the screen as food moves through the line. When ingredients run out, she would hide the affected dish from new orders; when an existing request cannot be made, she would explain why for the server. She also needs a clear on-screen interruption when a server cancels food that she has already started so she can stop work before wasting ingredients.

---

Elena Torres is a 47-year-old owner-operator of the restaurant who makes its spending and operating decisions while caring for an elderly parent outside work. Her job includes running daily service, maintaining the menu, training staff, resolving customer issues, and deciding which tools the restaurant pays to keep. Elena earned an associate degree in business management and is technically capable with spreadsheets, scheduling systems, and restaurant software, although she has little patience for systems that require duplicate entry or specialist support for routine changes. She needs the restaurant's administration work to stay within her shift so it does not take time away from her caregiving responsibilities.

Elena would use the product herself to update dishes, prices, availability, options, and tables before or during service. As the buyer, she would adopt and keep paying for it if she sees fewer ordering mistakes, less time spent relaying information between staff, quicker training for new servers, and smoother service for guests. She would drop it if staff work around it, menu and table changes do not reach everyone, or maintaining it adds more time and cost than it saves.

---

Marcus Lee is a 21-year-old community-college student who has just started his first restaurant job while studying part-time for an associate degree in graphic design. As a new server, his job involves learning the restaurant's service rhythm, greeting guests, recording requests, coordinating with the kitchen, delivering food, and helping close out service. Marcus is confident with smartphones and online tools but has little experience with restaurant systems. Because he balances classes with short work shifts, he needs to become useful quickly rather than wait through several weeks of gradual training.

Marcus would use the product to choose a table, enter a guest's dishes and options, check whether something can still be ordered, watch for kitchen updates, record that food has reached a guest, and produce a bill with help from a trainer when needed. On his first day, he would find it hardest to learn how table selection connects to a new order, when he should change or remove an item, how to interpret a kitchen message, and when an order is ready to bill. He needs the routine flow to be easy enough to learn in one day while knowing which exceptions require a more experienced coworker.

---

## 1-Pagers

### Guest Menu and Availability 1-pager

#### PROBLEM

When Maya arrives for dinner, she wants to scan the restaurant’s QR code, see what can actually be ordered, and decide before the server comes to the table. If the menu is slow, omits descriptions or prices, or shows an item that the kitchen has run out of, she must ask staff for information that the menu should already provide. That wastes time for Maya and creates avoidable work for Daniel and Priya during service.

Elena needs to maintain the menu once and have every person use the same current information. Daniel and Priya also need to remove an unavailable item during a shift, while Marcus needs to recognize that an item cannot be added before he records a guest’s request. The capability must update the guest menu and order-entry view consistently without changing items that were already ordered.

#### ASSUMPTIONS

- At the 95th percentile, a supported phone on a stable 4G or Wi-Fi connection renders the available menu categories and items within **2 seconds** of opening the generic QR-code URL. This is an initial target and requires validation with the restaurant and representative devices and networks.
- On a stable network connection, an availability change appears in the relevant active guest and server views within **3 seconds at the 95th percentile**, measured from confirmation of the change to display of the result. This proposed target requires validation before implementation.
- This release has no search, filter, or image capability. The ordering of categories and items and the presentation of modifiers must be confirmed with Elena before implementation.
- An unavailable item remains on an existing order unchanged. Priya rejects the existing item only if the kitchen cannot fulfill it; changing availability does not automatically reject it.

#### FUNCTIONAL REQUIREMENTS

- **As Maya, I want to open the generic QR-code menu and browse available categories and items so that I can decide what to ask Daniel to order without waiting for basic menu or availability information.**

  - Maya can access the view-only menu without an account or login.
  - The generic QR code identifies neither Maya nor her table.
  - The menu shows available categories and available items, including each item’s name, description, tax- and service-inclusive price, and modifiers.
  - The menu does not let Maya create or modify an order, see an order status, access a bill, or make a payment.

- **As Elena, I want to maintain menu categories, items, descriptions, prices, modifiers, and availability in the administrator view so that the restaurant can keep one current menu without duplicate entry or an external system.**

  - Elena can manage categories, item names, descriptions, tax- and service-inclusive prices, modifiers, and availability from the administrator view.
  - The product stores no tax rate and does not calculate tax or service charges separately.
  - Dietary information is not included in this release.
  - An item’s availability change is reflected in the guest menu and server order-entry view under the availability-update assumption.

- **As Daniel, I want to mark an item unavailable from the server view so that I do not take a new order for something the restaurant cannot provide.**

  - Daniel can toggle availability from the server view without access to the administrator view.
  - An unavailable item is removed from the guest menu and cannot be added to a new order.
  - Daniel’s availability change does not alter an item already on an order.

- **As Priya, I want to mark an item unavailable from the kitchen view so that new orders stop requesting an item the kitchen cannot make.**

  - Priya can toggle availability from the kitchen view without access to the administrator view.
  - An unavailable item is removed from the guest menu and cannot be added to a new order.
  - Priya rejects an existing ordered item only when the kitchen cannot fulfill it.

- **As Marcus, on my first server shift, I want to recognize when an item is unavailable before I enter a guest’s request so that I do not promise food the kitchen cannot make.**

  - The server order-entry view identifies currently unavailable items.
  - Marcus cannot add an unavailable item to a new order.
  - Marcus can use the same availability information that Maya sees in the guest menu.

#### NON-FUNCTIONAL REQUIREMENTS

- **Mobile menu performance:** Under the mobile-performance assumption, at least 95% of supported-device test runs render the available categories and items within 2 seconds after opening the QR-code URL. Verify this with timestamped browser tests on representative supported phones and stable 4G or Wi-Fi connections.
- **Availability freshness:** Under the availability-update assumption, at least 95% of tested availability changes appear in active guest and server views within 3 seconds, without reopening a view. Verify this with timestamped end-to-end tests.
- **Availability integrity:** Automated integration tests must prevent an unavailable item from being added to a new order while preserving the same item on orders created before the availability change.

#### REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Maya browses the generic QR menu | 8 | Requires a mobile view-only menu, QR entry point, categories, item details, modifiers, availability display, and responsive testing. The mobile performance target adds cross-device verification. |
| Elena maintains menu information | 8 | Requires administrator workflows for several related menu attributes, validation, persistence, and propagation to the guest and server views. The work spans a central data model and multiple views. |
| Daniel toggles availability | 3 | Reuses the shared availability capability but requires a server-view control, permission enforcement, propagation, and tests. |
| Priya toggles availability | 3 | Reuses the shared availability capability but requires the kitchen-view control and kitchen-specific permission coverage. |
| Marcus recognizes unavailable items | 3 | Reuses the availability data but requires deliberate server-view presentation and first-shift usability validation. |

### Server Order Entry 1-pager

#### PROBLEM

When Daniel takes a table’s order during a busy shift, he needs to select the correct active table and record the dishes and modifiers the guests chose from the current menu. If he cannot see whether an item is available or the table selection is unclear, he can create an order that the kitchen cannot fulfill or attach it to the wrong table. The product needs one accurate starting record for each order before Priya receives its items in the kitchen queue.

Marcus faces the same workflow without Daniel’s experience. On his first day, he needs to understand how choosing a table relates to a new order, recognize that he can only choose available items, and enter standard guest requests without asking a coworker to complete every step. Exceptions such as a rejection or cancellation remain in the kitchen and item-status workflow rather than becoming an unscoped order-editing feature here.

#### ASSUMPTIONS

- When Daniel or Marcus creates an order item, the system assigns it the `placed` state and associates it with exactly one selected active table. The item lifecycle that follows is defined in the Kitchen Queue and Item Status 1-pager.
- Each new order starts with one or more item entries. Because the bill must list quantities, this epic assumes a server records a positive quantity for each selected item; the default quantity, quantity-entry interaction, and maximum quantity require confirmation before implementation.
- For first-shift usability testing, an 80% passing rate is an initial target that requires validation with Elena and servers before implementation.
- Editing modifiers after creation, splitting an order, moving an order between tables, and merging orders are outside this release.

#### FUNCTIONAL REQUIREMENTS

- **As Daniel, I want to select one active table when I create an order so that every order is associated with the table I am serving.**

  - Daniel selects exactly one table from the active table list for each new order.
  - Daniel cannot create a new order without selecting a table.
  - Daniel cannot select a deactivated table for a new order.

- **As Daniel, I want to add available menu items, their selected modifiers, and quantities to the table’s order so that Priya receives an accurate request to prepare.**

  - Daniel selects the current menu items offered by the order-entry view.
  - Daniel records the modifiers selected for each item.
  - Daniel records a positive quantity for each item under the quantity-entry assumption.
  - Each newly created order item begins in `placed`.

- **As Daniel, I want to add items to an order that is already open so that later guest requests reach Priya as new kitchen work without replacing the existing order.**

  - Daniel can add current menu items, selected modifiers, and positive quantities to an order that is not `closed`.
  - Each added item is a new item on the existing order and begins in `placed`.
  - Adding an item does not change the existing items, their modifiers, quantities, or table association.

- **As Marcus, on my first server shift, I want to create a standard order by choosing a table and available guest requests so that I can become useful during service without relying on a coworker for every routine order.**

  - Marcus can distinguish active tables from tables that are not available for new orders.
  - Marcus uses the current menu items offered by the order-entry view.
  - The routine flow presents table selection before the item entries and selected modifiers.
  - Exceptions outside the routine flow, including rejection and cancellation, remain visible through the item-status workflow.

#### NON-FUNCTIONAL REQUIREMENTS

- **Order-entry integrity:** Automated integration tests must reject creating an order without exactly one active table, recording a non-positive quantity, or creating an item without the `placed` state.
- **First-shift usability:** Under the 80% initial usability target, at least 80% of representative new-server participants can create a sample order for an active table with a current menu item and modifier without selecting a deactivated table. Verify this in a moderated usability test.
- **Order persistence:** End-to-end tests must confirm that items created with a new order or added to an open order present the same table label, items, modifiers, and quantities to the server workflow and the kitchen queue without re-entry by either role.

#### REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Daniel selects an active table for a new order | 5 | Requires the new-order workflow, active-table query and validation, persistence of the selected table, and tests for deactivated-table rejection. |
| Daniel adds available items, modifiers, and quantities | 8 | Requires menu selection in the server workflow, availability validation, modifier and quantity capture, placed-state creation, persistence, and kitchen-facing verification. |
| Daniel adds items to an open order | 5 | Requires an open-order update path, creation of distinct placed items, preservation of existing items and table association, kitchen propagation, and tests. |
| Marcus creates a standard first-shift order | 3 | Reuses the core order-entry flow but needs deliberate sequencing and moderated usability validation for a new server. |

### Kitchen Queue and Item Status 1-pager

#### PROBLEM

During a busy shift, Priya needs to see every dish the servers have placed, including its modifiers and table, and update it as kitchen work begins and finishes. Daniel needs the same record to tell whether food is still waiting, being prepared, ready to carry out, or cannot be fulfilled. Without that shared record, Priya is interrupted for status checks and Daniel has to rely on verbal updates, increasing the chance that the kitchen makes the wrong dish or a table receives an inaccurate update.

The workflow must also make sense to Marcus on his first shift. He needs to understand which item states describe kitchen work, which action belongs to a server, and when a kitchen rejection means that he needs help responding to a table. If Daniel cancels work that Priya has already started or marked ready, Priya needs a visible in-app alert at the shared kitchen station so that the kitchen can stop or avoid unnecessary work.

#### ASSUMPTIONS

- The kitchen queue lists active items in the order that servers place them. This release has no prioritization, manual reordering, course firing, expedite controls, or table grouping.
- Active queue items are items in `placed`, `preparing`, or `ready`. Items in `canceled`, `rejected`, or `delivered` leave the active queue but remain in the order history.
- Each queue item shows its dish name, selected modifiers, and the table label of its order.
- The shared Kitchen login identifies the kitchen station, not an individual cook.
- Kitchen cancellation alerts are visual, in-app alerts. They do not require acknowledgement before other kitchen work can continue.
- On a stable network connection, a successful item-status or rejection-reason change appears in each relevant active application view within **3 seconds at the 95th percentile**, measured from confirmation of the change to display of the result. The target requires validation with the restaurant before implementation.
- For first-shift usability testing, the restaurant’s normal onboarding content, a six-item sample, and an 80% passing rate are provisional and require validation with the owner-operator and servers before implementation.
- The system derives each order status from its item states. A *fulfillable item* is one that is neither `canceled` nor `rejected`. The rules below are evaluated in order and the first match applies, except that `closed`, set as described in the Service Completion and Billing 1-pager, overrides the derived status:
  1. `rejected`: every item is `rejected`.
  2. `canceled`: no fulfillable item remains, and at least one item is `canceled`.
  3. `delivered`: at least one fulfillable item exists, and every fulfillable item is `delivered`.
  4. `ready`: at least one fulfillable item is `ready`, and every fulfillable item is `ready` or `delivered`. For example, delivered drinks and ready mains produce `ready`.
  5. `placed`: at least one fulfillable item exists, and every fulfillable item is `placed`.
  6. `preparing`: any other combination that has at least one fulfillable item.

#### FUNCTIONAL REQUIREMENTS

- **As Priya, I want to see active ordered items with their selected modifiers and table labels in a kitchen queue so that I can prepare the correct dishes without interrupting kitchen work.**

  - The queue shows every active item, its dish name, selected modifiers, and the associated table label.
  - The queue presents active items in the ordering described in the assumptions.
  - Priya can move an item from `placed` to `preparing` and from `preparing` to `ready`.
  - Priya cannot set an item to `delivered` or `canceled`.

- **As Priya, I want to reject an undelivered item that the kitchen cannot fulfill and optionally explain why so that Daniel can respond to the table accurately.**

  - Priya can reject an item before it is delivered only when the kitchen cannot fulfill it.
  - A rejection is terminal; the item cannot move to another state afterward.
  - Priya may enter an optional free-text rejection reason.
  - Daniel can see the rejection and its optional reason in the server view.

- **As Priya, I want an in-app alert when Daniel cancels an item that is preparing or ready so that the kitchen can stop or avoid unnecessary work.**

  - The kitchen receives an in-app alert when a server cancels an item whose current state is `preparing` or `ready`.
  - The alert appears only in the active kitchen application and is not pushed to a locked or sleeping device.
  - A canceled item is terminal and is no longer fulfillable.

- **As Daniel, I want to see each item’s current state, including a kitchen rejection and its reason, so that I can give tables accurate updates without repeated verbal checks with the kitchen.**

  - Daniel can see whether each item is `placed`, `preparing`, `ready`, `delivered`, `canceled`, or `rejected`.
  - Daniel can see an optional rejection reason entered by Priya.
  - The system derives the order state from its item states; Daniel cannot set an order state directly.
  - The displayed order state follows the order-status precedence rules in the assumptions, including `ready` when fulfillable items are all `ready` or `delivered` and at least one is `ready`.

- **As Daniel, I want to mark a ready item delivered and cancel an undelivered item when necessary so that the record reflects the service handoff to the table.**

  - Daniel can move only a `ready` item to `delivered`.
  - Daniel can cancel an item before it is delivered.
  - Canceling an item that is `preparing` or `ready` triggers the kitchen alert described above.
  - Daniel cannot move an item to `preparing`, `ready`, or `rejected`.

- **As Marcus, on my first server shift, I want the server view to distinguish kitchen-owned item states from the delivery action assigned to me so that I can use the shared record without changing kitchen work by mistake.**

  - Marcus can distinguish items waiting for kitchen work, being prepared, ready for delivery, delivered, canceled, and rejected in the server view.
  - The server view offers the delivery action only for ready items and does not offer kitchen-owned preparation or rejection actions.
  - The view identifies a rejection and its optional reason so Marcus knows that an item needs a table-facing response or help from a more experienced coworker.

#### NON-FUNCTIONAL REQUIREMENTS

- **Shared-state freshness:** Under the shared-state update assumption, at least 95% of tested item-status and rejection-reason changes appear in every relevant active kitchen and server view within 3 seconds. Verify this with timestamped end-to-end tests for each change type, without reopening a view.
- **First-shift usability:** Under the first-shift usability assumption, at least 80% of representative new-server participants can correctly identify six sample item states, identify a rejection reason, and mark a ready item delivered without attempting a kitchen-only action. Verify this in a moderated usability test.
- **State integrity:** Automated integration tests must reject invalid state transitions, including a non-kitchen attempt to set `preparing`, `ready`, or `rejected`; delivery of a non-ready item; and any transition from `canceled` or `rejected` to another state.

#### REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Priya views the queue and changes preparation states | 8 | Requires a kitchen queue view, modifier and table-label display, two kitchen-owned transitions, state validation, and tests. The shared-state display and update path span several related behaviors. |
| Priya rejects unfulfillable items with an optional reason | 5 | Adds a terminal transition, optional text capture, server visibility, validation, and tests across the kitchen and server views. The workflow is bounded but crosses roles. |
| Priya receives cancellation alerts | 5 | Requires detection of the canceled item’s prior state, an in-app alert at the kitchen station, and tests for preparing and ready items. Alert presentation details are still assumed. |
| Daniel views item and derived order status | 8 | Requires a server status view, rejection-reason display, and correct application of the precedence-based order-status rules across mixed item states. Shared updates and lifecycle coverage add test complexity. |
| Daniel delivers ready items and cancels undelivered items | 5 | Adds server-owned transitions, permission checks, terminal-state handling, and the connection to kitchen alerts. It spans server and kitchen behaviors but follows a defined workflow. |
| Marcus uses the first-shift server workflow | 3 | Reuses the status and delivery capabilities but needs deliberate presentation and usability-test support so a new server can recognize states and allowed actions. It does not introduce a training subsystem. |

### Service Completion and Billing 1-pager

#### PROBLEM

After food has reached the table, Daniel needs a reliable final bill without returning to paper notes or manually recalculating totals. The bill must reflect the items, modifiers, quantities, and tax- and service-inclusive prices that were actually ordered. Daniel also needs a clear completion step that distinguishes delivering food from finishing billing work, because a delivered order is not fully complete until the final bill has been generated and the order is closed. When no fulfillable item remains because every item was canceled or rejected, Daniel instead needs to close the order without generating a bill.

Marcus needs to recognize when an ordinary order has reached that point in service. On his first shifts, he can generate a bill, but the application must not suggest that it processed a payment or that a closed order can still receive item changes. Elena benefits when staff can close service consistently without an extra payment system or external point-of-sale integration.

#### ASSUMPTIONS

- The final bill is generated and viewed within the application. Printing, emailing, exporting, and providing guests direct bill access are outside this release.
- Generating a final bill does not process payment, suggest a tip, calculate tax or service charges, or store a tax rate.
- For first-shift billing usability testing, an 80% passing rate is an initial target that requires validation with Elena and servers before implementation.
- A closed order is final: it cannot receive further item-state changes. An order whose derived status is `canceled` or `rejected` may close without a bill. Archival, deletion, reopening, refunds, and post-close corrections are outside this release.

#### FUNCTIONAL REQUIREMENTS

- **As Daniel, I want to generate a server-only final bill for an order so that I can present an accurate total after service without manual calculation.**

  - Only Daniel’s Server role can generate or view the bill.
  - Daniel can generate and regenerate the bill at any time before closing the order.
  - Each generated bill reflects the order’s current items, selected modifiers, quantities, and tax- and service-inclusive prices at the time of generation.
  - The bill lists ordered items, selected modifiers, quantities, and the total.
  - Item prices and the total include tax and service.
  - The bill shows no separate tax or service amount, includes no tip suggestion, and does not process payment.

- **As Daniel, I want to close a delivered, canceled, or rejected order under its applicable completion rule so that the order record distinguishes completed food service, terminal exceptions, and billing work.**

  - Daniel can close an order when its derived status is `delivered` and a bill has been generated after the most recent item change.
  - Daniel can close an order whose derived status is `canceled` or `rejected` without generating a bill.
  - `closed` overrides the otherwise derived order status.
  - A closed order cannot receive further item changes.
  - Closing an order does not indicate that payment was processed.

- **As Marcus, on my first server shift, I want to recognize when an order is ready for the billing step and generate a bill so that I can complete routine service without confusing delivery with payment.**

  - Marcus can see that closing an ordinary order becomes available only after the order is delivered and a current bill has been generated.
  - Marcus can generate the server-only bill.
  - The workflow makes clear that bill generation and order closure do not collect payment.

#### NON-FUNCTIONAL REQUIREMENTS

- **Bill calculation integrity:** Automated integration tests must verify that every generated bill contains the current ordered items, selected modifiers and quantities, and a total equal to the sum of the included tax- and service-inclusive item prices. The tests must also verify that regeneration after an item change updates the bill and that no separate tax, service, or tip amount appears.
- **Closure integrity:** Automated integration tests must permit closing a delivered order only after a bill has been generated after its most recent item change, permit bill-free closure only when the derived order status is `canceled` or `rejected`, and reject item changes after closure.
- **Billing-flow usability:** Under the 80% initial usability target, at least 80% of representative new-server participants can identify a delivered sample order as ready to bill and close and explain that the resulting bill does not process payment. Verify this in a moderated usability test.

#### REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Daniel generates and regenerates a server-only bill | 8 | Requires bill composition from current items, modifiers, quantities, and inclusive prices; Server-only access; regeneration after item changes; a timestamp comparison for stale-bill detection; and accuracy tests. The timestamp check extends the existing bill workflow without adding a separate lifecycle subsystem. |
| Daniel closes a delivered, canceled, or rejected order | 8 | Requires separate completion validation for delivered-and-billed, canceled, and rejected orders; verification that a delivered order’s bill follows its final item change; the closed final state; prevention of later item changes; and integration tests for each path. |
| Marcus completes the first-shift billing workflow | 3 | Reuses bill and closure capabilities but requires clear eligibility cues, payment-boundary language, and moderated usability validation for a new server. |

### Table Administration and Role Access 1-pager

#### PROBLEM

Before service, Elena needs to keep a clear list of the restaurant’s tables so that servers can attach each new order to the correct place and staff can still identify a table on an older order. Reused or ambiguous table labels create mistakes during a busy shift. Deleting a table would also make an existing order harder to understand, so Elena needs a way to stop using a table for new service without losing its historical identity.

The shared application also needs to present the right workflow to each person. Priya uses a shared kitchen station, Daniel and Marcus use the server workflow, Elena uses the administrator view, and Maya only browses from a QR code. If roles can reach the wrong view, staff may perform actions outside their responsibilities or the administrator workflow may be exposed to people who should not use it.

#### ASSUMPTIONS

- Elena creates and deactivates staff accounts and assigns each account a Server, Kitchen, or Admin role. The Kitchen role may be assigned to the shared kitchen-station account rather than an individual cook account.
- The product does not manage password reset or identity-provider integration.
- A table label is a human-readable unique identifier. Its format, numbering convention, and maximum length must be confirmed with Elena before implementation.
- Deactivating a table blocks only new-order selection. Existing orders retain their table label and can continue through their existing item-status and billing workflows.
- For access-flow usability testing, an 80% passing rate is an initial target that requires validation with Elena and staff before implementation.

#### FUNCTIONAL REQUIREMENTS

- **As Elena, I want to maintain a list of uniquely labeled tables in the administrator view so that Daniel and Marcus can attach each new order to the correct table.**

  - Elena can maintain the table list from the administrator view.
  - Each table has a unique label.
  - A table has no seat-capacity attribute in this release.

- **As Elena, I want to deactivate a table instead of deleting it so that it cannot receive a new order but remains identifiable on its existing orders.**

  - Elena can deactivate a table from the administrator view.
  - A deactivated table cannot be selected for a new order.
  - The table label remains visible on its existing orders.

- **As Elena, I want to create and deactivate staff accounts and assign each account a role so that a new server can log in on the first day while former staff no longer have access.**

  - Elena can create and deactivate staff accounts from the administrator view.
  - Elena assigns each staff account one of the Server, Kitchen, or Admin roles.
  - A new server with an active Server account can log in to the server workflow on the first day.
  - A deactivated staff account cannot access its former workflow.
  - The Kitchen role may be assigned to the shared kitchen-station account rather than an individual cook account.

- **As Elena, I want the administrator view available only through the Admin role so that routine menu and table maintenance stays limited to the person responsible for it.**

  - Elena uses the Admin login to access the administrator view.
  - Server and Kitchen roles cannot access the administrator view.
  - The Server and Kitchen roles retain their permitted availability controls without receiving administrator-view access.

- **As Priya, I want to use one shared Kitchen station login so that the kitchen can use its queue and availability controls from the shared workstation without individual cook accounts.**

  - The Kitchen login identifies the shared station rather than an individual cook.
  - Priya can access the kitchen workflow and its permitted availability control through the Kitchen role.
  - The Kitchen role cannot access the administrator view.

#### NON-FUNCTIONAL REQUIREMENTS

- **Role isolation:** Automated authorization tests must verify that Server and Kitchen credentials cannot access administrator-view routes or actions, that a guest session cannot access staff routes or actions, and that a deactivated staff account cannot access its former workflow.
- **Table identity integrity:** Automated integration tests must reject duplicate table labels and new-order use of a deactivated table while confirming that the label remains visible on previously created orders.
- **Access-flow usability:** In a moderated usability test, at least 80% of representative participants assigned a role can reach their permitted starting workflow and cannot mistake another role’s workflow for their own. The 80% target is an initial assumption that requires validation with Elena and staff before implementation.

#### REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Elena maintains uniquely labeled tables | 5 | Requires a table data model, administrator workflow, uniqueness validation, persistence, and tests. The scope is bounded but establishes shared operational data. |
| Elena deactivates tables while preserving existing order identity | 5 | Requires lifecycle handling for table records, new-order validation, historical display behavior, and integration tests with orders. |
| Elena creates, deactivates, and assigns staff accounts | 8 | Requires staff-account lifecycle management, role assignment, active-account authorization, first-day login coverage, and tests for deactivation. The shared Kitchen station account adds a role-specific access path. |
| Elena uses the Admin-only administrator view | 5 | Requires role-based route and action authorization plus coverage for the availability-control exception. The underlying password-reset and identity-provider mechanisms remain out of scope. |
| Priya uses the shared Kitchen station login | 3 | Requires Kitchen-role routing and authorization for a shared station identity, plus tests that it cannot reach administrator capabilities. |
