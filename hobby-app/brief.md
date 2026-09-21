# NextHobby

Working description of the product.

## What it is

A website for finding a hobby that matches what you are in the mood for and what you can
actually commit right now, and then pointing you at where to begin. Every hobby carries
structured information about what it demands, so hobbies can be filtered and compared at a
glance instead of researched one at a time. Once a hobby is chosen, the product says what to buy
and where to learn.

The product does not teach and does not sell. It does not host lessons, and it does not supply
or ship materials. It is the index, not the library and not the store.

## The problem

Starting a new hobby is appealing. Choosing one is hard, and the hard part is not a shortage of
options. It is that what a hobby will demand of you is not knowable quickly.

What someone wants varies by occasion. Sometimes the appetite is for something cheap, quick, and
undemanding that fits into the gaps of a week. Sometimes it is for something physically hard.
Sometimes the binding constraint is money, or space, or how much sustained attention is
available. The appetite is usually clear. The information needed to match it is not.

Finding out what a hobby actually requires means reading scattered prose across videos, forums,
and retailer pages, one hobby at a time, then trying to hold the answers side by side in your
head. There is no way to ask the obvious question: show me hobbies that cost under this much,
need under an hour per session, and are physically demanding. The information exists in the
world. It is not structured, not comparable, and not fast to get.

The same is true after choosing. Learning material is abundant and free, but which video to
start with, and what to buy before you can follow along at all, are questions you answer by
trial and error.

## The effort profile

Every hobby carries an explicit profile across four axes. These are what you filter, sort, and
compare on, not just what you read once you arrive.

| Axis | What it captures |
|---|---|
| Monetary | Cost of entry, separated into minimum viable outlay versus typical outlay, plus ongoing consumable cost |
| Time | Session length, realistic frequency, and time to a first result worth keeping |
| Physical | Strength, stamina, dexterity, mobility, and the space, noise, ventilation, and storage the hobby demands |
| Mental | Learning curve steepness, tedium tolerance, frustration tolerance, and how much sustained focus a session needs |

High demand on an axis is not a negative. A user who wants something physically punishing or
deeply absorbing is searching for that, not avoiding it. The axes describe hobbies rather than
rank them.

## Getting started

For each hobby, two things beyond the effort profile.

**What to buy.** A starting kit list, specific enough to act on. For crochet that means hooks in
sizes 4, 5, and 6 and named yarn weights, not "hooks and yarn." Separated into the minimum
needed to find out whether you like the hobby versus what you want if you stay with it.

**Where to learn.** Pointers into learning material that already exists, with enough direction
to be useful: for crochet, look up videos on basic stitches, and here is where to start. The
product curates and orients. It does not produce the lessons.

## Open questions

- Where effort data comes from: author declaration, community aggregation, derivation from the
  kit list, or some combination, and how it stays accurate
- The kit list gives the monetary axis a concrete basis, since a priced list of items is a cost.
  Whether monetary demand should be derived from the kit rather than declared separately
- Prices and availability vary by region and over time. Whether the product states specifications
  and lets the user source them, links to retailers, or tracks prices
- Curated external links decay. Videos are deleted, channels go quiet, better material appears.
  Who notices and who fixes it
- How resource quality is judged, given that "here is where to start" is a recommendation the
  product is staking its credibility on
- Effort to a first result and effort to genuine proficiency are different numbers. Whether the
  product shows one, both, or a curve
- Cross-hobby comparability requires a consistent scale. What makes woodworking's physical
  demand legitimately comparable to watercolor's
- How a user expresses appetite: a saved profile, a per-visit query, or a short intake
- It is a website, not a native mobile application. Whether the layout is designed for phone
  browsers first is still open, and it matters, since browsing hobbies and checking a kit list
  while standing in a craft store are plausible uses

## Competitive landscape

Checked September 2026. Two kinds of alternative, and they need different answers.

**Content sources.** YouTube tutorials, hobby subreddits and forums, Skillshare and Udemy,
Pinterest, Meetup for local groups, and retailer starter guides. Several are free and all have
more instructional content than this site will ever have.

This site does not compete with them on content. It points into them. The structural gap it
fills is that all of them hold what a hobby demands as prose, scoped to one hobby at a time, and
prose cannot be filtered, sorted, or compared. Nor does any of them tell you what to buy and
which video to open first, in one place, before you have committed to anything.

**Direct competitors.** Hobby matching products already exist, and several are close to this
idea. Descriptions below are paraphrased from each site.

- [pastime.com](https://pastime.com/): a seven-question intake on time, budget and energy,
  matching against a catalog of 176 hobbies, each scored on what starting it actually takes.
  The closest existing product to this one.
- [allthehobbies.com](https://allthehobbies.com/): a short AI quiz covering personality,
  schedule and budget, followed by guided courses and a community of beginners. Bundles the
  teaching this site declines to do.
- [sidequest.ink](https://sidequest.ink/): matching filtered against the user's real
  circumstances, plus guided starting and coaching from zero.
- [findyourhobby.org](https://findyourhobby.org/): suggestions derived from available time,
  budget, interests, goals and location, presented with reasoning and a starting plan.
- [HobbyDex](https://hobby-dex.com/): a hobby tracker with game mechanics, built around
  hobbies you have already picked rather than around the choice itself.

**What this means for the differentiator.** Matching hobbies on effort is not by itself a
distinguishing feature, because several products already do it. The differentiation has to come
from something narrower. Candidates, none of them settled yet:

- A browsable reference you return to and compare within, rather than a one-shot quiz that hands
  you a single answer and is done
- Kit lists specific enough to shop from, naming hook sizes and yarn weights, rather than a
  general starting plan
- Declining to teach or sell, which means recommendations can point at the best free material
  anywhere instead of routing users into the site's own courses
- Four separately scored axes, with mental and physical demand kept distinct, rather than one
  blended measure of energy or effort

## Who it is for

- The repeat starter who enjoys taking up new hobbies and wants to pick well without a research
  project each time
- Someone with a specific appetite to satisfy, such as wanting something physically demanding
- Someone bounded by one axis: tight budget, small apartment, limited mobility, or fragmented
  time such as 20 minute windows
- An experienced hobbyist who wants to contribute the effort data, kit list, and starting
  pointers for their hobby
- Whoever keeps it trustworthy, since the value collapses if the numbers are wrong or the links
  are dead

## Scope and phasing

The filterable effort data, the matching experience, the kit lists, and the curated starting
pointers are the core and need to be specified in buildable detail.

Explicitly out: hosting or producing lessons, selling or shipping materials, and fulfillment of
any kind.

Community contribution, revision history, and moderation are real parts of the product but
should stay separable so they can be deferred.
