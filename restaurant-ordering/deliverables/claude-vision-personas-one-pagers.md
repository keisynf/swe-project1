# Product Vision, Personas, and 1-Pagers

**Product:** Restaurant Ordering & Status Platform
**Model:** Claude Opus 5 (Kiro CLI)
**Students:** Keisy Núñez and Ezequiel Buck
**Course:** CS 3365, Fall 2026, Project 1

---

## Product Vision

For the owner-operator of an independent dine-in restaurant, whose servers and cooks
lose time and accuracy every service because an order's real state is split between a
paper ticket, a server's memory, and what the kitchen has actually started cooking,
**Rail** is a table-to-kitchen ordering and status platform. It holds one shared,
item-level record of every order, which the floor and the line read from and write to
as the food moves. Unlike restaurant POS suites such as Toast or Square for
Restaurants, which bundle that coordination with card processing, proprietary
terminals, and a contract, Rail leaves payment alone. It runs on phones and screens
sold anywhere, so a kitchen can be working on it within a week without changing
processor or signing anything.

Rail is bought by the owner-operator who works the floor and signs the cheques. They
stop paying for plates remade from misread tickets and dishes sold after the kitchen
ran out, and they control the menu themselves. Buyer and users are different people,
so they keep paying only if the servers and kitchen actually use it.

"Rail" is a placeholder name. Scope and requirements live in the 1-pagers below.

---

## Personas

Five people, set in one fictional restaurant — *La Jarra*, fourteen tables, four
servers, three kitchen — so they can be read against each other. One buys the
product, three use it during service, and one only ever sees the menu.

What each person is frustrated by today, how they will judge the product, and why
they might reject it lives in `drafts/adoption-risks.md`, to keep these
descriptions short.

---

#### Marisol Ruiz — owner-operator

Marisol is 44 and has owned La Jarra for seven years, after twelve years working
other people's floors. She is divorced, has a teenage son who does homework in the
back booth on school nights, and the restaurant is both her income and most of her
waking life. She took two years of business classes at community college and did
not finish them; everything she knows about running a restaurant she learned
standing in one. She is comfortable but unsentimental about technology — the books
live in a spreadsheet she built herself, stock is ordered by text message, and the
card reader on the counter works well enough that she has no intention of
discussing it with anyone.

Her job is whatever the night requires. Monday afternoons are counts, invoices, the
rota, and a menu change because the fish changed. Tuesday through Saturday she is
seating guests, expediting, covering a section when someone calls out, and settling
checks at the register. She is also the person who apologises when a plate comes
back wrong and the person who absorbs the cost of remaking it.

What draws her to this product is that it is the first thing pitched to her that
does not want to touch how she takes money. She would keep her processor, her
reader, and her rate, and she could stop the specific losses that annoy her most:
plates remade because a ticket was misread, and dishes sold after the kitchen has
run out. She would use it on a Monday to fix prices and pull a dish herself,
without calling her nephew, and she would want to set the whole thing up in one
afternoon and be able to walk away from it in a week if her staff hated it.

#### Devin Okafor — server

Devin is 26, shares a flat twenty minutes from the restaurant, and has been serving
at La Jarra for eighteen months after four other restaurants. He has a bachelor's
degree in graphic design and still takes freelance work when it appears, which is
not often enough to quit; serving pays the rent, and the tips on a good Saturday
beat a week of client revisions. He is entirely at home with software. He judges an
interface in about ten seconds, has strong opinions about the ones he uses, and
will abandon a tool that takes more taps than the alternative without feeling any
need to explain why.

He works four or five shifts a week across four to six tables, nine on a Saturday,
and sometimes covers the bar. His hands are usually full. He is greeting an
arriving table while carrying two plates and holding in his head that table three
wants the sauce on the side. He writes on a pad in his apron, fires tickets at the
terminal by the kitchen door, and spends more of the night than he would like
standing at the pass asking whether table six's mains are up.

The product appeals to him for one reason above all others: he wants to know the
moment food is ready, so it goes out hot and he is not the reason it sat under a
lamp. He would fire orders from his section instead of walking to a terminal, type
a note on an item rather than trusting his handwriting, and see at a glance what is
cooking and what has been rejected. He would also want the end of the night to get
easier — splitting a six-top who shared a bottle and a platter, quickly enough that
no queue forms behind him. All of this only holds if entering an order is faster
than his pad, because that is what he is comparing it to.

#### Tom Baran — kitchen lead

Tomasz Baran, who everyone calls Tom, is 38 and has cooked for nineteen years,
three of them at La Jarra. He trained at a vocational culinary school in Kraków,
came over at 23, and worked up through hotel kitchens and two chain restaurants
before landing somewhere he is trusted to run the line. He lives with his partner
and their two young daughters, works six services a week, and is asleep by eleven.
His technical life is a phone: messages, football scores, and a banking app he uses
reluctantly. He is not bad with technology, he is uninterested in it, and he will
learn a tool in one service if it earns its place and ignore it permanently if it
does not.

He runs the line with two cooks, or alone on a slow Tuesday, and he calls the pass.
Tickets come off the printer, go on the rail left to right, and he moves them
around as timing changes — the rail is his working memory, and he reorders it by
hand constantly. He holds the rest in his head: what is on which burner, what is
about to be plated, which table has been waiting longest. His hands are wet,
gloved, or full, and the nearest screen would be across a hot room.

He would want this product for the interruptions it removes. Servers walk up to ask
him questions the rail already answers, and every one of them costs him focus he
cannot spare. He would want to see one clear queue from six feet away without
walking to it, tap an item to Ready and have the floor know, refuse an item he
cannot make and have that be visibly his call, and mark the salmon gone the moment
the last portion is plated so he never has to shout it twice. He would also want to
be told when something he has already started gets cancelled, rather than a ticket
vanishing off a board he has memorised.

#### Eli Whitaker — new server, first shift

Eli is 34, recently separated, and shares custody of a six-year-old, which is why
he took a job with evening shifts he can trade. He drove a delivery van for six
years and worked retail before that, and he has never waited tables. He finished
secondary school and did part of an apprenticeship he left when his first child was
born. He is fine with consumer technology — he lived inside a dispatch app for six
years and can learn a phone interface without help — but he has never touched
restaurant software, does not know what a POS is, and has no idea that "86" means
anything.

His job today is to be useful by the end of one shift. He has been given an apron,
a section of three tables, a printed menu he has annotated in his own shorthand,
and the instruction to ask Devin if he gets stuck. Nobody has time to train him
during service. He is learning the menu, the table numbers, where the glassware
lives, what the kitchen's abbreviations mean, and the app, all in the same six
hours, in front of paying guests.

What he needs from the product is for it to teach him the job rather than add to
it. He would want to open it and be able to take an order without asking how, see
the current menu in it so he stops flipping to the paper copy in his apron, and be
stopped before he sells something the kitchen has run out of, because that is the
mistake he is most afraid of making at a table. He would want to see where his own
tables' food has got to without asking a cook he is intimidated by. Most of all he
would want to be confident that a wrong tap cannot ruin a table's evening, because
if he is afraid of the screen he will write on paper and quietly hand his tickets
to someone more senior.

#### Priya Raman — guest

Priya is 31, a physiotherapist at a nearby clinic, and she is out with three
friends on a Friday evening for the second time this year. She has an MSc, a heavy
caseload, and a phone she uses constantly and impatiently. She is thoroughly
capable with technology, which is exactly why she has no tolerance for a website
that wastes her time: her standards were set by every other QR menu she has
scanned, and the test is whether it works in three seconds or whether she asks for
a paper one.

She has no job to do here. She is not a user of the system in any meaningful sense
— no account, no login, no record of her exists — and she will touch exactly one
thing, the code on the table.

She would scan it because reading a menu on her own phone is genuinely easier than
sharing one laminated copy between four people, and because she can look at it
while the others are still talking. What she wants from it is a page, not an app:
no install, no email, no loyalty prompt, readable in dim light without zooming,
with prices that match what she will be charged and without dishes the kitchen
cannot make. Then she wants to put the phone down and tell a person what she wants.
If the software works, she will not remember it exists.

---

## 1-Pagers

### Guest Menu 1-pager

**Epic:** the one page a paying customer ever sees, reached by scanning a code at
the table.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §15;
`drafts/adoption-risks.md`.

#### PROBLEM

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

#### ASSUMPTIONS

1. **One code for the whole restaurant**, printed identically on every table, with no
   table context in the scan. This page can never know which table it is being read
   at.
2. **No photos.** An item is a name, a description, and a price (Menu and Staff
   Administration). Whether dish photography is wanted is undecided, and it would
   change the page substantially.
3. **No allergen or dietary information, and no modifiers.** This is worth flagging
   beyond a scope note: a guest with an allergy gets nothing from this page and must
   ask a server, and Devin's scenario has an allergy in it.
4. **One language.** There is no localisation.
5. **Nothing about the guest is collected or stored** — no account, no identifier, no
   analytics, no cookies beyond what is technically unavoidable.
6. **No offline case.** A guest whose phone has no signal cannot read the menu, and
   the restaurant's wifi is weakest at the back of the room. Undecided whether that
   needs addressing, and it is the most likely way this page fails in practice.
7. **Printing and placing the codes is the restaurant's problem**, not the product's.
   The same code is printed on every table tent, but nothing generates or supplies
   it. Undecided whether the product produces a printable code at all.
8. **No fallback if the page is down.** Paper menus remain the fallback; the product
   provides none.

#### FUNCTIONAL REQUIREMENTS

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

* **As Priya, I want the menu to offer only dishes the kitchen can still make, so that
  I do not choose something and then be told no.**

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

#### NON-FUNCTIONAL REQUIREMENTS

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

#### REQUIREMENTS SIZING

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

### Server Order Entry 1-pager

**Epic:** taking an order at the table on a handheld and getting it to the kitchen
intact.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §4, §14;
`drafts/adoption-risks.md`.

#### PROBLEM

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

#### ASSUMPTIONS

1. **One open order per table at a time.** A second party at the same table starts
   a new order only after the first is settled. The merge capability suggests
   exceptions exist.
2. **Items are sent in explicit batches, not individually as they are tapped.**
   Devin composes the table's order and sends it in one action.
3. **No coursing.** Nothing is held back for later firing; what is sent enters the
   queue immediately.
4. **Covers, seat numbers, and guest names are not captured.** An order is attached
   to a table and a server, and nothing else.
5. **Repeated dishes are separate items, not a quantity field**, because each one
   can carry its own note and its own status. Undecided.
6. **A note can be edited until the item is sent, and not afterwards.** What happens
   when a guest changes their mind about a modification after firing is undecided.
7. **Any server can act on any order, not only the server who owns it.** Orders
   record their owner, but ownership restricts nothing. Undecided.
8. **Voiding an unsent item leaves no record; voiding a sent item becomes a
   Cancelled item** the kitchen is told about. The send action is the boundary
   between "removed" and "cancelled".
9. **No undo and no confirmation step.** Eli is the person
   this hurts, and fear of a mistap in front of guests is the specific mechanism by
   which he reverts to paper.
10. **No training mode.** A new server's first use is a live table.
11. **Order entry requires connectivity.** Whether a server can compose an order
    offline and have it send on reconnect is undecided, and the restaurant's wifi
    reaches the back of the room unreliably.
12. **Table identifiers already exist** and are maintained in Menu and Staff
    Administration.

#### FUNCTIONAL REQUIREMENTS

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

#### NON-FUNCTIONAL REQUIREMENTS

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

#### REQUIREMENTS SIZING

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

### Kitchen Queue and Item Status 1-pager

**Epic:** the shared record of where every ordered item stands, and the kitchen
surface that drives it.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §5, §10–13;
`drafts/adoption-risks.md`.

#### PROBLEM

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

#### ASSUMPTIONS

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

#### FUNCTIONAL REQUIREMENTS

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

#### NON-FUNCTIONAL REQUIREMENTS

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

#### REQUIREMENTS SIZING

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

### Item Availability 1-pager

**Epic:** taking a dish off the menu the moment it runs out, from wherever the
person who found out is standing.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §8, §11, §15;
`drafts/adoption-risks.md`.

#### PROBLEM

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

#### ASSUMPTIONS

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

#### FUNCTIONAL REQUIREMENTS

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

#### NON-FUNCTIONAL REQUIREMENTS

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

#### REQUIREMENTS SIZING

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

### Order and Table Lifecycle 1-pager

**Epic:** keeping an order attached to the right table and the right server as the
room and the roster change.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §6, §7;
`drafts/adoption-risks.md`.

#### PROBLEM

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

#### ASSUMPTIONS

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

#### FUNCTIONAL REQUIREMENTS

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

#### NON-FUNCTIONAL REQUIREMENTS

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

#### REQUIREMENTS SIZING

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

### Settlement and Splitting 1-pager

**Epic:** what the order cost, how it divides between guests, and recording that it
has been paid — without processing the payment.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §9;
`drafts/adoption-risks.md`.

#### PROBLEM

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

#### ASSUMPTIONS

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

#### FUNCTIONAL REQUIREMENTS

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

#### NON-FUNCTIONAL REQUIREMENTS

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

#### REQUIREMENTS SIZING

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

### Menu and Staff Administration 1-pager

**Epic:** the owner's control of what is on the menu, what it costs, and who can use
the system.
**Sources:** `personas/personas-claude.md`; `drafts/scenarios-claude.md` §1, §2, §3;
`drafts/adoption-risks.md`.

#### PROBLEM

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

#### ASSUMPTIONS

1. **An item is a name, a description, and a price, inside one category.** No
   modifiers, option groups, combos, dayparts, or scheduled pricing. No photos either,
   which is undecided. **Prices are entered
   tax-inclusive**: what Marisol types is what the guest pays, and no tax rate or
   service charge is stored anywhere, so a rate change means re-entering prices by
   hand.
2. **A price change does not re-price an open order.** Items are charged at the price
   they were ordered at. Undecided, and directly relevant because Marisol edits prices
   during the week.
3. **Deleting an item does not affect historical orders.** Past orders keep what was
   charged.
4. **No menu version history.** There is no record of what the menu looked like last
   month or who changed it. Undecided, and it is the only audit trail Marisol would
   plausibly want.
5. **Roles are fixed: Admin, Server, Kitchen.** They cannot be created or customised,
   and a user has exactly one.
6. **The Kitchen role is normally one shared login for the station**, not an account
   per cook, so kitchen actions are not attributable to an individual.
7. **Deactivating a user is possible; hard deletion is not defined.** What happens to
   orders a departed server still owns is undecided, and connects to the unresolved
   admin-reassignment gap in Order and Table Lifecycle.
8. **Credential handling is undecided.** How a staff member gets or resets a
   password, whether Marisol sets it for them, and what happens when someone forgets
   it mid-service are all open, and an answer is needed.
9. **The table list is admin-maintained here.** Tables are identifiers only, with no
   capacity or layout.
10. **There is one restaurant and one menu**, with no multi-location or multi-tenant
    support.
11. **Marisol is the only Admin in practice**, though nothing prevents more. Whether a
    second admin is expected is undecided.
12. **Admin has no visibility of service.** She cannot see the queue, order statuses,
    or a night's settlements from her own role beyond what the settlement epic exposes,
    and there is no reporting anywhere. This is the gap most likely to end her trial.

#### FUNCTIONAL REQUIREMENTS

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
      items unavailable and available again, and cannot change the menu or prices.
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

#### NON-FUNCTIONAL REQUIREMENTS

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

#### REQUIREMENTS SIZING

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
