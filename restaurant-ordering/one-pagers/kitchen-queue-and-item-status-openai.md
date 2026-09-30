# Kitchen Queue and Item Status 1-pager

## PROBLEM

During a busy shift, Priya needs to see every dish the servers have placed, including its modifiers and table, and update it as kitchen work begins and finishes. Daniel needs the same record to tell whether food is still waiting, being prepared, ready to carry out, or cannot be fulfilled. Without that shared record, Priya is interrupted for status checks and Daniel has to rely on verbal updates, increasing the chance that the kitchen makes the wrong dish or a table receives an inaccurate update.

The workflow must also make sense to Marcus on his first shift. He needs to understand which item states describe kitchen work, which action belongs to a server, and when a kitchen rejection means that he needs help responding to a table. If Daniel cancels work that Priya has already started or marked ready, Priya needs a visible in-app alert at the shared kitchen station so that the kitchen can stop or avoid unnecessary work.

## ASSUMPTIONS

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

## FUNCTIONAL REQUIREMENTS

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

## NON-FUNCTIONAL REQUIREMENTS

- **Shared-state freshness:** Under the shared-state update assumption, at least 95% of tested item-status and rejection-reason changes appear in every relevant active kitchen and server view within 3 seconds. Verify this with timestamped end-to-end tests for each change type, without reopening a view.
- **First-shift usability:** Under the first-shift usability assumption, at least 80% of representative new-server participants can correctly identify six sample item states, identify a rejection reason, and mark a ready item delivered without attempting a kitchen-only action. Verify this in a moderated usability test.
- **State integrity:** Automated integration tests must reject invalid state transitions, including a non-kitchen attempt to set `preparing`, `ready`, or `rejected`; delivery of a non-ready item; and any transition from `canceled` or `rejected` to another state.

## REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Priya views the queue and changes preparation states | 8 | Requires a kitchen queue view, modifier and table-label display, two kitchen-owned transitions, state validation, and tests. The shared-state display and update path span several related behaviors. |
| Priya rejects unfulfillable items with an optional reason | 5 | Adds a terminal transition, optional text capture, server visibility, validation, and tests across the kitchen and server views. The workflow is bounded but crosses roles. |
| Priya receives cancellation alerts | 5 | Requires detection of the canceled item’s prior state, an in-app alert at the kitchen station, and tests for preparing and ready items. Alert presentation details are still assumed. |
| Daniel views item and derived order status | 8 | Requires a server status view, rejection-reason display, and correct application of the precedence-based order-status rules across mixed item states. Shared updates and lifecycle coverage add test complexity. |
| Daniel delivers ready items and cancels undelivered items | 5 | Adds server-owned transitions, permission checks, terminal-state handling, and the connection to kitchen alerts. It spans server and kitchen behaviors but follows a defined workflow. |
| Marcus uses the first-shift server workflow | 3 | Reuses the status and delivery capabilities but needs deliberate presentation and usability-test support so a new server can recognize states and allowed actions. It does not introduce a training subsystem. |
