# Adoption risks and evaluation criteria — by person

Working notes, organised by person, extracted from the first draft of the
personas. This material was cut from the persona descriptions to keep those short,
and is kept here because it belongs in the one-pagers: what each person is
frustrated by today, what they will actually use to judge the product, and the
specific reasons they might reject it.

The rejection reasons are the useful part. Most of them are consequences of
product decisions, not speculation.

---

## Marisol Ruiz — owner-operator (the buyer)

**What frustrates her today.** The same failure repeats every week: a ticket is
misread, a plate comes back, she eats the cost and apologises to the table. She
cannot answer "how long on table 6?" without walking to the pass herself. When she
is not in the building she has no idea how service actually went. Every POS she has
been pitched wants to replace her card processing, sign her to a contract, and sell
her their hardware — the pitch always ends at money she does not want to spend on a
problem she did not describe. Her printed menu and the QR menu her nephew made are
nine months out of sync.

**How she will judge it after a month.** Fewer comps and remakes, which she will
feel in the till before she can prove it. Servers not queueing at the pass to ask
questions. No "we're out of that" conversation at a table after the order was
taken. And the new server who started on Thursday being useful on Thursday.

**Why she might reject it.**

- **She cannot see whether it worked.** Reporting is out of scope, so she is asked
  to believe service improved on feeling alone. She is a numbers person about cost,
  and this is the gap most likely to end a trial.
- **Settling twice.** Marked paid in the product, then taken on her existing
  terminal. That is genuine double entry at the busiest moment of the evening, and
  if it adds ten seconds per check she will notice.
- **Two systems instead of one.** A POS rep will tell her a single vendor is
  simpler, and on that narrow point the rep is right.
- **Staff not adopting it.** If her servers quietly go back to a notepad, she has
  paid for a screen nobody looks at.

---

## Devin Okafor — experienced server

**What frustrates him today.** Walking to the pass to ask about a table four or
five times a night, interrupting a cook who is busy. Finding out a dish is 86'd
*after* he has sold it. His handwriting being the reason a steak came out wrong.
Four guests wanting to split a shared bottle and a platter three ways while two
more tables wait for him. Food sitting ready at the pass because nobody told him.

**How he will judge it after a week.** Trips to the pass per shift, down to near
zero. No plate sitting ready without him knowing. Closing out a split six-top
without a queue forming behind him. Not having to apologise for something the
kitchen misread.

**Why he might reject it.**

- **He will not be told his food is up.** Notifications are in-app only, with
  nothing pushed to a sleeping handheld. If the phone is in his apron, "Ready"
  waits until he looks, so the kitchen belling the pass is still how he finds out —
  which undercuts the main thing he wanted. This is the single largest adoption
  risk in the product.
- **Any friction in order entry.** A pad is fast and never loads. Every extra tap
  is a reason to stop using this mid-shift.
- **A handheld is one more thing to hold** with two plates in his hands, and one
  more thing to have die at 9pm.
- **Split flows that fight him.** If dividing a shared bottle takes more than a few
  taps, he will do it on paper and enter the result.

---

## Tom Baran — kitchen lead

**What frustrates him today.** Servers at the pass asking questions the rail
already answers. Handwriting, where a misread modifier wastes a portion and his
time. Cooking something for ten minutes before learning the table cancelled it.
Selling out of a dish and watching three more tickets for it arrive anyway. Plates
going cold at the pass because the floor did not hear him call.

**How he will judge it after a service.** How many times a server walked up to ask
him something. Whether anything came back to the line as a remake. Whether he
cooked anything that had already been cancelled. Whether he had to shout "86" more
than once.

**Why he might reject it.**

- **A screen he has to touch with dirty hands.** The pass tablet lives in the
  splash zone. If it needs precise taps or wakes slowly, it ends up ignored under a
  towel.
- **Alerts on every single item.** A busy Saturday fires constantly. If it chirps
  at everything, he mutes it on the second night and the queue becomes a display he
  occasionally glances at.
- **Losing the paper rail.** He has nineteen years of muscle memory in physically
  reordering tickets as timing changes. A fixed-order digital queue that cannot be
  rearranged is worse than the rail, not better. This is a live requirement gap,
  not just a risk.
- **Depending on the floor to look at their phones.** If servers do not see
  "Ready," food sits and he gets blamed for cold plates he finished on time.
- **One shared kitchen login means no accountability**, which he may see as a
  feature and Marisol may eventually see as a problem.

---

## Eli Whitaker — new server, first shift

**What frustrates him today.** Everything is new at once: the menu, the table
numbers, the abbreviations other people use, where the glassware lives, and now
software. Nobody has time to train him during service, so he learns by asking
Devin between tables and by getting things wrong in front of guests. He carries a
printed menu in his apron with his own notes on it because he cannot remember
which dishes have the pickled onion.

**How he will judge it at the end of his first shift.** Whether he could take an
order without asking someone how the app works. Whether he got through a table
without apologising for the system. Whether it told him a dish was unavailable
before he embarrassed himself. Whether he felt faster at 9pm than he did at 6pm.

**Why he might reject it.**

- **Learning the app competes with learning the job.** On day one his attention is
  spent on the menu and the floor. Every concept the software makes him learn —
  statuses, splits, table binding — is attention taken from that.
- **Jargon with no explanation.** "86", "Rejected vs Cancelled", "derived order
  status", and "the pass" mean nothing to him. A UI that assumes restaurant
  vocabulary teaches him nothing and leaves him guessing.
- **Fear of breaking something in front of guests.** If a mistap sends the wrong
  order to the kitchen or cancels an item with no obvious undo, he will fall back
  to paper and hand his tickets to a senior server — invisible to Marisol, and it
  hides the product's failure.
- **No safe place to practise.** There is no training mode, so his first real use
  is a live table on a Friday.
- **Being the slowest person on the floor.** If the app makes him visibly slow, the
  social pressure alone pushes him back to a notepad.

---

## Priya Raman — guest

**What frustrates her today.** QR menus that open a PDF she has to pinch and drag
around. Links that want her email before showing her a starter. Prices that are out
of date, which feel like a small deception even when they are only carelessness.
Ordering flows that try to replace her server when she would rather talk to a
person.

**How she will judge it.** She will not consciously judge it at all, which is the
target. Success is that she reads the menu, orders from a person, and never thinks
about the software. The only signals available are negative: asking for a paper
menu, or being told at the table that something she picked is off.

**Why it might fail for her.**

- **A slow or awkward page.** Three seconds and no pinch-to-zoom is the whole
  budget; past that she asks for paper.
- **Stale prices**, which reach her as a surprise on the check.
- **No status view**, so "where is my food?" always goes through a human. That is
  deliberate, but it means the value of the status model is only ever felt
  second-hand by the person actually waiting for the food.
