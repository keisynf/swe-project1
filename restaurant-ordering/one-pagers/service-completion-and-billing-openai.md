# Service Completion and Billing 1-pager

## PROBLEM

After food has reached the table, Daniel needs a reliable final bill without returning to paper notes or manually recalculating totals. The bill must reflect the items, modifiers, quantities, and tax- and service-inclusive prices that were actually ordered. Daniel also needs a clear completion step that distinguishes delivering food from finishing billing work, because a delivered order is not fully complete until the final bill has been generated and the order is closed. When no fulfillable item remains because every item was canceled or rejected, Daniel instead needs to close the order without generating a bill.

Marcus needs to recognize when an ordinary order has reached that point in service. On his first shifts, he can generate a bill, but the application must not suggest that it processed a payment or that a closed order can still receive item changes. Elena benefits when staff can close service consistently without an extra payment system or external point-of-sale integration.

## ASSUMPTIONS

- The final bill is generated and viewed within the application. Printing, emailing, exporting, and providing guests direct bill access are outside this release.
- Generating a final bill does not process payment, suggest a tip, calculate tax or service charges, or store a tax rate.
- For first-shift billing usability testing, an 80% passing rate is an initial target that requires validation with Elena and servers before implementation.
- A closed order is final: it cannot receive further item-state changes. An order whose derived status is `canceled` or `rejected` may close without a bill. Archival, deletion, reopening, refunds, and post-close corrections are outside this release.

## FUNCTIONAL REQUIREMENTS

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

## NON-FUNCTIONAL REQUIREMENTS

- **Bill calculation integrity:** Automated integration tests must verify that every generated bill contains the current ordered items, selected modifiers and quantities, and a total equal to the sum of the included tax- and service-inclusive item prices. The tests must also verify that regeneration after an item change updates the bill and that no separate tax, service, or tip amount appears.
- **Closure integrity:** Automated integration tests must permit closing a delivered order only after a bill has been generated after its most recent item change, permit bill-free closure only when the derived order status is `canceled` or `rejected`, and reject item changes after closure.
- **Billing-flow usability:** Under the 80% initial usability target, at least 80% of representative new-server participants can identify a delivered sample order as ready to bill and close and explain that the resulting bill does not process payment. Verify this in a moderated usability test.

## REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Daniel generates and regenerates a server-only bill | 8 | Requires bill composition from current items, modifiers, quantities, and inclusive prices; Server-only access; regeneration after item changes; a timestamp comparison for stale-bill detection; and accuracy tests. The timestamp check extends the existing bill workflow without adding a separate lifecycle subsystem. |
| Daniel closes a delivered, canceled, or rejected order | 8 | Requires separate completion validation for delivered-and-billed, canceled, and rejected orders; verification that a delivered order’s bill follows its final item change; the closed final state; prevention of later item changes; and integration tests for each path. |
| Marcus completes the first-shift billing workflow | 3 | Reuses bill and closure capabilities but requires clear eligibility cues, payment-boundary language, and moderated usability validation for a new server. |
