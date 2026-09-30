# Order and Table Lifecycle 1-pager

**Epic:** keeping an order attached to the right table and the right server as the
room and the roster change.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §6, §7;
`drafts/adoption-risks.md`.

## PROBLEM

A dining room does not hold still. A two-top at table four is halfway through
drinks when two friends arrive and the party moves to table eleven. Two tables get
pushed together for a party of six, and what were two orders now needs to settle as
one bill. At nine o'clock Devin's shift ends with two of his tables mid-meal, and
somebody else has to own them. On paper each of these is handled by someone
remembering to say something out loud: the ticket still says table four for the
rest of the night, so a runner puts a plate in front of the wrong guests; the
handover is a "table seven's yours" on the way out the door, which works until it is
forgotten and a plate comes up for a table nobody is watching.

This epic makes those three movements explicit and recorded. An order can be moved
to a different table, two orders can be merged into one, and an order can be handed
from one server to another, with the transfer recorded so responsibility is always
current rather than assumed. Items keep the statuses they already have through all
of it, and the kitchen is unaffected: the items are the same items, and Tom never
needs to know the room was rearranged. Marisol benefits indirectly — when she covers
a section or a server goes home sick, the tables have an owner without her
negotiating it.

Scope boundary: this epic covers moving, merging, and transferring ownership of
existing orders. Creating orders and adding items belongs to Server Order Entry;
item statuses and the kitchen's view belong to Kitchen Queue and Item Status;
dividing a check belongs to Settlement and Splitting; the list of tables itself is
maintained in Menu and Staff Administration.

## ASSUMPTIONS

1. **Tables are admin-maintained configuration** in the administration epic, with no
   capacities.
2. **A merge cannot be undone.** Once two orders are one, splitting them back apart
   is a settlement-time operation, not a reversal. Undecided.
3. **Merging is allowed regardless of which server owns each order**, with the
   merged order taking one owner. Which owner it takes is undecided.
4. **A partly settled order cannot be moved or merged.** Settled parts are locked
   (Settlement and Splitting), and moving money already taken is not defined.
   Undecided.
5. **A handoff transfers the whole order**, not individual tables or items, and
   needs no manager approval.
6. **An admin cannot force a reassignment.** Only a server can hand off an order,
   which means a server who leaves mid-shift without handing over leaves orders
   owned by someone who is not in the building. Undecided and a plausible
   real-world gap.
7. **Handoff is one order at a time.** Whether a server can hand over an entire
   section in one action is undecided, and Devin's scenario has two tables.
8. **The kitchen is never notified of a move, merge, or handoff**, since none of
   them changes what is being cooked.
9. **History is retained** — an order remembers that it moved tables or changed
   hands. How long the record is kept and who can see it is undecided.
10. **No table state of its own.** The system does not track a table as free,
    seated, or dirty; a table is only an identifier an order points at.

## FUNCTIONAL REQUIREMENTS

* **As Devin, I want to move an order to a different table, so that the order follows
  the guests when they change seats.**

    * Every item moves with the order and keeps its current status.
    * The kitchen queue is unchanged by the move.
    * The order can only move to a table that has no open order of its own.

* **As Devin, I want to merge two orders into one, so that guests who have joined
  tables receive a single check.**

    * All items from both orders end up on one order, keeping their statuses and
      their notes.
    * The resulting order is bound to one table and has one owner.
    * The merge either completes fully or leaves both orders as they were; a
      half-merged state is never visible to anyone.

* **As Devin, I want to hand an order to another server, so that responsibility
  transfers cleanly when my shift ends.**

    * The receiving server's name becomes the order's owner, and the transfer is
      recorded with who handed it over and when.
    * The order appears in the receiving server's own tables, and its alerts go to
      them from that moment.
    * No approval from a manager or admin is required.

* **As Devin, I want to see which orders are mine, so that I know what I am
  responsible for right now.**

    * My open orders are listed, with their tables and their derived status.
    * Orders I have handed away are no longer mine.
    * The rest of the floor's orders remain reachable when I am covering for someone.

* **As Eli, I want to see who owns a table I am asked about, so that I can point a
  guest or a cook at the right person on my first shift.**

    * Each order shows its responsible server by name.
    * This is visible without needing to own the order.

## NON-FUNCTIONAL REQUIREMENTS

* **Propagation latency.** A move, merge, or handoff is reflected on every affected
  device within 2 seconds, so two servers never act on different pictures of who
  owns what.
* **Durability through restructuring.** No item, note, or status is ever lost or
  duplicated by a move or a merge, including when two servers act at the same
  moment.
* **Traceability.** For any order, it is possible to establish afterwards which
  server owned it at any point in the evening, and when it changed hands.
* **Speed of use.** A handoff of one order takes a server a few seconds at the end
  of a shift; a move takes no longer than walking the guests to the new table.
* **Session endurance.** An order handed to a server who is logged in on another
  device appears there without that server re-logging in.

## REQUIREMENTS SIZING

**Metric: story points on a modified Fibonacci scale (1, 2, 3, 5, 8, 13),**
consistent with the other 1-pagers. One point is a day or less of well-understood
work for one person; 13 means the story carries unresolved design as well as build.

| # | Story | Size | Rationale |
| --- | --- | --- | --- |
| 1 | Move an order to another table | **3** | A single reference change, with the empty-target rule and the guarantee that statuses survive. Low risk. |
| 2 | Merge two orders | **8** | The riskiest story in the epic. Two item sets, two owners, two derived statuses, all resolving to one, with an all-or-nothing outcome that must hold when two servers act at once — and no way back if it goes wrong, since merges cannot be undone. |
| 3 | Hand an order to another server | **5** | Ownership change plus rerouting that order's alerts to a different device, and a recorded transfer that has to be readable later. |
| 4 | See my own orders | **3** | A filtered view, but it is the server's home screen and depends on ownership being reliable. |
| 5 | See who owns a table | **1** | One field surfaced in a view that already exists. |

**Not sized, because they are unresolved rather than unestimated:** admin-forced
reassignment of a departed server's orders (assumption 6), handing over a whole
section in one action (assumption 7), unmerging (assumption 2), and any handling of
a partly settled order (assumption 4). Assumption 6 is the one most likely to be
needed in practice, because a server going home sick mid-service is ordinary and
currently leaves orders stranded.
