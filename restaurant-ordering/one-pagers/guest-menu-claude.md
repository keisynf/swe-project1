# Guest Menu 1-pager

**Epic:** the one page a paying customer ever sees, reached by scanning a code at
the table.
**Sources:** `vision/vision-statement-claude.md` §5.1, §8.1;
`personas/personas-claude.md`; `drafts/scenarios-claude.md` §15;
`drafts/adoption-risks.md`.

## PROBLEM

Priya sits down with three friends and there is one code on the table. Her standards
were set by every other QR menu she has scanned: a PDF she has to pinch and drag
around, or a link that wants her email before showing her a starter. Her budget is
about three seconds, after which she asks for a paper menu, and the restaurant's
first impression is a bad one. La Jarra's current alternative is one laminated menu
passed between four people, which works but slowly, plus a QR menu Marisol's nephew
built nine months ago that still lists dishes the kitchen no longer makes and prices
that have since changed.

This epic is deliberately the shallowest surface in the product. A single
restaurant-wide code opens the current menu on the guest's own phone: categories,
items, descriptions, prices, and nothing that has run out. There is no cart, no
submit button, no account, no identifier, and no order status — guests decide what
they want and tell their server, which is what Priya wants anyway. The value to
Marisol is that the menu is never stale again and the code never needs reprinting
when the fish changes; the value to the restaurant is that four people read the menu
at once instead of passing one copy around.

Scope boundary: this epic covers reaching and reading the menu as a guest. What is on
the menu and what it costs is maintained in Menu and Staff Administration; whether an
item is currently available is Item Availability, which this page reflects; ordering
is the server's job in Server Order Entry, and guest self-ordering, guest-visible
order status, and guest accounts are all explicitly out of scope for the product.

## ASSUMPTIONS

1. **One code for the whole restaurant**, printed identically on every table, with no
   table context in the scan. Confirmed in the vision, and it means this page can
   never know which table it is being read at.
2. **No photos.** The vision defines an item as a name, a description, and a price.
   Whether dish photography is wanted is undecided, and it would change the page
   substantially.
3. **No allergen or dietary information, and no modifiers.** Excluded from v1 by the
   vision. This is worth flagging beyond a scope note: a guest with an allergy gets
   nothing from this page and must ask a server, and Devin's scenario has an allergy
   in it.
4. **One language.** No localisation is mentioned anywhere.
5. **Nothing about the guest is collected or stored** — no account, no identifier, no
   analytics, no cookies beyond what is technically unavoidable. Assumed from the
   vision's insistence that guests have no record.
6. **No offline case.** A guest whose phone has no signal cannot read the menu, and
   the restaurant's wifi is weakest at the back of the room. Undecided whether that
   needs addressing, and it is the most likely way this page fails in practice.
7. **Printing and placing the codes is the restaurant's problem**, not the product's.
   The vision says the same code is printed on every table tent but nothing generates
   or supplies it. Undecided whether the product produces a printable code at all.
8. **No fallback if the page is down.** Paper menus are assumed to still exist, but
   nothing in the product says so.

## FUNCTIONAL REQUIREMENTS

* **As Priya, I want to scan the code on the table and land on the menu, so that I can
  read it on my own phone without being asked for anything.**

    * One scan opens the menu directly; no app, no install, no sign-up, no email, no
      loyalty prompt.
    * Nothing identifies me, and nothing is kept about me.
    * The same code works at every table.

* **As Priya, I want to read the whole menu on a phone, so that I can decide while my
  friends are still settling in.**

    * Items grouped by category, each with its description and price.
    * Usable one-handed on a phone held at the table.

* **As Priya, I want dishes the kitchen has run out of not to be offered, so that I do
  not choose something and then be told no.**

    * Unavailable items are not presented as choices.
    * A dish that runs out while I have the page open stops being offered without me
      reloading or rescanning.

* **As Priya, I want the prices I read to be the prices I am charged, so that the
  check holds no surprises.**

    * The page shows the current menu price for every item.
    * Prices are tax-inclusive, so the figure I read is the figure I am charged, with
      nothing added at the end.
    * A price Marisol changes is reflected the same evening.

* **As Marisol, I want one code that never needs reprinting, so that changing the menu
  never means reprinting anything.**

    * Menu changes appear to guests without the code changing.
    * No per-table setup, so a new table tent is a copy of the same code.

## NON-FUNCTIONAL REQUIREMENTS

* **Time to readable menu.** From scan to a readable menu in under 3 seconds on a
  mid-range phone over the restaurant's wifi or mobile data. Past that, guests ask for
  paper, which is the failure condition for this epic.
* **Legibility on a phone.** The whole menu is readable at a phone's default zoom in
  low restaurant lighting, without pinching, zooming, or horizontal scrolling.
* **Freshness without interaction.** A menu left open for the length of a meal
  reflects availability and price changes without the guest reloading it.
* **Guest privacy.** No guest is identifiable from anything the product stores, and no
  personal data is requested at any point.
* **Availability during service.** The page is available throughout opening hours; an
  outage during service is visible to every guest in the room simultaneously, which
  makes it the most publicly damaging failure in the product.
* **Device reach.** Works on current mainstream phone browsers without installing
  anything.

## REQUIREMENTS SIZING

**Metric: story points on a modified Fibonacci scale (1, 2, 3, 5, 8, 13),**
consistent with the other 1-pagers. One point is a day or less of well-understood
work for one person; 13 means the story carries unresolved design as well as build.

| # | Story | Size | Rationale |
| --- | --- | --- | --- |
| 1 | Scan the code and land on the menu | **3** | Little logic: a public route with no authentication and nothing to remember about the visitor. Most of the cost is the load-time target. |
| 2 | Read the whole menu on a phone | **5** | The only surface a paying customer sees, so presentation quality is the requirement rather than a nicety. Sized for layout and legibility work, not data. |
| 3 | Unavailable dishes not offered | **3** | Filtering is trivial; keeping an already-open page current is the real work, and it is shared with the Item Availability epic — count it once across the two. |
| 4 | Prices are current | **2** | Falls out of reading from the live menu, provided the administration epic keeps one source of truth. |
| 5 | One durable code | **1** | A single public URL. Almost free, and only this small because per-table codes were ruled out. |

**Not sized, because they are unresolved rather than unestimated:** photos
(assumption 2), allergen and dietary information (assumption 3), any offline or
no-signal handling (assumption 6), and generating a printable code (assumption 7).
Assumption 3 deserves a decision rather than a deferral: an allergy is a safety
matter, and the product currently routes it entirely through a server's memory and a
free-text note.
