# Server Order Entry 1-pager

## PROBLEM

When Daniel takes a table’s order during a busy shift, he needs to select the correct active table and record the dishes and modifiers the guests chose from the current menu. If he cannot see whether an item is available or the table selection is unclear, he can create an order that the kitchen cannot fulfill or attach it to the wrong table. The product needs one accurate starting record for each order before Priya receives its items in the kitchen queue.

Marcus faces the same workflow without Daniel’s experience. On his first day, he needs to understand how choosing a table relates to a new order, recognize that he can only choose available items, and enter standard guest requests without asking a coworker to complete every step. Exceptions such as a rejection or cancellation remain in the kitchen and item-status workflow rather than becoming an unscoped order-editing feature here.

## ASSUMPTIONS

- When Daniel or Marcus creates an order item, the system assigns it the `placed` state and associates it with exactly one selected active table, as defined in the vision.
- Each new order starts with one or more item entries. Because the bill must list quantities, this epic assumes a server records a positive quantity for each selected item; the default quantity, quantity-entry interaction, and maximum quantity require confirmation before implementation.
- For first-shift usability testing, an 80% passing rate is an initial target that requires validation with Elena and servers before implementation.
- The vision does not define editing modifiers after creation, splitting an order, moving an order between tables, or merging orders. These capabilities are outside this release unless separately decided.

## FUNCTIONAL REQUIREMENTS

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

## NON-FUNCTIONAL REQUIREMENTS

- **Order-entry integrity:** Automated integration tests must reject creating an order without exactly one active table, recording a non-positive quantity, or creating an item without the `placed` state.
- **First-shift usability:** Under the 80% initial usability target, at least 80% of representative new-server participants can create a sample order for an active table with a current menu item and modifier without selecting a deactivated table. Verify this in a moderated usability test.
- **Order persistence:** End-to-end tests must confirm that items created with a new order or added to an open order present the same table label, items, modifiers, and quantities to the server workflow and the kitchen queue without re-entry by either role.

## REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Daniel selects an active table for a new order | 5 | Requires the new-order workflow, active-table query and validation, persistence of the selected table, and tests for deactivated-table rejection. |
| Daniel adds available items, modifiers, and quantities | 8 | Requires menu selection in the server workflow, availability validation, modifier and quantity capture, placed-state creation, persistence, and kitchen-facing verification. |
| Daniel adds items to an open order | 5 | Requires an open-order update path, creation of distinct placed items, preservation of existing items and table association, kitchen propagation, and tests. |
| Marcus creates a standard first-shift order | 3 | Reuses the core order-entry flow but needs deliberate sequencing and moderated usability validation for a new server. |
