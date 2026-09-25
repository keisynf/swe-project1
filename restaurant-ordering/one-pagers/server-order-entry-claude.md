# Server Order Entry 1-pager

**Epic:** taking an order at the table on a handheld and getting it to the kitchen
intact.
**Sources:** `vision/vision-statement-claude.md` §5.2, §5.7;
`personas/personas-claude.md`; `drafts/scenarios-claude.md` §4, §14;
`drafts/adoption-risks.md`.

## PROBLEM

Devin takes orders on a pad in his apron and fires them at a terminal by the
kitchen door. Both hands are usually full, so the pad is written at speed and
abbreviated under pressure, and then Tom reads that handwriting across a hot line.
This is where the expensive failures start: table six has four covers and three
modifications — an allergy, a steak temperature, and a plate to be split in the
kitchen — and any one of them misread means a plate comes back, a portion is
wasted, the guest's evening is spoiled, and Devin loses the tip. Walking to the
terminal also takes him out of his section at exactly the moment new guests are
sitting down.

This epic puts order entry on the handheld at the table. A server opens an order
against a table, adds items from the live menu, types a note onto any item that
needs one, and sends it; the items appear in the kitchen queue with the note
verbatim. Later rounds are added to the same order, and a mistake is voided rather
than argued about at the pass. For Eli on his first shift this is also where the
product either teaches him the job or adds to it: the menu he cannot yet remember
is in his hand, and the dish the kitchen ran out of an hour ago is not offered to
him at all.

Scope boundary: this epic covers composing and sending an order and correcting it.
What happens to items after they are sent belongs to Kitchen Queue and Item Status;
moving, merging, and handing over orders belongs to Order and Table Lifecycle;
marking dishes unavailable belongs to Item Availability; totals, receipts, and
settlement belong to Settlement and Splitting.

## ASSUMPTIONS

1. **One open order per table at a time.** A second party at the same table starts
   a new order only after the first is settled. The vision implies this but never
   states it, and the merge capability suggests exceptions exist.
2. **Items are sent in explicit batches, not individually as they are tapped.**
   Devin composes the table's order and sends it in one action. Not stated in the
   vision.
3. **No coursing.** Nothing is held back for later firing; what is sent enters the
   queue immediately.
4. **Covers, seat numbers, and guest names are not captured.** An order is attached
   to a table and a server, and nothing else. The vision never mentions them.
5. **Repeated dishes are separate items, not a quantity field**, because each one
   can carry its own note and its own status. Undecided.
6. **A note can be edited until the item is sent, and not afterwards.** What happens
   when a guest changes their mind about a modification after firing is undecided.
7. **Any server can act on any order, not only the server who owns it.** The vision
   records order ownership but never says it restricts anything. Undecided.
8. **Voiding an unsent item leaves no record; voiding a sent item becomes a
   Cancelled item** the kitchen is told about. The boundary between "removed" and
   "cancelled" is assumed at the send action.
9. **No undo and no confirmation step.** The vision has neither. Eli is the person
   this hurts, and fear of a mistap in front of guests is the specific mechanism by
   which he reverts to paper.
10. **No training mode.** A new server's first use is a live table.
11. **Order entry requires connectivity.** Whether a server can compose an order
    offline and have it send on reconnect is undecided, and the restaurant's wifi
    reaches the back of the room unreliably.
12. **Table identifiers already exist** and are maintained elsewhere. The vision
    never says where the list of tables comes from.

## FUNCTIONAL REQUIREMENTS

* **As Devin, I want to open an order and bind it to a table, so that everything
  ordered is attached to the right table and to me.**

    * The order records both the table and the server who opened it.
    * The order is visible to me as one of my tables from the moment it exists.
    * An order cannot exist without a table.

* **As Devin, I want to add items to the order from the live menu while standing at
  the table, so that I never walk to a terminal to fire an order.**

    * The menu is browsable by category, with prices, as the guest sees it.
    * An item marked unavailable cannot be added.
    * Adding an item does not require leaving the order I am building.

* **As Devin, I want to attach a free-form note to an individual item, so that the
  kitchen receives the guest's requirements exactly as I heard them.**

    * The note is attached to one item, not to the order.
    * Two of the same dish on one order can carry different notes.
    * The kitchen sees the note verbatim, unabbreviated and unaltered.

* **As Devin, I want to send the order to the kitchen in one action, so that cooking
  starts and I know it has landed.**

    * Sending is explicit; nothing reaches the kitchen while I am still composing.
    * Sent items enter the kitchen queue and become visible to the kitchen
      immediately.
    * I can see that the send succeeded before I walk away from the table.

* **As Devin, I want to add a later round to an order that is already open, so that
  a table can order more without starting a second check.**

    * New items join the existing order and are sent the same way.
    * Items already served or rejected stay on the order and are unaffected.

* **As Devin, I want to void an item I entered wrongly, so that a mistake costs
  nothing more than a tap.**

    * An item not yet sent is removed outright.
    * An item already sent becomes Cancelled, and the kitchen is told if it has
      been started.
    * Voiding does not remove the rest of the order.

* **As Devin, I want to cancel an entire order, so that a table that leaves or was
  entered twice does not stay open all night.**

    * Every outstanding item on the order is cancelled in one action.
    * Anything the kitchen has started is reported to the kitchen.
    * A settled or partly settled order cannot be cancelled this way.

* **As Eli, I want to take an order on my first shift without being taught during
  service, so that I am useful on day one.**

    * The menu in the app is complete and current, so I do not need my annotated
      paper copy to know what exists.
    * Dishes the kitchen has run out of are not offered to me at all.
    * The steps are labelled in plain language, with no reliance on restaurant
      shorthand.

## NON-FUNCTIONAL REQUIREMENTS

* **Entry speed.** A server can enter a four-cover order with three item notes in
  less time than writing it on a pad. This is the adoption threshold for the whole
  epic: if entry is slower than paper, servers stop using it mid-shift.
* **Interaction responsiveness.** Adding an item, opening the note field, and typing
  register without perceptible delay, and never block on a network round trip.
* **Send confirmation latency.** A sent order is confirmed to the server, and
  visible in the kitchen, within 2 seconds on the restaurant's wifi.
* **Durability of a sent order.** Once a send is confirmed, no item is ever lost,
  including if the handheld is dropped, sleeps, or loses wifi immediately
  afterwards.
* **One-handed use.** Every step of taking an order can be completed on a handheld
  held in one hand, while standing.
* **Session endurance.** A server's session lasts a full shift on one device
  without re-login.
* **Coverage.** Order entry works everywhere guests are seated, including the parts
  of the room where wifi is weakest.

## REQUIREMENTS SIZING

**Metric: story points on a modified Fibonacci scale (1, 2, 3, 5, 8, 13),** as used
in the Kitchen Queue and Item Status 1-pager, so sizes are comparable across epics.
One point is a day or less of well-understood work for one person; 13 means the
story carries unresolved design as well as build.

| # | Story | Size | Rationale |
| --- | --- | --- | --- |
| 1 | Open an order bound to a table | **3** | Small data model, but it establishes order ownership that three other epics depend on. |
| 2 | Add items from the live menu | **8** | The most-used screen in the product and the one with the hardest target: faster than a pad, one-handed, in a noisy room. Cost is interaction design and iteration, not logic. |
| 3 | Free-form note per item | **3** | Mechanically simple. Its value is that the text survives to the kitchen unaltered, which is a contract more than a feature. |
| 4 | Send the order | **5** | Batch semantics, a confirmation the server can trust before walking away, and the durability guarantee behind it. |
| 5 | Add a later round | **2** | Reuses send once items and orders are separable. |
| 6 | Void an item | **5** | Two different behaviours either side of the send boundary, plus the cross-epic cancellation alert to the kitchen. |
| 7 | Cancel an order | **3** | A batch of the above, with the settled-order exclusion. |
| 8 | First-shift usability for a new server | **5** | Little new code, real work: plain-language wording and walking the whole entry path with someone who has never worked a restaurant. Sized for design and testing effort. |

**Not sized, because they are unresolved rather than unestimated:** offline
composition and send-on-reconnect (assumption 11), an undo or confirmation path
(assumption 9), editing a note after sending (assumption 6), and a training mode
(assumption 10). Offline entry in particular could exceed story 2 on its own, and
should be decided before the handheld platform is chosen.
