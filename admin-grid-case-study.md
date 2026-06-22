# Admin Grid Console Overhaul
### UserVoice · Product Design · Sole IC Designer · 6-week cycle
**What followed:** Idea Lists → Themes → Impact Reports

---

## The setup

The Idea Grid was UserVoice's most-visited surface — over a million page views a year, 60% of all admin interactions. It was also running on a legacy architecture where every filter, sort, and click triggered a full page reload. Filtering took 3.5 seconds. Sorting took 2. Grid load: 3.6 seconds. Every core action was past the threshold where research says users start doubting their inputs.

"Let's modernize the grid" doesn't get resourced. I needed a sharper wedge.

---

## 01 — The problem you couldn't pitch directly

The wedge was performance. I benchmarked our core interactions against ProductBoard and anchored the gap to Nielsen Norman Group's response time thresholds — the research standard for when delays break user focus and erode trust.

| Core action | UserVoice | Productboard | Target |
|---|---|---|---|
| Grid load | 3.6s | 1.75s | 1.0s |
| Applying filters | ~3.5s | 0.10s | 0.10s |
| Sorting | 2.0s | 0.10s | 0.10s |
| Idea detail open | 2.7s | 0.30s | 1.0s |

*NNG: under 1s feels responsive. Over 3s, flow breaks. Most of our core actions were in the wrong zone.*

The argument wasn't aesthetic — it was that every action our most active admins perform daily was past the point where users start doubting their inputs. That's a retention problem. It got a six-week Big Batch cycle approved.

Engineering ran parallel — rewriting the specific filter logic causing full page refreshes in React without touching the rest of the Angular codebase. I designed the UX layer on top of a faster foundation. We couldn't rearchitect everything in six weeks, so we didn't try.

---

## 02 — How I approached it

**Lead with evidence, not instinct.** The pitch was built on benchmarks, NNG thresholds, heatmaps, and session data — not a feeling that the grid needed help.

**Use constraints as a filter.** The Angular limitation told me exactly where to focus. Target the interactions causing the most trust damage. Build on what engineering can actually ship.

**Subtract before you add.** Remove complexity that isn't earning its place before introducing anything new. Simpler surfaces are easier to extend.

**Design for what comes next.** Every component decision was evaluated against what the grid would need in future cycles — Custom Fields, inline editing, AI labels. None existed yet, but the patterns had to accommodate them.

**Test before you release broadly.** Moderated sessions before beta. Beta before full release. Nothing post-launch was a surprise.

---

## 03 — What users actually needed

I ran moderated sessions with 10 users — power users from pre-development interviews and first-time participants. Task-based: filter to a forum, manage saved views, sort and save, search, add a label.

What surfaced: admins weren't coming to the grid to look at ideas. They were coming to make decisions and clear their backlog. The job wasn't "browse feedback" — it was "process a set of ideas and move on." Slow loads, invisible filter state, bulk actions that went nowhere — all of it was getting in the way of that job.

> *"The less she has to do page loads, the better."*
> — Power User, Procore

> *"The new color scheme makes it clear to see and the slide out filter list is easy to use. I like the idea of mass selection for tasks."*
> — Product Manager, ShowingTime

---

## 04 — The design bet: a slideout for everything

The most consequential decision wasn't a visual choice — it was an interaction model.

The old grid exposed everything at once. Maximum density, no hierarchy. It didn't scale as customers added more forums, labels, and status types. I introduced a filter drawer — a slideout that exposed the full filter set in context without leaving the grid. Most-used filters stayed surfaced in a persistent top bar. Everything else was one click away.

The same model shaped bulk actions. The job wasn't "select ideas" — it was "process a batch and move on." A persistent action bar made that visible: here's what you've selected, here's what you can do. It worked for this cycle. When the action set outgrew it, the job definition pointed to what came next — a slideout that could scale.

> *"Forum and category filters worked better when they were above the ideas heading — all the filters were clearly visible. Having them hidden can cause confusion."*
> — Product Manager, SimplePractice

**Complexity should be available but never imposed.** That principle shaped every pattern in this project — and every pattern that followed.

---

## 05 — What shipped

**Flexible columns.** Reorder, resize, add, remove — saved as named views. One user's priority set isn't another's.

**Advanced filter drawer.** Full filter set exposed in context — forum, category, label, status, date, custom fields. Filter chips showed applied state at a glance. Per-column filtering for power users. Select All and Collapse added back for large taxonomies.

**Bulk actions surfaced.** Persistent action bar: select ideas, see your options, confirm before executing. First time admins could operate on a set of ideas without opening each one individually. The bottom bar was a starting point — when the action set grew, it evolved into the slideout that spread the pattern across the application.

**Strategic subtraction.** Removed the reach column data visualizations — bar charts that looked sophisticated but added confusion. Replaced with cleaner typography and intentional color. Added filter chips, quick filters, and merge match candidates surfaced directly in the grid.

**Color as wayfinding.** Darkest blue for Idea Lists, light blue for saved views, royal blue for the default grid. Not decoration — orientation. An admin switching between views needed to know instantly what they were looking at.

**Components built to extend.** Alternating rows, loading states, corrected fonts throughout. Designed knowing inline editing and Custom Fields were coming. That same extensibility later accommodated AI-generated labels surfaced directly in the grid.

---

## 06 — What the grid made possible

The grid improvements mattered on their own — sentiment improved, admins worked faster, the experience stopped being a liability in sales conversations. But I was building infrastructure.

The bulk action pattern introduced a mental model: select a set of ideas, act on them together. That thinking extended into Idea Lists — persistent, hand-picked collections separate from filter-based views. Once admins had curated collections, you could build meaning on top of them.

I wrote this into the pitch:

> *"This project won't have a significant effect on company goals on its own. We're setting the stage to introduce Idea Impact Reports, which should have significant impact on both retention and new business."*

Naming what wasn't shipping yet — and why this was a prerequisite — made it easier to align on work with modest near-term numbers. Leadership could see the sequence, not just the step.

Idea Lists shipped. Themes followed. Impact Reports came after. The slideout pattern I introduced in the filter drawer showed up in bulk actions two years later. The grid wasn't just a table. It was where the product's design language took shape.

**Grid → Idea Lists → Themes → Impact Reports.** Each step a deliberate prerequisite.

---

## 07 — What I'd tell you

**Frame the work to win cycles.** "Modernize the grid" loses. "Our core page loads 35x slower than a direct competitor, past the threshold where users doubt their inputs" wins. That's not just communication — it's how consequential design work gets resourced.

**Bets compound.** The filter drawer was one decision. Two years later the same pattern was in bulk actions, Idea Lists, and AI reporting. Build for what comes next, not just what ships this cycle.

**Constraints are information.** The Angular limitation didn't slow this project — it told me exactly where to focus. The tightest constraints often produce the clearest design decisions.

---

*[Visual slots: before grid / after grid / filter drawer / column library / bulk action slideout / themes panel]*
