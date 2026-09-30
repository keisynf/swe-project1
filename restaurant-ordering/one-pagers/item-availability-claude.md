# Item Availability 1-pager

**Epic:** taking a dish off the menu the moment it runs out, from wherever the
person who found out is standing.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §8, §11, §15;
`drafts/adoption-risks.md`.

## PROBLEM

The last salmon goes on a plate at 8:40. Tom shouts "86 the salmon" at whoever is
nearest and hopes it travels, and it does not travel fast enough: three more tickets
for salmon arrive before the floor catches up, each one a table that has to be told
no after they have already ordered. Devin has the same problem from the other
direction — he is told at the pass that the hake is finished, and the only way to
spread that is to tell each server individually as he passes them, so someone sells
the hake anyway because they were at a table when he walked by. For Marisol this is
the worst guest moment of the night and frequently ends in a comp. For Eli it is the
mistake he is most afraid of making, because he has no idea what ran out an hour
before he arrived.

This epic makes availability one shared fact. Either the kitchen or a server can
mark an item unavailable, because the news reaches whoever happens to be standing at
the pass rather than whoever holds the authority. The moment it is marked, the item
disappears from the guest menu on every phone in the room and can no longer be added
to an order by anybody, including a new server who never heard the conversation.
Putting an item back is the same action in reverse, for the next delivery or the next
service.

Scope boundary: this epic covers the availability state of an existing menu item and
who may change it. Creating, pricing, and describing items belongs to Menu and Staff
Administration; refusing an individual item already ordered is the kitchen's
rejection in Kitchen Queue and Item Status, which is a different thing — a rejection
concerns one item on one order, while unavailability concerns the dish for everyone.

## ASSUMPTIONS

1. **Availability is a simple on or off state, not a count.** The system does not
   track portions remaining and does not decrement anything as orders are taken,
   because inventory depletion is out of scope for the product.
2. **Unavailability persists until someone reverses it.** It does not expire at the
   end of service or reset overnight. Undecided, and the daily reality is that most
   86'd items come back the next day, so a manual reset every morning may be a chore
   nobody does.
3. **Anyone who can mark an item unavailable can also make it available again** —
   kitchen or server, not only an admin.
4. **No confirmation step and no undo.** Marking the wrong dish unavailable takes
   it off every menu in the room instantly, and the only correction is to reverse it
   manually. Undecided.
5. **Nobody is actively notified that an item became unavailable.** Notifications
   cover status changes only. Servers discover it by looking, or
   by being unable to add the item. This may be wrong for a server mid-order at a
   table.
6. **Items already ordered are unaffected.** Marking a dish unavailable does not
   touch items already sent to the kitchen; those are cooked or rejected
   individually.
7. **Availability is recorded but not reported on.** Who 86'd what and how often is
   not surfaced anywhere, which is a pity given Marisol's stated interest in dishes
   running out.
8. **Availability applies to the whole restaurant**, not per service or per daypart,
   since there is only one menu and no dayparts in v1.

## FUNCTIONAL REQUIREMENTS

* **As Tom, I want to mark a dish unavailable from the pass tablet the moment the
  last portion is plated, so that I never have to shout it twice.**

    * One action from the kitchen surface, without leaving the queue.
    * Takes effect for every guest and every member of staff at once.
    * Does not require going through a manager or the office.

* **As Devin, I want to mark a dish unavailable from my handheld, so that what I was
  told at the pass reaches the whole floor without me repeating it.**

    * Available to the Server role, not only the Kitchen role.
    * Can be done while walking, without opening an order.

* **As Eli, I want a dish the kitchen has run out of to be impossible to add to an
  order, so that I cannot sell something that does not exist on my first shift.**

    * An unavailable item cannot be added to any order by any server.
    * The reason it cannot be added is stated plainly, not shown as a silent
      failure.

* **As Priya, I want the menu I am reading to list only dishes that can still be
  ordered, so that I do not pick one that has run out and then be told no.**

    * Unavailable items are not presented as orderable on the guest menu.
    * The menu I am reading reflects the change without me reloading the page or
      rescanning the code.

* **As Marisol, I want to put a dish back on the menu, so that tomorrow's delivery
  is sellable without anyone calling me.**

    * The reverse of marking it unavailable, available to the same roles.
    * The item returns to the guest menu and becomes orderable again.

* **As Devin, I want to see everything that is currently unavailable in one place,
  so that I know what is off before I start my shift.**

    * A single list of currently unavailable items, visible to servers and kitchen.
    * Reachable without hunting through the whole menu.

## NON-FUNCTIONAL REQUIREMENTS

* **Propagation latency.** An availability change reaches every staff device and
  every open guest menu within 2 seconds. This is the entire value of the epic: the
  window between "it ran out" and "everyone knows" is the window in which the
  restaurant sells something it cannot make.
* **Guest menu freshness without interaction.** A guest who has had the menu open
  for twenty minutes sees the current state without reloading or rescanning.
* **Correctness under contention.** When an item is marked unavailable at the same
  moment a server is adding it to an order, the outcome is one of the two clear
  results and never a half-added item.
* **Speed of use.** Marking an item unavailable takes a cook with full hands a
  couple of seconds, from the queue he is already looking at.
* **Resilience.** An availability change made on a device that then loses wifi is
  not lost, and does not resurrect a dish when the device reconnects.

## REQUIREMENTS SIZING

**Metric: story points on a modified Fibonacci scale (1, 2, 3, 5, 8, 13),**
consistent with the other 1-pagers. One point is a day or less of well-understood
work for one person; 13 means the story carries unresolved design as well as build.

| # | Story | Size | Rationale |
| --- | --- | --- | --- |
| 1 | Kitchen marks a dish unavailable | **3** | One state change on an existing item, from a surface that already exists. The cost is the fan-out to guest menus, which is shared with story 4. |
| 2 | Server marks a dish unavailable | **2** | The same action from a second surface once story 1 exists; mostly placement and reachability on the handheld. |
| 3 | Unavailable items cannot be ordered | **3** | A guard in the order-entry path plus a plainly worded explanation, and the contention case where an item goes unavailable mid-order. |
| 4 | Unavailable items absent from the guest menu | **5** | Requires the guest menu to update while open, which is the first live-update requirement on a page with no login and no app. Sized for that mechanism, not the filtering. |
| 5 | Put a dish back on the menu | **2** | The reverse of story 1, reusing the same machinery. |
| 6 | See everything currently unavailable | **2** | A simple filtered list, valuable at the start of a shift. |

**Not sized, because they are unresolved rather than unestimated:** an end-of-service
or overnight reset (assumption 2), a confirmation or undo for marking the wrong dish
(assumption 4), and actively alerting the floor when something goes unavailable
(assumption 5). Assumption 5 is worth deciding early: without it, a server who is
mid-order at a table finds out only when the item refuses to be added, in front of
the guest.
