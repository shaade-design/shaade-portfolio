# Idea Sheet Redesign
### UserVoice · Product Design · Sole IC Designer · Multi-cycle effort

**What came before:** Admin Grid Console Overhaul
**What this unlocked:** AI Summaries · Internal Chat · Idea Owner · Impact Reports

---

## The setup

The grid got admins to the right idea. The Idea Sheet is where they figured out what to do with it.

It was the second most visited page in the product — 700K+ page views a year, over 13 minutes average time on page. Admins weren't bouncing. They were working. Reading activity, parsing comments, updating statuses, trying to understand what a piece of feedback actually meant before deciding what to do next.

The page had everything. It just had no way of telling you what mattered.

---

## 01 — The constraint you had to solve first

Before any design work could happen, there was a technical wall.

When the Idea Sheet was first built, the team forked Angular UI Router. That decision had compounded for years — it blocked Angular updates, blocked the React migration, and meant you couldn't meaningfully change the layout without first replacing the component underneath it.

So that's where we started. Product, engineering, and I aligned on replacing it with React Dock before touching the design. Not a win on its own — just what had to happen first. Same situation as the grid, same approach: unblock the technology, then do the work.

*[IMAGE: before state — old Angular Idea Sheet]*

---

## 02 — Research & Validation

This wasn't designed in a vacuum. Before touching a layout, I ran moderated interviews with 8+ admins across Procore, Netflix, Zendesk, Greenhouse, Xero, SmartRecruiters, Mitel, and PandaDoc — power users, occasional visitors, large enterprises, smaller teams.

The interviews were structured around jobs to be done — not "what do you think of this design" but "walk me through the last time you opened an idea." That framing surfaced things a survey never would.

I layered those findings against Heap analytics — heatmaps and path data showing what admins actually did, not what they said they did. Interviews told me why. Data told me how often.

The Options dropdown is a good example of why both mattered. It came up constantly in interviews as something admins relied on. Heap confirmed it — 12% of all post-view clicks went straight into that menu. But the interviews explained why that was a problem: nobody could predict what was inside it.

Before Part 1 shipped we ran prototype sessions with a subset of participants. The removed features weren't noticed or missed. Buried actions started getting used — merge match came up unprompted. After launch we iterated on feedback as real usage surfaced edge cases. Testing was part of the process, not a checkpoint at the end.

> *"Cleaner, more modern look — stuff is front and center."*
> — Product Manager, Zendesk

> *"I'd like to tuck away the metadata stuff, to focus on the activity entries."*
> — Product Manager, Greenhouse

*[IMAGE: annotated before state — options menu overload, buried revenue data, indistinct comments]*

---

## 03 — How I approached it

**Separate reading from acting.** The most clarifying decision: split the page into two zones. Left for read content — description, activity, metrics, the story of the idea. Right rail for admin actions and idea state — statuses, labels, custom fields, integrations. Once that delineation was clear, everything else fell into place.

**Explode the Options menu.** The dropdown was doing too much — 12% of all post-view clicks went into a menu that buried edit, merge, status updates, outreach, and delete side by side with no hierarchy. I surfaced the most-used actions into the right rail and reduced the Options menu to what was truly secondary.

**Reduce modal takeover.** The old sheet launched full-screen modals for almost every action. I introduced slide-in panels — status updates, outreach, commenting — that stayed anchored to the sheet. Context preserved. A deliberate step toward the slideout pattern that would later spread across the product.

**Subtract before you add.** Analytics told us which features weren't being adopted. We dropped them — not tucked away, dropped. Unused features add cognitive load even when they're not being clicked.

**Design for the scroll.** Sticky navigation anchored key idea information — title, status, key metrics — as admins scrolled through long activity feeds. Borrowed from mobile scrolling patterns. A small decision that made a large difference.

---

## 04 — Three parts, not one

This wasn't a single redesign. It was three separate pitches, sequenced deliberately.

**Part 1 — The shell and right rail.**
Replace the Angular sheet component with React Dock. Redesign everything except the activity feed — the right rail, quick actions, status, labels, tabs, the two-zone layout. The activity feed stayed as-is because it was its own complex Angular component, outside the scope of this cycle.

**Part 2 — The activity feed.**
Its own pitch, its own complexity. Internal and external activity made visually distinct. Iconography introduced to differentiate user types, accounts, revenue. Quick filter tabs — Comments & Feedback, Internal Comments, All Activity. Improved scannability for high-volume feeds.

**Part 3 — The inner tabs.**
Users, Accounts, Features, Validation, and SFDC Opportunity tabs all still running old designs after parts 1 and 2 shipped. Updated to match the new design language. User Detail and Account Detail pages redesigned to match. One system, propagated across the product.

This sequencing mirrors what we did on the grid — target the highest-impact piece first, leave the complex Angular component for a separate cycle, build forward iteratively.

*[IMAGE: after state — full sheet, two-zone layout visible]*

---

## 05 — What shipped

*[CIRCLE GRID — 6 circles]*

**01 — Two-Zone Layout**
Read left, act right — the IA decision that structured everything else.

**02 — Right Rail Actions**
Status, labels, custom fields, integrations — persistent and one click regardless of scroll position.

**03 — Status Updates**
Hidden by default, expandable on demand. Progressive disclosure at the component level.

**04 — Activity Feed**
Iconography distinguishing internal from external, user type from account type.

**05 — Sticky Navigation**
Title and key state anchored as admins scroll deep into the activity feed.

**06 — Design Language**
Color system, revenue badges, source attribution — carried forward from the grid.

---

## 06 — The connective tissue

The Idea Sheet didn't just inherit the grid's visual language — it extended the interaction philosophy.

The grid introduced the filter drawer as a slide-in pattern for exposing complexity without navigating away. The sheet introduced slide-in panels for actions — a stepping stone between full modal takeover and the full slideout that would later appear in bulk actions. Each project pushed the pattern one step further.

The color system, status pills, and iconography carried forward deliberately. An admin who'd learned to read the grid could read the sheet without relearning anything. That consistency wasn't visual tidiness — it was reduced cognitive load across the whole product.

> *"It was a way of keeping an eye on the chatter."*
> — Product Manager, Procore

---

## 07 — What it made possible

The first redesign established the foundation. What came next was built on top of it.

With the sheet now in React, we could move faster. The component library was reusable. The design language was consistent. The two-zone structure created natural homes for new capabilities.

The second round was informed by heatmapping data and a shift in how admins were beginning to think about ideas. Not just individual ideas, but groupings. Themes. Patterns across the backlog. The work was scoped and slated — designs in progress when the project paused.

That shift pointed toward AI: an overview landing page with AI-generated problem/solution/why it matters summaries. An activity feed that could summarize recent changes rather than requiring admins to scroll through every entry. Internal chat with @ mentions replacing internal comments. Idea Owner as a native field. AI label recommendations.

The sheet wasn't just a management tool anymore. It was becoming an intelligence layer — a place where the product could help admins understand what a piece of feedback meant, not just store it.

*[IMAGE: AI overview page mock]*
*[IMAGE: internal chat / @ mentions mock]*

---

## 08 — What I'd tell you

**The IA decision is the design decision.** Reorganizing elements within a broken structure doesn't fix the structure. The two-zone split — read left, act right — sounds obvious in retrospect. It took eight interviews and click analytics to see it clearly enough to commit to it.

**Sequence the work like you sequence the design.** Three separate pitches, each scoped tightly, each building on the last. The activity feed wasn't in scope for Part 1 because it was too complex. Trying to do everything at once would have meant shipping nothing. Bounded work ships.

**Subtraction is a design skill.** Every feature we removed was something engineering had built and someone had once believed in. Dropping them based on analytics rather than sentiment is harder than adding new ones. But unused features add noise even when they're not being used.

**One step at a time builds the pattern.** The slide-in panels weren't the end state — they were a deliberate step toward it. Two years later the slideout pattern was everywhere in the product. The direction was clear from the first cycle; each iteration moved closer.
