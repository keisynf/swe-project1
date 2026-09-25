# Menu and Staff Administration 1-pager

**Epic:** the owner's control of what is on the menu, what it costs, and who can use
the system.
**Sources:** `vision/vision-statement-claude.md` §5.8, §3, §4.2;
`personas/personas-claude.md`; `drafts/scenarios-claude.md` §1, §2, §3;
`drafts/adoption-risks.md`.

## PROBLEM

The fish supplier substituted hake for the cod, so the cod dish has to come off and a
hake dish go on at a slightly higher price. Marisol does this on a Monday afternoon,
in the fifteen minutes between counting invoices and collecting her son. Today that
change reaches the printed menus whenever they are next reprinted and reaches the QR
menu never, because her nephew built it nine months ago; guests order dishes that no
longer exist and a server walks it back at the table. Separately, Eli starts on
Friday, and the only thing that currently happens before a new server's first shift is
that somebody hands him a pad — which means there is nothing to set up and equally
nothing stopping him from doing anything.

This epic gives Marisol both. She maintains categories and items with their
descriptions and prices, and a change she makes is what guests see the same evening.
She creates a user for each member of staff with a role attached, so a new server can
take orders and settle checks on his first shift without being able to change a price,
and a departed server's access ends when they do. It is deliberately narrow: no
modifiers, no combos, no dayparted menus, no scheduled pricing. At La Jarra's scale a
free-text note from the server covers the real special cases, and the whole setup has
to be something she can finish in one afternoon.

Scope boundary: this epic covers maintaining menu content, staff users and their
roles, and the table list. Whether a dish is available right now belongs to Item
Availability; using the menu to take an order belongs to Server Order Entry; the
guest-facing rendering belongs to Guest Menu; reporting and analytics are out of scope
for the product.

## ASSUMPTIONS

1. **An item is a name, a description, and a price, inside one category.** No
   modifiers, option groups, combos, dayparts, or scheduled pricing — confirmed
   excluded in the vision. No photos either, which is undecided. **Prices are entered
   tax-inclusive**: what Marisol types is what the guest pays, and no tax rate or
   service charge is stored anywhere, so a rate change means re-entering prices by
   hand.
2. **A price change does not re-price an open order.** Items are charged at the price
   they were ordered at. Undecided, and directly relevant because Marisol edits prices
   during the week.
3. **Deleting an item does not affect historical orders.** Past orders keep what was
   charged. Assumed, not stated.
4. **No menu version history.** There is no record of what the menu looked like last
   month or who changed it. Undecided, and it is the only audit trail Marisol would
   plausibly want.
5. **Roles are fixed: Admin, Server, Kitchen.** They cannot be created or customised,
   and a user has exactly one. The vision names three and no more.
6. **The Kitchen role is normally one shared login for the station**, not an account
   per cook, so kitchen actions are not attributable to an individual. Confirmed as
   the practical default in the vision.
7. **Deactivating a user is possible; hard deletion is not defined.** What happens to
   orders a departed server still owns is undecided, and connects to the unresolved
   admin-reassignment gap in Order and Table Lifecycle.
8. **Credential handling is unspecified.** Nothing in the vision says how a staff
   member gets or resets a password, whether Marisol sets it for them, or what happens
   when someone forgets it mid-service. Undecided and needed.
9. **The table list is admin-maintained here.** The vision binds orders to tables but
   never says where tables come from; this epic is the assumed home. Tables are
   identifiers only, with no capacity or layout.
10. **There is one restaurant and one menu**, with no multi-location or multi-tenant
    support — confirmed in the vision.
11. **Marisol is the only Admin in practice**, though nothing prevents more. Whether a
    second admin is expected is undecided.
12. **Admin has no visibility of service.** She cannot see the queue, order statuses,
    or a night's settlements from her own role beyond what the settlement epic exposes,
    and there is no reporting anywhere. This is the gap most likely to end her trial.

## FUNCTIONAL REQUIREMENTS

* **As Marisol, I want to maintain the categories my menu is organised into, so that
  the menu guests read is structured the way I think about it.**

    * Create, rename, reorder, and remove categories.
    * A category that still contains items cannot silently disappear.

* **As Marisol, I want to add and edit an item with its description and price, so that
  a menu change I make on Monday is live the same evening.**

    * Name, free-text description, and price, within one category.
    * The price entered is the price the guest pays, with no tax or service charge
      added at settlement.
    * The change reaches the guest menu and every staff device without anyone
      republishing anything.
    * No modifiers, sizes, or option groups.

* **As Marisol, I want to take an item off the menu permanently, so that a dish I have
  stopped making is gone rather than merely unavailable.**

    * Removal is distinct from marking an item unavailable for the night.
    * Orders already taken keep the item and its price.

* **As Marisol, I want to create a user for a member of staff with a role, so that a
  new hire can work their first shift with exactly the access they need.**

    * One role per user, from Admin, Server, or Kitchen.
    * A Server can take orders, mark items served, split and settle checks, and mark
      items unavailable, and cannot change the menu or prices.
    * Creating a user takes a couple of minutes, because the floor turns over
      regularly.

* **As Marisol, I want to deactivate a user, so that someone who has left cannot use
  the system the next evening.**

    * Deactivation takes effect on their next attempt to use it, whatever device they
      are on.
    * What they did before remains attributed to them.

* **As Marisol, I want to maintain the list of tables, so that servers can bind orders
  to the room as it actually is.**

    * Add, rename, and remove table identifiers.
    * A table with an open order cannot be removed.

* **As Marisol, I want to set the whole thing up in one afternoon, so that trying this
  product costs me a Monday rather than a migration.**

    * Entering a full menu, the table list, and the current staff is achievable in a
      single sitting with no assistance.
    * Nothing about the setup depends on my payment processor, my register, or my
      hardware supplier.

## NON-FUNCTIONAL REQUIREMENTS

* **Time to live.** A menu or price change is visible to guests and staff within 5
  seconds of being saved, with no republish step.
* **Setup effort.** A first-time setup of a fourteen-table restaurant — roughly forty
  items, the table list, and eight staff users — is completable by the owner alone in
  under two hours. This is the commercial premise of the product, not a convenience.
* **Credential security.** Staff credentials are stored so that a breach of the
  product's data does not expose usable passwords, and a deactivated user's access
  cannot be reused.
* **Attribution durability.** Actions remain attributed to the user who performed them
  after that user is deactivated.
* **Data protection scope.** The only personal data held is staff names and login
  credentials; no guest personal data exists anywhere in the product.
* **Admin surface.** The whole of administration is usable on whatever device Marisol
  has in the back office, without dedicated hardware.

## REQUIREMENTS SIZING

**Metric: story points on a modified Fibonacci scale (1, 2, 3, 5, 8, 13),**
consistent with the other 1-pagers. One point is a day or less of well-understood
work for one person; 13 means the story carries unresolved design as well as build.

| # | Story | Size | Rationale |
| --- | --- | --- | --- |
| 1 | Maintain categories | **3** | Straightforward, with ordering and the non-empty-category rule as the only wrinkles. |
| 2 | Add and edit items | **5** | The editing itself is ordinary; the requirement that a change is live everywhere with no publish step is what carries the cost, shared with the guest menu epic. |
| 3 | Remove an item permanently | **3** | Small, but it needs the distinction from unavailability and the guarantee that historical orders are untouched. |
| 4 | Create a staff user with a role | **8** | The largest story here, because it is where authentication lives: accounts, credentials, sessions, and role enforcement across three surfaces. Every other epic's access control depends on it. |
| 5 | Deactivate a user | **3** | Revocation that must take effect on a device already logged in, while preserving past attribution. |
| 6 | Maintain the table list | **2** | A simple list, with the open-order guard. Small only because tables carry no capacity or layout. |
| 7 | One-afternoon setup | **5** | Not a screen but a target: sequencing, sensible defaults, and bulk-friendly entry so forty items is not forty separate journeys. Sized for the design and testing effort. |

**Not sized, because they are unresolved rather than unestimated:** password reset and
credential delivery (assumption 8), menu change history (assumption 4), item photos
(assumption 1), and any reporting for the owner (assumption 12). Assumption 8 is a
blocker for story 4 — a staff account is not usable in practice until there is an
answer for a forgotten password at 7pm on a Friday. Assumption 12 is the commercial
risk: without any reporting, the buyer has no evidence the product worked, which is the
reason her trial is most likely to end.
