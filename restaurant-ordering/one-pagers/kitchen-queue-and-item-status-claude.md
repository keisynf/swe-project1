# Kitchen Queue and Item Status 1-pager

**Epic:** the shared record of where every ordered item stands, and the kitchen
surface that drives it.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §5, §10–13;
`drafts/adoption-risks.md`.

## PROBLEM

At La Jarra, an order's real state lives in three places that disagree: the paper
ticket on the rail, the server's memory, and whatever Tom has actually started
cooking. Tom runs the line with two cooks and calls the pass from one spot for six
hours. Every service, four or five times, a server walks up to ask him whether a
table's mains are up — a question the rail already answers, and each one costs him
focus he cannot spare. When he finishes a plate he calls it out and hopes the floor
hears; when they do not, food sits under the lamp and goes out cold. Meanwhile
Devin, three tables away with both hands full, has no way to know that table six's
mains are ready without walking to the pass himself, and no way to know that the
lamb he cancelled two minutes ago is still cooking.

This epic replaces that with one item-level record both sides read from. Items
arrive in a single undifferentiated queue on a TV Tom can read from across the
kitchen, and he advances them on a tablet at the pass: In progress, Ready, or
rejected when the line cannot make it. Devin sees those statuses on his handheld
without leaving his section, marks items Served as he delivers them, and is told
when something goes Ready or is refused. The order's own status is derived from its
items, so nobody maintains it by hand and nobody has to reconcile two versions of
the truth.

Scope boundary: this epic covers the queue, the item status lifecycle, and the
alerts attached to status changes. Order entry and free-form item notes, marking
menu items unavailable, splitting and settlement, menu management, and staff user
administration are separate epics, and are referenced here only where this one
depends on them.

## ASSUMPTIONS

1. **Queue order is arrival order.** The queue sorts oldest-sent first and cannot
   be manually rearranged. This is an identified gap, not a settled design: Tom has
   nineteen years of muscle memory in physically sliding tickets along the rail as a
   table's timing changes, and a fixed-order queue is a regression from the paper it
   replaces. Manual reordering is out of v1 and needs a decision.
2. **No coursing.** Items are not held back or grouped into courses; starters and
   mains enter the queue together as sent.
3. **The TV is a read-only client of the same kitchen session that the pass tablet
   drives.** How the two are actually paired is an open question, as is
   what the TV displays if the tablet sleeps or dies mid-service.
4. **Alerts are in-app only.** Nothing is pushed to a locked or sleeping
   handheld, so a Ready alert waits until Devin next looks at his device. Whether
   alerts batch, group by table, or throttle is open, and an alert on every
   item is expected to get muted.
5. **Rejection captures no structured reason.** Tom taps reject and the server is
   told; there is no reason code or free-text explanation. Undecided.
6. **Served is marked per item.** A server delivering three plates marks three
   items. Whether a "serve all ready items for this table" action exists is
   undecided.
7. **No undo on a status transition.** There is no undo, confirm step, or training
   mode anywhere. Eli is the person this hurts, and it is the reason he
   is expected to fall back to paper. A correction path is needed and undecided.
8. **A Ready item leaves the TV when it is marked Served.** Rejected and cancelled
   items leave immediately. How long anything lingers for reference is undecided.
9. **The kitchen queue shows the table number and the responsible server's name**,
   since an order carries both.
10. **Admin has no view of the queue.** Marisol cannot answer "how long on table
    six?" from her own login, which is one of her stated frustrations. Whether the
    Admin role gets read-only status visibility is undecided.
11. **One shared Kitchen login**, so no transition is attributable to an individual
    cook. Tom may regard this as a feature; Marisol may later want attribution.
12. **Statuses are labelled in plain language** rather than restaurant or internal
    jargon, for Eli's benefit. No wording has been agreed.

## FUNCTIONAL REQUIREMENTS

* **As Tom, I want every item sent to the kitchen to appear in one queue on the TV,
  so that I can cook in the right order without walking to a screen.**

    * One undifferentiated queue; no routing to grill, fryer, or bar stations.
    * Each row shows the item, its table, its free-form note verbatim, its current
      status, and how long it has been waiting.
    * Readable from across a hot line: large type, high contrast, no fine detail,
      no controls on the TV itself.
    * New items appear without anyone touching anything.

* **As Tom, I want to move an item to In progress and then to Ready from the pass
  tablet, so that the floor can see where the food is without asking me.**

    * One tap per transition, with targets usable with wet or gloved hands.
    * The TV reflects the change immediately.
    * Only the Kitchen role can make these two transitions.

* **As Tom, I want to reject an item the line cannot make, so that the server can
  go back to the guest and the refusal is recorded as the kitchen's decision.**

    * Rejection is a distinct outcome from a server's cancellation, and stays
      distinguishable in the record.
    * The responsible server is alerted immediately.
    * The item leaves the active queue.

* **As Tom, I want to be told when an item I have already started is cancelled, so
  that I stop cooking something nobody will eat.**

    * An explicit alert on the pass tablet, not a silent disappearance from a board
      he has memorised.
    * The alert identifies the item and its table.

* **As Tom, I want two people acting on the same item at once to end in one
  unambiguous state, so that the queue never shows something that did not happen.**

    * When two cooks tap the same item, the first transition applies and the second
      is reported as already done rather than overwriting it.
    * When a kitchen rejection and a server cancellation reach the same item, the
      item ends removed either way, and the record keeps whichever arrived first as
      the reason it left.
    * A transition that arrives for an item that has already moved past it is
      refused rather than applied out of order — Ready cannot land on an item
      already marked Served.
    * After any collision, the TV, the pass tablet, and every handheld show the same
      state.

* **As Devin, I want to see the status of every item on my own tables from my
  handheld, so that I stop walking to the pass to ask.**

    * Grouped by table, showing each item's status.
    * The order's status is derived from its items, not set by hand: Ready only when
      every outstanding item is ready.
    * Only my tables by default, with the rest of the floor reachable.

* **As Devin, I want to be alerted when an item goes Ready or is rejected, so that
  I can move without watching a screen.**

    * In-app badge, highlighted row, and sound while the app is open.
    * Identifies the table and the item.
    * Nothing is pushed to a sleeping handheld, which is a known limitation of this
      requirement rather than an omission from it.

* **As Devin, I want to mark an item Served when I put it on the table, so that the
  record matches the room.**

    * Server-role transition only; the kitchen cannot mark an item served.
    * When every item on an order has been served, rejected, or cancelled, the
      order is no longer outstanding.

* **As Eli, I want the queue and the statuses labelled in words I understand on my
  first shift, so that I can use them without being trained during service.**

    * Plain-language status names and actions; no reliance on kitchen shorthand.
    * The meaning of a rejected item is legible without someone explaining it.
    * Nothing on the handheld requires knowing what "the pass" or "86" means.

## NON-FUNCTIONAL REQUIREMENTS

* **Propagation latency.** A status change is visible on the TV and on every
  relevant handheld within 2 seconds on the restaurant's wifi. Slower than that and
  servers stop trusting it and walk to the pass anyway, which defeats the epic.
* **TV legibility.** A person with normal or corrected vision can read any row of
  the queue from 2 metres away in kitchen lighting. Status must be distinguishable
  without relying on colour, given glare, grease, and colour blindness. How that is
  achieved is a design decision, not a requirement.
* **Tablet responsiveness.** The pass tablet wakes and accepts input within one
  second of being touched.
* **Session endurance.** The kitchen session survives a six-hour service on an
  always-on screen without a refresh, re-login, or manual reconnect.
* **Degradation.** A handheld that loses wifi mid-order must never lose an item
  already sent; when connectivity returns, the queue converges to one true state
  with no duplicated or dropped items.
* **Capacity.** A full Saturday service at fourteen tables — roughly 60 live items
  at peak — displays without the queue becoming unreadable or requiring scrolling
  on the TV.
* **Access control.** No guest-identifying data exists anywhere in this epic, so
  the only thing to protect is staff access to the surfaces themselves.

## REQUIREMENTS SIZING

**Metric: story points on a modified Fibonacci scale (1, 2, 3, 5, 8, 13).** Points
are used rather than days because the team's throughput is unknown and the estimates
are comparative. One point is a day or less of well-understood work for one person;
13 means the story carries unresolved design as well as build.

| # | Story | Size | Rationale |
| --- | --- | --- | --- |
| 1 | Queue on the TV | **8** | The data is simple but the surface is not: a legible always-on display, live updates without interaction, and a layout that holds 60 items at 2 metres. Most of the cost is presentation and endurance, not logic. |
| 2 | Kitchen advances In progress / Ready | **5** | Two transitions, role-gated, plus the live propagation contract to two other surfaces. Straightforward once the status model exists. |
| 3 | Reject an item | **5** | Similar mechanics to story 2, but adds a second outcome to the model, a cross-role alert, and the Cancelled/Rejected distinction that must survive into the record. |
| 4 | Kitchen told of a cancellation after starting | **3** | One targeted alert on an event the system already knows about. Small, and valuable out of proportion to its size. |
| 5 | Colliding transitions resolve to one state | **8** | The hardest logic in the epic and the easiest to get subtly wrong: transition ordering rules, a first-writer-wins outcome that must still be correct when one writer is a rejection, and convergence across three surfaces. Needs deliberate testing of races, not just a happy path. |
| 6 | Server sees item status for their tables | **5** | Needs the derived order status rule and a per-server view, both of which depend on order ownership from another epic. Moderate logic, low presentation risk. |
| 7 | Server alerted on Ready / Rejected | **3** | In-app only, so no push infrastructure. Cheap deliberately — and the open batching question could raise it later. |
| 8 | Server marks Served | **2** | One role-gated transition plus the rule that closes out an order. The smallest real story here. |
| 9 | Plain-language labels for a first-shift server | **3** | Little code, real work: agreeing wording, and reviewing every label and action against someone who has never worked a restaurant. Sized for the design effort, not the build. |

**Not sized, because they are unresolved rather than unestimated:** manual queue
reordering (assumption 1), a correction path for a mistaken transition (assumption
7), and alert batching on the pass tablet (assumption 4). Each is a candidate story
in its own right once decided, and assumption 1 in particular could be as large as
story 1.
