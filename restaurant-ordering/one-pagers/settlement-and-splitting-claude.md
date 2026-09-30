# Settlement and Splitting 1-pager

**Epic:** what the order cost, how it divides between guests, and recording that it
has been paid — without processing the payment.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §9;
`drafts/adoption-risks.md`.

## PROBLEM

It is 10:40 and table eleven wants to pay. Six guests, and they want it in four
ways: two couples paying together, two people paying alone, and a bottle of wine and
a shared platter that everyone had some of. On paper this is arithmetic done at speed
on the back of a ticket, with a queue of other tables building behind Devin and a
real chance the parts do not add up to the bill. Then one couple pays, and one of the
remaining guests offers to cover a friend, and the whole division has to be redone —
except two people have already handed over money, so those parts cannot move. For
Marisol the same evening ends with her settling checks at the register, and her
interest is narrow and firm: this must not touch her card processing, her processor,
or her rate.

This epic produces the paperwork around the money and stops there. An order has a
total computed from the items actually on it. A check can be divided into any number
of parts, either by assigning each guest's dishes or by dividing a shared item into
even shares across the parts carrying it. Any part can be marked paid by a server,
which locks it; the unpaid remainder stays rearrangeable. Receipts can be produced
for the whole order or for one part. No card data is ever entered, transmitted, or
stored — the restaurant takes the money the way it already does, and this records
that it happened.

Scope boundary: this epic covers totals, splitting, receipts, and marking parts paid.
Payment processing, tips, and tip-out are explicitly out of scope for the product.
What was ordered belongs to Server Order Entry; item statuses belong to Kitchen Queue
and Item Status; merging two tables into one check belongs to Order and Table
Lifecycle.

## ASSUMPTIONS

1. **Prices are tax-inclusive, and there is no service charge line.** The
   price Marisol sets is the price the guest pays, so an order total is simply the sum
   of its items and no tax or service charge is calculated, apportioned, or displayed
   anywhere. This keeps totals, split shares, and the rounding rule working on a single
   number. Two consequences follow, and neither is resolved: a receipt from this
   product shows no tax breakdown, so if anything itemising tax is required it must
   come from the register that actually takes the money; and a change in tax rate is
   absorbed by Marisol re-entering prices by hand, because no rate is stored to change.
2. **Prices are taken from the item as ordered, not from the live menu.** A price
   change mid-service does not re-price an open order. Undecided, and it matters
   because Marisol edits prices on Mondays.
3. **Splitting happens at settlement time**, not while the table is eating.
   Undecided.
4. **A shared item divides into even shares only.** No percentages, no custom
   amounts per part.
5. **Every share of a divided item is rounded up to the cent**, so all parts carry
   the same amount and the parts together exceed the order total by a few cents.
   This deliberately over-collects rather than leaving the restaurant short.
6. **The rounding overage is not disclosed on the receipt.** This is flagged as
   worth a look from whoever owns tax and books, since over-collected cents are real
   money.
7. **Receipts are on-screen only.** No printer support in v1.
   Whether a guest can be sent a receipt some other way is undecided.
8. **Only the Server role marks a part paid**, recorded against whoever did it.
   Whether an Admin can also do it is undecided, which matters because Marisol
   settles at the register herself.
9. **A paid part cannot be reversed.** There is no un-pay, refund, or correction
   path for a part settled in error. Undecided and a plausible nightly occurrence.
10. **Splitting does not require all items to be served.** A table can settle while
    something is still cooking. Undecided.
11. **Nothing prevents an order being left open indefinitely.** There is no
    end-of-night process that forces every order to be settled or closed. Undecided.
12. **The kitchen never sees any of this** — one order is one ticket however the
    check divides.

## FUNCTIONAL REQUIREMENTS

* **As Devin, I want to see the running total for an order, so that I can answer
  "how much is it so far?" without adding it up myself.**

    * Computed from the items actually on the order, excluding cancelled and
      rejected items.
    * Item prices are tax-inclusive, so the total is what the guest owes with nothing
      added at the end.
    * Updates as items are added.

* **As Devin, I want to produce a receipt for an order, so that a table can see what
  they are paying for.**

    * Lists the items charged and the total.
    * Available for an order that has not been split, which is the ordinary case.

* **As Devin, I want to divide a check into any number of parts, so that guests can
  pay separately without me doing arithmetic at the table.**

    * Any number of parts, created at settlement.
    * Each guest's own dishes can be assigned to their part.
    * Every item's cost ends up allocated across the parts.

* **As Devin, I want to divide a single shared item across several parts, so that a
  bottle everyone drank is paid for by everyone who drank it.**

    * A shared item splits into even shares across the parts carrying it.
    * A share that does not divide cleanly is rounded up to the cent, so every part
      carries the same amount for that item.
    * The parts together therefore come to slightly more than the order total, and
      never less.

* **As Devin, I want a receipt for a single part, so that a guest paying their own
  share can see it.**

    * Shows the items on that part, including the share of any divided item.
    * The share of a divided item is shown as what that part is paying, not as the
      menu price.

* **As Devin, I want to mark a part as paid, so that the record reflects money that
  has been taken at the register.**

    * Recorded against the server who marked it and the time it happened.
    * A part marked paid is locked: its items and its allocations cannot change.
    * Parts are settled independently, so a table where some guests have paid and
      others have not is a valid state.

* **As Devin, I want to rearrange an unpaid split, so that guests changing their
  minds about who pays for what costs me one adjustment rather than a restart.**

    * Any part that has not been settled can be re-divided, and items moved between
      unpaid parts.
    * Shares of a divided item are recalculated across the unpaid parts.
    * Settled parts are untouched, including on a partly settled order, and shares of
      an item already partly paid for do not change.

* **As Marisol, I want to know an order has been settled and by whom, so that I can
  reconcile a night's checks against what the register took.**

    * Each order shows whether it is fully settled, partly settled, or open.
    * Each settled part shows who marked it paid and when.

## NON-FUNCTIONAL REQUIREMENTS

* **No payment data.** No card number, cardholder name, or any other payment
  instrument data is ever entered, transmitted, or stored by the product. This is
  both the commercial premise of the product and its main security simplification.
* **Arithmetic integrity.** For any split, the sum of the parts is greater than or
  equal to the order total, never less, and the difference is only ever rounding.
* **Settlement records are durable and immutable.** Once a part is marked paid, that
  record survives device loss, restarts, and connectivity failures, and is not
  silently altered by later activity on the order.
* **Close-out speed.** Splitting a six-cover check four ways, including two shared
  items, is fast enough that no queue of waiting tables forms behind the server.
* **Traceability.** For any settled part it is possible to establish afterwards which
  items it covered, what it totalled, who marked it paid, and when.
* **Availability at close.** The product is usable during the final hour of service
  and at cash-up; being unable to settle is worse than being unable to order, because
  guests are waiting to leave.

## REQUIREMENTS SIZING

**Metric: story points on a modified Fibonacci scale (1, 2, 3, 5, 8, 13),**
consistent with the other 1-pagers. One point is a day or less of well-understood
work for one person; 13 means the story carries unresolved design as well as build.

| # | Story | Size | Rationale |
| --- | --- | --- | --- |
| 1 | Running total for an order | **2** | A sum over items, with cancelled and rejected excluded. Small, and it stays small because prices are tax-inclusive: there is no tax to calculate, apportion across split parts, or display. |
| 2 | Receipt for a whole order | **3** | Rendering plus deciding what a receipt must contain. On-screen only keeps it small. |
| 3 | Divide a check into parts | **8** | The core model change in the epic: parts as first-class things, with every item allocated. Everything else here depends on it. |
| 4 | Divide a shared item into even shares | **5** | Even shares are easy; the rounding rule, and keeping the sum-never-less guarantee while parts are rearranged, is where the care goes. |
| 5 | Receipt for one part | **3** | Reuses story 2, with the added case of showing a share rather than a menu price. |
| 6 | Mark a part paid | **5** | Locking semantics, an immutable record, and attribution to the server. The locking is what makes the rest safe. |
| 7 | Rearrange an unpaid split | **8** | The hardest story: re-dividing around locked parts on a partly settled order, recalculating shares of items that are partly paid for, and never touching settled money. Easy to get subtly wrong and expensive when wrong. |
| 8 | Settlement visibility for the owner | **3** | A read-only view over records the other stories already produce. |

**Not sized, because they are unresolved rather than unestimated:** a correction path
for a part marked paid in error (assumption 9), an end-of-night process that forces
open orders closed (assumption 11), printed or sent receipts (assumption 7), and a
tax breakdown on a receipt should one ever be required (assumption 1). Assumption 9
is the most likely to be needed nightly: a part settled against the wrong guest
currently has no remedy at all, and the parts around it are locked.
