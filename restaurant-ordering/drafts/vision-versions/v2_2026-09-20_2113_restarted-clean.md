# Product Vision — Restaurant Ordering and Status Platform

**Status:** Draft v1
**Date:** 2026-09-20
**Author:** Product Manager (drafted with Claude Opus 5)
**Scope:** Single restaurant, single location

---

## 1. Vision statement

For a single dine-in restaurant, we will replace handwritten tickets and verbal
kitchen updates with one shared record of every order. Guests browse an
always-current menu on their own phone by scanning a QR code at the table.
Servers enter the order against a table, and the kitchen receives it the moment
it is sent. Each item carries its own status, so a server can answer "where is
my food?" by looking at a screen instead of walking into the kitchen, and the
kitchen never works from an ambiguous ticket.

We are deliberately not building a point-of-sale system. We do not process
payments, and we do not give guests an account, an identity, or a transactional
surface. The platform's job is to move an order accurately from the table to the
kitchen and to keep everyone honest about its state.

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
| **Guest** (anonymous, no account) | Scans the table QR code | Read the current menu, with prices, and see what is unavailable |
| **Server** | Logs in as a user with the Server role | Enter an order against a table, attach details to an item, watch item progress, close out the check |
| **Kitchen staff** | Log in as a user with the Kitchen role — one shared station user or several individual ones | See incoming items in one queue, start them, mark them ready, reject what cannot be made |
| **Admin / manager** | Logs in as a user with the Admin role | Maintain the menu: categories, items, prices, availability |

Guests are not users of the system in any technical sense. They have no login,
no role, no identifier, and no record. Scanning the QR code takes them to the
menu and nothing else.

## 4. What we are building

### 4.1 Guest menu (read-only)

A QR code at the table opens the menu on the guest's phone. The menu reflects
the live state of the kitchen: an item marked unavailable does not appear as
orderable. There is no cart, no submit button, no order history, and no status
view. The guest decides what they want and tells their server.

### 4.2 Server order entry

A server creates an order, **binds it to a table**, and adds items to it. Every
item belongs to exactly one order, and every order belongs to exactly one table.
For any item, the server can attach a **free-form description** — "no onions,"
"medium rare," "allergy: shellfish," "split into two plates" — which the kitchen
sees verbatim on the item.

An open order is editable: the server can add items, void an item, cancel the
whole order, and move or merge an order between tables when guests change seats
or tables combine. When something is cancelled after the kitchen has already
started it, the kitchen is told explicitly rather than having the item silently
vanish from the queue.

### 4.3 Kitchen queue

One undifferentiated queue. There is no routing to grill, fryer, or bar stations
in v1. Items arrive as they are sent, the kitchen works the queue, and each item
is advanced individually.

### 4.4 Status model

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

### 4.5 Item availability (86-ing)

Both **kitchen and servers** can mark a menu item unavailable, because both
discover it — the kitchen when the last portion is plated, the server when the
kitchen tells them across the pass. Marking an item unavailable removes it from
the guest menu immediately and blocks it from being added to new orders.

### 4.6 Notifications

The platform pushes an alert to whoever owes the next action, rather than
expecting anyone to stare at a screen:

- Kitchen is alerted when new items are sent to the queue.
- Server is alerted when an item goes Ready, and when the kitchen rejects an
  item.
- Kitchen is alerted when an item they have started is cancelled.

### 4.7 Menu management

Admins maintain a flat, minimal structure: **categories**, and within them items
with a name, description, and price. An item can be marked available or
unavailable. Modifiers, option groups, combos, dayparted menus, and scheduled
pricing are not in v1 — per-item free-form descriptions from the server cover
the real special-request cases at this scale.

### 4.8 Totals, receipts, and settlement

Payment processing is **out of scope**. We take no card data and integrate with
no payment provider. We do produce the paperwork around the money:

- An **order total**, computed from the items actually on the order.
- A **printable/viewable receipt** for the order.
- A manual **"mark as paid"** action, recorded by the staff member who settles
  the check at whatever terminal or register the restaurant already uses.

The platform is the system of record for *what was ordered and what it cost*,
not for *how it was paid*.

## 5. Explicitly out of scope for v1

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

## 6. What success looks like

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

## 7. Open questions and assumptions to confirm

1. **QR scope.** Because guests have no identifier and see no status, the QR code
   only needs to reach the menu — one restaurant-wide code would work. Assumed:
   per-table codes anyway, so the printed code at a table can later carry table
   context (and so guests at table 12 can't be handed the wrong thing). Confirm
   whether per-table codes are worth the printing overhead.
2. **"Orders linked to the table, items linked to the order."** Read that way
   from the brief. Confirm there is no case where an item needs to belong to
   something other than a single order (e.g. a shared appetizer across two
   checks).
3. **Splitting a check.** "Move or merge tables" is in scope; splitting one
   order into two checks was not discussed. Assumed out of v1.
4. **Who may mark an order paid.** Assumed any Server or Admin. Confirm whether
   this should be restricted.
5. **Void vs cancel wording.** Assumed a server-removed item and a
   kitchen-refused item are distinguished in the record (Cancelled vs Rejected)
   because the reasons differ operationally. Confirm that distinction is wanted.
6. **Hardware.** Server devices (personal phones vs restaurant handhelds) and
   the kitchen surface (wall tablet vs ticket printer) are undecided and will
   shape the kitchen queue design.
7. **Notification delivery.** In-app sound and badge is assumed. Whether
   anything needs to reach a device that is asleep or locked is unresolved.
