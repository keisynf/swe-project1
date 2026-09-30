# Model Critique: Restaurant Ordering and Status Platform

Two models produced the same set of documents from the same starter prompt (`starter-prompt.md`):

- **Claude:** Claude Opus 5, in Kiro CLI.
- **OpenAI:** gpt-5.6-terra.

Each model worked in its own session and wrote its own vision, personas, and 1-pagers. The full record of each run is in `prompt-logs/`, and the vision drafts are in `drafts/`.

## At a glance

| | Claude | OpenAI |
|---|---|---|
| Prompts logged | 21 | 23 |
| Scope questions asked before drafting | 10 | 7 |
| Longest vision draft | 3,289 words (v9) | 1,504 words (v3) |
| Final vision | 387 words | 273 words |
| Personas | 5 | 5 |
| Scenarios | 15, in `drafts/scenarios-claude.md` | none as a separate file; each 1-pager's PROBLEM section is written as a scenario |
| 1-pagers | 7 | 5 |
| User stories | 48 | 23 |
| Story points | 193 | 125 |

The two products differ in scope. Claude's covers check splitting, table moves and merges, and order handoff between servers. OpenAI's has none of these, but it adds modifiers, quantities, rejection reasons, and a bill that can be regenerated and must be current before an order closes. Neither scope is wrong, since both come from the same brief and my answers to each model's questions.

## Part 1: Critique of the specifications

### Vision

Both final visions follow Sommerville's advice that a vision be "simple and succinct". Both use Moore's template and end with a paragraph about the buyer, as the iLearn example does.

- **Claude's vision** is sharper. It names a competitor (a full POS suite) and a real point of difference: payment is deliberately left out, so the restaurant can trial the product with no contract or processor switch.
- **OpenAI's vision** is generic. Its UNLIKE clause compares the product against "disconnected menus, paper tickets, and verbal handoffs", which is the problem restated rather than a competing product. A reader cannot tell from it why a restaurant would choose this product over an existing one.

### Personas

After revision, both sets meet Sommerville's four aspects: personalization, job, education and technical skill, and relevance. Both include the buyer and a new server, so a product feature can be checked against a user who has no experience.

- **Claude's personas** are more specific. Each personal detail explains how the person would use the product: Tom's wet hands and his habit of reordering the paper tickets by hand, Devin's full hands, and Priya's three-second patience.
- **OpenAI's personas** became concrete only after a second correction. Even then, they describe what each person would do with the product in general terms rather than tying it to a physical detail of their work, the way Claude does with Tom's wet hands.

### 1-pagers

**PROBLEM sections.** Claude's read like Sommerville's scenarios, with a named person, a moment in service, and what goes wrong on paper. OpenAI's name the personas but describe a need more than a situation.

**Assumptions.** Claude records many items as "Undecided" and names the ones that block a story, for example password reset blocking staff accounts. OpenAI settles more of them by declaring them "outside this release". Claude's approach suits a milestone whose next step is refining requirements. OpenAI's is easier to build from, but some of its exclusions are decisions made without me.

**Functional requirements.** Both write stories in the template's form with persona names. OpenAI's stories are larger (about 5.4 points each, against 4.0 for Claude) and its acceptance criteria are more uniform. Claude's criteria include more edge cases, such as two cooks tapping the same item at once, or a price change during an open order.

**Non-functional requirements.** OpenAI is stronger here. Every NFR states a percentile target (for example, 95% of availability changes appear within 3 seconds), says how to test it, and marks unvalidated numbers as assumptions. Claude's NFRs needed a correction round to remove design prescriptions and untestable wording, and one still cannot be tested: "fast enough that no queue of waiting tables forms".

**Sizing.** Both use Fibonacci points with one point defined as a day or less of well-understood work. Claude's rationales are specific to each story and list the items it left unsized because they are unresolved. OpenAI's rationales are accurate but formulaic. OpenAI also needed two corrections: once to re-estimate instead of keeping the old numbers, and once when it inflated the bill story to 13 points.

## Part 2: Critique of the models

### Where Claude did well

- **It found problems in its own work.** When I chose a TV for the kitchen, Claude pointed out that a TV cannot accept the status changes the kitchen owns, and asked how cooks would enter them. When I dropped push notifications, it recorded that this weakens two of its own success measures.
- **It did not guess at ambiguous answers.** It recorded typos and unclear answers as open questions, and pointed out when my "No" answered a different question from the one it asked.
- **It never lost a decision.** Everything I decided in conversation reached the documents.
- **It widened checks without being told.** When asked for four missing scenarios, it found six gaps and reported the two it did not write. While writing the 1-pagers, it raised tax, password reset, and the table list as blockers before I noticed them.

### Where OpenAI did well

- **It applied a Moore-style statement unprompted** in its first draft. Claude only did so after I asked, at v7.
- **It generalized from a single example.** I gave it one broken case in the order-status table (delivered drinks with ready mains). It rewrote the whole table as precedence-ordered rules, which fixed other cases I had not mentioned.
- **It planned before writing.** Asked to list its epics first, it found a story that belonged in another epic and moved it rather than counting it twice.
- **It wrote testable quality requirements** from the first draft onward.
- **It stayed concise.** Its longest vision was under half the length of Claude's.

### Where each fell short

- **Both defaulted to UX-template personas.** Both wrote them with Goals, Needs, and tables, which Sommerville argues against. Both fixed this once told.
- **Neither looked at competitors without being asked.** Claude produced a good comparison once asked. OpenAI never produced one.
- **Both let the vision grow into a specification.** Each decision was added to the vision until both had to be cut back after the 1-pagers existed.
- **Claude wrote too much.** The v9 vision is 3,289 words, and its log summaries are longer than they need to be.
- **OpenAI's conversation was better than its documents.** It proposed a `closed` state, an order-status rule, and who owns each transition in chat, then left all three out of the revised vision until I asked for them.
- **OpenAI made surface fixes.** When asked for a first-day story for Marcus, it renamed Daniel's delivery story instead of writing a new one. When given a new sizing definition, it kept the old numbers. When its personas were audited against the vision, it removed tables from the personas, when the right fix was to add tables to the product.

### Which prompts worked better

- **Directive prompts that gave the reason behind each correction** worked for both models. An example is Claude's four NFR corrections, each saying why the item was wrong.
- **One concrete example** worked better than asking a model to "find every mismatch". OpenAI's audit prompt found real gaps, but it chose the wrong way to resolve one of them.
- **Asking for a plan before a large write** prevented duplication, as with OpenAI's epic list.
- **Short open prompts** such as "let's create the personas" produced template output from both models. That output then needed a correction round each time.
- **Format constraints taken from the book** gave both models the same result: 2 or 3 paragraphs of prose, no goals, and the four aspects to cover. This was the most reliable prompt in either run.

## Verdict

Claude was the better product manager simulator overall. It caught contradictions in its own work, kept every decision, and wrote scenarios and problem statements that follow Chapter 3 closely. Its weaknesses were length and loose non-functional requirements, and both are cheap to fix. OpenAI was better at testable quality requirements and concise writing. However, it needed me to find the decisions it dropped and the rules that broke, which is the work a product manager is supposed to do.

For Milestone 2, I recommend the Claude set as the base, with OpenAI's non-functional requirements as the model for tightening Claude's.
