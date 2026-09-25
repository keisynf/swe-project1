# Product Vision — Restaurant Ordering and Status Platform

**Status:** Draft v1
**Date:** 2026-09-20
**Author:** Product Manager (drafted with Claude Opus 5)
**Scope:** Single restaurant, single location

---

## 1. Vision statement

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

## 2. The problem

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

## 3. Who this is for

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

## 4. Why a restaurant would choose this

### 4.1 What they would choose instead

Our target buyer is a single independent dine-in restaurant. Today they have four
realistic options, and we have to beat each on its own terms:

| Alternative | What it gets them | What it costs them |
| --- | --- | --- |
| **Paper tickets and shouting** (the real incumbent) | Free, zero setup, every member of staff already knows it | The five failure modes in section 2, every single service |
| **A full POS suite** (Toast, Square for Restaurants, Clover, Lightspeed) | Ordering, kitchen display, payments, reporting, everything | Monthly per-terminal fees, a cut of sales, proprietary hardware, a contract, switching payment processors, and retraining every employee |
| **A digital-menu SaaS** | A QR menu, cheaply | Solves only the menu; the kitchen coordination problem is untouched |
| **A kitchen display add-on** | A screen for the line | Generally only sold bolted onto a POS they would first have to adopt |

### 4.2 Our answer

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

### 4.3 Where this position is weak

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

## 5. What we are building

### 5.1 Guest menu (read-only)

A **single QR code** for the restaurant opens the menu on the guest's phone; the
same code is printed on every table tent, so there is nothing per-table to
maintain or reprint. The menu reflects the live state of the kitchen: an item
marked unavailable does not appear as orderable. There is no cart, no submit
button, no order history, and no status view. The guest decides what they want
and tells their server.

### 5.2 Server order entry

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

### 5.3 Kitchen queue

One undifferentiated queue. There is no routing to grill, fryer, or bar stations
in v1. Items arrive as they are sent, the kitchen works the queue, and each item
is advanced individually.

### 5.4 Status model

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

### 5.5 Item availability (86-ing)

Both **kitchen and servers** can mark a menu item unavailable, because both
discover it — the kitchen when the last portion is plated, the server when the
kitchen tells them across the pass. Marking an item unavailable removes it from
the guest menu immediately and blocks it from being added to new orders.

### 5.6 Notifications

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

### 5.7 Devices

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

### 5.8 Menu management

Admins maintain a flat, minimal structure: **categories**, and within them items
with a name, description, and price. An item can be marked available or
unavailable. Modifiers, option groups, combos, dayparted menus, and scheduled
pricing are not in v1 — per-item free-form descriptions from the server cover
the real special-request cases at this scale.

### 5.9 Totals, receipts, splitting, and settlement

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

## 6. Explicitly out of scope for v1

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

## 7. What success looks like

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

## 8. Decisions and open questions

### 8.1 Decided

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

### 8.2 Open

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

### 8.3 Deferred by decision

Raised, consciously set aside for now, and cheap to revisit later:

- **Rounding overage disclosure.** Round-up over-collects a few cents per split
  item. Nothing extra will be shown on the receipt for now. Flagged rather than
  dropped because the amounts are real money, so it is worth a look from whoever
  owns tax and books before the restaurant runs it in production.
- **Receipt output format.** No printer support, on-screen only for now.

