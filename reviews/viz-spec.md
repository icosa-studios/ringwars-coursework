# Visualization Spec: review-viz.html

Round 5 design. Source material: the six reviewer files in `reviews/` and `reviews/SYNTHESIS.md`.
`reviews/viz-data.json` was being written at the same time as this spec and didn't exist when it was designed. The field names below are the **logical fields** each visualization needs. Map them to whatever keys viz-data.json actually uses. If viz-data.json is missing a field, use the appendix tables, which I transcribed by hand from the review files. If viz-data.json and the appendix disagree, viz-data.json wins, but log the mismatch to the console (`console.warn`) so someone can check it.

---

## 0. Page frame and metadata

**Header block (full width, top of page, about 160px tall)**

| Element | Content |
|---|---|
| Title | Ring Wars Game Design Document |
| Subtitle | Multi-agent design review: 6 reviewers, Round 1 + cross-examination |
| Source link | "GDD.md @ 0ddab88". Link to `https://github.com/icosa-studios/ringwars-coursework/blob/0ddab88b645e07ed0874157bd81080bcc701a8b8/GDD.md`, opening in a new tab with `rel="noopener"` |
| Review date | 2026-10-19 |
| Verdict banner | A red-bordered box: **"Not ready to drive production."** Below it is a one-sentence summary: "Two clusters block it: the loss rules contradict each other and can be beaten by failing on purpose, and the eight-week plan has no scope boundary. Fix scope first." A "Read full verdict" toggle expands the full SYNTHESIS §4 paragraph. |

**Line-number caveat.** Reviewers cite line numbers in `gdd.txt`, and those may not match line numbers in GDD.md on GitHub. Show line references as plain text (e.g. "L308"). **Don't** generate `#L308` anchor links into the GitHub file. Put a one-line footnote under the header: "Line references (L###) refer to the text export reviewed, not GitHub line numbers."

**Layout.** Single column, max-width 1200px, centered. Sections appear in the order below. Use a sticky left mini-nav on viewports ≥1280px and a top anchor bar below that. The order follows the reader's questions: *what's the verdict → what are the top problems → what's still undecided → how did the debate change things → who argued with whom → let me look at everything*.

**Shared visual vocabulary (use it everywhere):**
- Severity colours: BLOCKING `#b91c1c`, MAJOR `#d97706`, MINOR `#6b7280`. Every colour must also have a text label or letter (B/M/m), so nothing is shown by colour alone.
- Reviewer colours (Okabe-Ito palette, colourblind-safe) and abbreviations, used in every chart:
  SD systems-designer `#0072B2`, NC narrative-critic `#CC79A7`, PP player-psychologist `#009E73`, FL feasibility-lead `#E69F00`, AQA adversarial-qa `#D55E00`, BA business-analyst `#56B4E9`.
- Finding IDs: `{REVIEWER}-{n}`. Round-1 findings that were split in Round 2 become `-a` and `-b` (e.g. `FL-3a`). A finding new in Round 2 is `FL-N1`.

**Shared filter state (one global store).** Viz 1, 4, 5 and 6 read it:
`{ reviewers: Set<abbr>, severities: Set<B|M|m>, severityBasis: "r1" | "final", status: Set<status> }`.
By default everything is selected and `severityBasis = "final"`. A "Clear filters" chip appears in a slim sticky filter bar under the header whenever any filter is active, along with the text "Showing N of 34 findings".

---

## Viz 1: Severity breakdown strip

**Insight:** how severe the board found the document, and which reviewers were harshest. This is also the main filter control.

**Type:** Six horizontal stacked bars, one per reviewer, plus a seventh "All reviewers" bar drawn thicker and set apart with a rule. Each bar is split into B / M / m segments, and each segment shows its count inside it (hide the count if the segment is narrower than 18px; it still appears in the tooltip). Above the bars is a toggle with the options **Round 1** and **Final (after cross-examination)**. Its default is Final.

**Data:** `findings[].reviewer`, `findings[].severity_r1`, `findings[].severity_final`. In the Round 1 view, use only the 30 Round-1 findings. In the Final view, use all 34 final items (split findings count separately, and FL-N1 is included).

**Interactions:**
- *Toggle Round 1 / Final.* Bars animate between the two states over 400ms. The aggregate bar changes from 5B / 20M / 5m to 7B / 24M / 3m. This shift is the headline result of cross-examination, so put a caption under the strip: "Cross-examination raised 2 findings to BLOCKING, upgraded 6 overall, and withdrew none." The numbers in the caption come from the data.
- *Hover a segment.* A tooltip lists the finding IDs and short titles in that segment.
- *Click a segment.* Sets the global filter to that reviewer + severity, using the currently toggled basis. Shift-click adds the segment to the current filter. Clicking a reviewer label filters to that reviewer only. Active segments get a 2px dark outline, and inactive ones fade to 35% opacity.

**Size/position:** Full width, about 260px tall, directly under the header.

---

## Viz 2: Top 5 issues drill-down

**Insight:** what to fix, how sure the board is, and the full trail behind each issue. This is the main payload of the page.

**Type:** Five expandable cards stacked vertically, numbered #1–#5 in synthesis order.

**Collapsed card (about 96px):**
- Rank badge, a one-line title (the synthesis heading), and a severity pill. Issue #4 shows a **split pill**, "BLOCKING (FL) / MAJOR (BA)", with half of it in each colour.
- **Reviewer chips** in two groups: "Flagged in R1" (filled chips) and "Built on in R2" (outlined chips). Example for #1: filled SD, PP, AQA, NC and outlined BA, FL.
- **Cross-exam outcome badge:** STRENGTHENED (green-teal), SURVIVED INTACT (grey-blue), WEAKENED, or WITHDRAWN. Use a neutral palette, not severity colours. In this review all five are STRENGTHENED, except #2, which is "SURVIVED INTACT, slightly strengthened". Show the badge text exactly as given.
- If an escalated disagreement attaches to the issue, a link chip reads "Remedy disputed → Disagreement A". Issue #1 links to A and #2 links to B.

**Expanded card (click anywhere on the header, or press Enter/Space when focused; several cards can be open at once):** three vertical sections, laid out as a timeline with a thin left rail.
1. **Round 1: original findings.** One row per contributing R1 finding: reviewer chip, ID, R1 severity pill, short title, and the cited source lines as plain text. Each row has a "show text" disclosure that reveals the reviewer's Problem paragraph.
2. **Round 2: cross-examination.** One row per R2 item that touches the issue, labelled with the reviewer's own label (e.g. "SD K1", "PP C1", "AQA B"). Each row has a type tag, **Connection** (blue) or **Conflict** (red), and one or two summary sentences. For #1, the four enablers from the synthesis (friendly fire, scouting both branches, save model, loss of the XCOM hook) appear as connection rows, and NC's line-380 calibration appears as a "Calibration" row (grey tag).
3. **Final status.** Shows the final severity per reviewer where reviewers differ (#4: FL BLOCKING, BA MAJOR), any severity changes as "PP-2: MAJOR → BLOCKING" with an up-arrow, and any matching **Quick win** from SYNTHESIS §3 in a green callout: issue #3 gets quick win 1, issue #5 gets quick win 3. Issue #4 has no quick win. Don't invent one.

**Data:** `top_issues[]` with `rank, title, severity (or per-reviewer severities), flagged_by[], built_on_by[], cross_exam_outcome, outcome_note, disagreement_ref, quick_win_ref, r1_findings[] (ids → findings[]), r2_items[] {reviewer, label, type: connection|conflict|calibration, summary, targets[]}`. The R1 rows come from `findings[]` by ID.

**Global filter interaction:** Cards are **never hidden** by filters, because they are the synthesis and must stay visible. When a reviewer filter is active, rows inside expanded cards from non-matching reviewers fade to 35% opacity, and the collapsed card shows "N of M rows match filter".

**Below the cards:** a muted line titled "Just outside the top 5", listing the five near-misses from synthesis §1 as chips. Each chip links to its row in Viz 6.

**Size/position:** Full width, right after Viz 1. About 520px when all cards are collapsed. Expanded cards grow to fit their content, with no internal scroll.

---

## Viz 3: Consensus and clash matrix

**Insight:** where the board agrees (the diagnosis) and where it splits (the remedy). The point it makes is that reviewers agree on what is wrong and disagree on how to fix it.

**Type:** A heatmap-style grid. Columns are the 6 reviewers (SD, NC, PP, FL, AQA, BA, coloured headers). Rows come in two labelled bands:
- **Band 1, "Consensus: top issues" (5 rows, #1–#5).** Cell encoding:
  - *Flagged in R1*: filled cell in the colour of that reviewer's R1 severity, with the letter (B/M/m) and the finding ID in small text.
  - *Built on in R2*: diagonal-hatched cell in the colour of the reviewer's stated severity, or neutral grey if they didn't state one, with the R2 label (e.g. "K1").
  - *Silent*: empty cell with a light border.
  - If the cell's severity changed in R2, show a small ↑ or ↓ glyph in the corner.
- **Band 2, "Escalated decisions: unresolved" (6 rows, A–F).** Cells hold a **short position label** of no more than 4 words, on a background coloured by position cluster *within that row* (positions that agree share a colour, using a separate neutral-pastel palette, not severity colours). Reviewers who took no position are empty. Position labels from the synthesis:
  - A Wipe cost: SD "≥ one operator lost" · PP "capture + rescue mission" · NC "capture, never close" · AQA "only with roster floor" · FL "cheapest rule; save model first"
  - B Side missions: FL "curated pool in slice" · BA "out of slice" · SD "pool OK if sized" · AQA "decide with roster floor"
  - C Bench: SD "penalties (recovery time)" · PP "rewards (bench XP)" · FL "declare optional"
  - D Narrative gaps: NC "add cheap content" · BA "subtract (stop lockouts)" · FL "subtract (stop lockouts)" · PP "framing after mechanics fix"
  - E Market severity: BA "MAJOR" · FL "MINOR until goal stated"
  - F Opening prisoner: NC "MAJOR" · PP "MINOR (dependency)" · AQA "missing game-over rule"
  On each Band 2 row, a right-hand column shows a red **"DECISION NEEDED"** tag with the number of distinct position clusters ("3 positions").

**Data:** `top_issues[].flagged_by / built_on_by` (Band 1). `disagreements[] {id, title, positions[] {reviewer, label, summary, cluster}, escalated_decision}` (Band 2). If viz-data.json has no `cluster` field, use Appendix C.

**Interactions:**
- *Hover a cell.* A tooltip shows the full position or finding summary (1–3 sentences) and the citation labels (e.g. "PP C1").
- *Click a Band 1 row label.* Scrolls to and expands the matching card in Viz 2.
- *Click a Band 2 row label.* Expands an inline panel under the row. It shows each reviewer's position as a short paragraph and then the **Escalated decision** text in a bordered box. Only one Band 2 panel is open at a time.
- *Hover a column header.* Highlights that reviewer's column and dims the rest.
- *Global reviewer filter.* Columns for unselected reviewers collapse to 12px-wide stubs that still show colour but not text. The row structure stays.

**Size/position:** Full width, about 560px tall (11 rows × about 44px + headers + band labels). It sits after Viz 2.

---

## Viz 4: Finding flow (Round 1 → Final severity)

**Insight:** what cross-examination did to each finding. Which findings were upgraded, held, narrowed, or split, and which appeared new. It also shows that **no finding was withdrawn**, which is itself worth showing.

**Type:** A two-column **slope chart**, chosen over a Sankey. With only 3 severity levels, a Sankey would collapse into three fat ribbons and hide *which* findings moved. Lines per finding keep them individually traceable.
- The left axis is "Round 1" and the right axis is "Final". Each axis has three vertical bands, BLOCKING at the top, then MAJOR, then MINOR. The bands are sized to their maximum count across both sides, so the lines don't overlap.
- Each finding is a dot on each side, joined by a line. Inside a band, dots are ordered by reviewer (SD, NC, PP, FL, AQA, BA) and then by number, so the same reviewer's findings line up.
- Lines are coloured by reviewer. Horizontal (HELD) lines are drawn thin at 40% opacity. Lines that change severity are drawn 2.5px at full opacity with an arrowhead on the right.
- A **split** finding has one left dot that forks into two right dots (FL-3 → FL-3a, FL-3b; FL-5 → FL-5a, FL-5b; BA-5 → BA-5a, BA-5b).
- **New** findings (FL-N1) start from a small "New in R2" marker to the left of the Final axis, with no Round 1 dot.
- On the far right is a **"Withdrawn"** lane, which is empty in this data. Label it "0 withdrawn" in muted text. Don't hide it, because an empty lane is information.
- A status glyph sits beside each right-side dot: ▲ upgraded, ● held, ◐ narrowed, ⊕ widened, ⑂ split, ★ new, plus a small "conditional" ⚑ on AQA-3 ("→ BLOCKING if any wipe penalty is adopted").

**Data:** `findings[] {id, reviewer, title, severity_r1 (null if new), severity_final, status, status_note, parent_id (for splits), conditional_note}`.

**Interactions:**
- *Hover a line or dot.* Highlights the line, fades all others to 10%, and shows a tooltip with ID, title, "R1 MAJOR → Final BLOCKING", the status, and the reviewer's own revision sentence (`status_note`).
- *Click a line.* Pins the highlight and scrolls Viz 6 to that row, flashing it. Click again or press Esc to unpin.
- *Legend buttons* above the chart: "Show only changed" hides the HELD lines, and "Show all" restores them.
- *Global filters.* Lines that don't match the filter fade to 10% but stay in place, so the layout doesn't jump. When `severityBasis` is "r1" the severity filter applies to the left dot, and when it is "final" it applies to the right dot.

**Size/position:** Full width, about 520px tall. It sits after Viz 3. A one-line caption is generated from the data: "6 upgraded · 3 split · 1 new · 0 withdrawn".

---

## Viz 5: Cross-examination network

**Insight:** this is what the multi-agent setup produced: who read whom, and whether they pushed back or built on each other. It shows that adversarial QA was the most-cited reviewer, that the feasibility lead wrote the most connections, and that the densest adversarial pairs were SD↔PP and SD↔AQA.

**Type:** A node-link diagram with a **fixed hexagonal layout** (not force-directed, so it stays stable and readable).
- Six nodes on a hexagon, ordered SD, NC, PP, FL, AQA, BA clockwise from the top. Each node is a reviewer-coloured circle with its abbreviation and full name underneath. Node radius scales with the total number of Round 2 items the reviewer wrote (range 28–44px).
- Edges are directed from the reviewer who wrote the R2 item to the reviewer whose finding it cites. Each directed pair can have two separate curved edges:
  - **Conflict** edge: red `#b91c1c`, dashed.
  - **Connection** edge: blue `#1d4ed8`, solid.
  - Stroke width = 1.5px + 1.5px × item count. Offset the curvature so A→B and B→A, and conflict versus connection, don't overlap.
- Beside the diagram is a legend and a small "busiest pairs" list: the top 3 pairs by total edge count, worked out from the data.

**Data:** `cross_exam_edges[] {from, to, type: conflict|connection, label (e.g. "SD C1"), summary, finding_refs[]}`. If the source item cites several reviewers, it produces one edge entry per cited reviewer. If viz-data.json doesn't supply edges, use Appendix B.

**Interactions:**
- *Hover a node.* Highlights all of that node's edges in and out, fades the rest, and shows a tooltip such as "Wrote N R2 items (x conflicts, y connections) · Cited by others M times". All counts are computed from the data.
- *Click a node.* Pins the highlight and sets the global reviewer filter to that reviewer.
- *Hover an edge.* Shows a tooltip with the direction and type ("SD → PP · 2 conflicts") and, for each item, its label and a one-line summary.
- *Click an edge.* Opens a side drawer (360px, right side) listing the items in full, each with a "jump to finding" link into Viz 6.
- *Toggles* above the chart, "Conflicts" and "Connections", show or hide each edge type. Both start on.
- *Global filters.* When a reviewer filter is active, edges that don't touch a selected reviewer fade to 10%.

**Size/position:** About 640×520px for the diagram plus a 280px legend/list column. It sits after Viz 4. Below 900px viewport width, the list moves under the diagram.

---

## Viz 6: Findings explorer (filterable, sortable table)

**Insight:** the complete record. Every finding is reachable, and every other visualization links into this one.

**Type:** A table with one row per final item (34 rows: 30 Round-1 findings, with 3 of them split, plus 1 new).

**Columns:** ID · Reviewer (chip) · Title · R1 sev · Final sev · Change (▲/▼/●/⑂/★ with text) · Status · Top-issue link (e.g. "#1", empty if none) · Cited by (count of R2 edges pointing at this finding) · Source lines (plain text).

**Row expansion:** Clicking a row expands it in place to show the Round 1 *Problem* text, the *Needed / Fix* text if present, the reviewer's own Round 2 revision note, and a list of the R2 items from *other* reviewers that cite this finding, each tagged Conflict or Connection.

**Controls (above the table, wired into the global filter store):**
- Reviewer multiselect chips (6).
- Severity chips (B/M/m) with a "by: Round 1 | Final" switch, which is the same `severityBasis` used by Viz 1.
- Status multiselect: upgraded, held, narrowed, widened, split, new.
- Text search over title and problem text, debounced by 150ms.
- Checkbox: "Only findings in a Top-5 issue".

**Sorting:** Click a column header to cycle asc → desc → default. The default sort is Final severity (B > M > m), then Cited-by descending, then ID. Severity sorts by rank, not alphabetically.

**Data:** `findings[]` (all fields above, plus `problem_text, needed_text, source_lines, top_issue_rank`), and `cross_exam_edges[]` for the "Cited by" column and the expanded list.

**Size/position:** Full width, at the bottom of the page before the quick wins. Use a sticky table header, and don't paginate (34 rows). The table can scroll horizontally on viewports narrower than 900px. Hide the Source lines and Cited by columns there.

---

## After the visualizations (static text, not a viz)

**Quick wins:** the three items from SYNTHESIS §3 as a numbered list, each with the proposing reviewers as chips and a link to the top issue it resolves (#3, none, #5). They stay as text because they are already short and a chart would add nothing.

---

## Considered and cut

- **Sankey of severity flow.** Cut in favour of the Viz 4 slope chart. With 3 levels, a Sankey hides which findings moved.
- **Reviewer × reviewer agreement heatmap.** Cut because it overlapped with Viz 5. The network already shows reviewer-to-reviewer engagement, and Viz 3 shows agreement *by topic*, which is the more useful question.
- **Word cloud or theme bubbles.** Decorative.
- **Line-reference density over the GDD.** Tempting, but the line numbers are from `gdd.txt` and may not map onto the linked GDD.md, so it would mislead.

---

## Accessibility and behaviour requirements

- Every chart has a visually hidden `<table>` alternative or an `aria-describedby` summary built from the same data.
- All interactive elements can be reached with the keyboard (Tab/Enter/Space/Esc). Focus rings stay visible.
- Severity and edge type never rely on colour alone, since they also use letters, dash patterns, and glyphs.
- Respect `prefers-reduced-motion` by turning off the bar and slope transitions.
- The page must work from `file://` with no build step. Load viz-data.json with fetch, and fall back to an inline `<script type="application/json">` copy if fetch fails, because file:// blocks it in Chrome.

---

## Appendix A: Expected findings (sanity check for viz-data.json)

Severity: B = BLOCKING, M = MAJOR, m = MINOR.

| ID | Short title | R1 | Final | Status | Top issue |
|---|---|---|---|---|---|
| SD-1 | Wipe costs less than losing one operator | B | B | widened | #1 |
| SD-2 | Economy has no numbers / no farming cap | M | M | widened (absorbs AQA-4 AP loop; pool-size condition) | - |
| SD-3 | Nothing carries over; bench has no job | M | M | held (reframed: loss/rotation near-zero cost) | - |
| SD-4 | Branch choices lock whole kits | M | M | widened (lose-it-twice spiral) | #5 |
| SD-5 | No approach pressure; reinforcements undefined | m | M | upgraded (partial withdrawal: credits-per-kill ruled out) | #3 (context) |
| NC-1 | Ring / insider / fantasy hooks unused | M | M | held (priority raised) | - |
| NC-2 | Player identity contradicts itself | M | M | held | - |
| NC-3 | No authored characters; faceless antagonist | M | M | held (scope-aware fix) | - |
| NC-4 | Loss unacknowledged; wipe inverts stakes | M | M | narrowed | #1 |
| NC-5 | Exclusive choices hide moral stakes | m | M | upgraded | #5 |
| PP-1 | Wipe cheaper than loss → throw missions | B | B | held (remedy refined) | #1 |
| PP-2 | Downed abandoned without confirmation | M | B | upgraded | #3 |
| PP-3 | Mission 2 overload; rules never taught | M | M | widened (priority raised; absorbs friendly-fire-on-Downed) | - |
| PP-4 | Blind, permanent kit lockouts | M | M | widened | #5 |
| PP-5 | Attachment starts late; prisoner undefined | m | m | narrowed (bench-XP handed to SD-3) | - |
| FL-1 | No scope boundary / week-8 target / cut list | B | B | held | #2 |
| FL-2 | Generated side missions unverifiable | M | M | held (cut withdrawn → curated pool) | - |
| FL-3a | No playthrough/test harness | M | B | split + upgraded | #4 |
| FL-3b | Level Builder token budget | M | M | split | - |
| FL-4 | Combat coupling; no gameplay-AI design | M | M | held | - |
| FL-5a | Customization art cost | m | M | split + upgraded | - |
| FL-5b | Action cameras / macOS | m | m | split | - |
| FL-N1 | Save/persistence model unspecified | - | M | new | #1 (enabler) |
| AQA-1 | Extraction/Downed/failure rules contradict | B | B | held (misclick sub-point narrowed; adds branch scouting) | #1, #3 |
| AQA-2 | Downed state rules missing | M | M | held | - |
| AQA-3 | Roster softlock, no recovery rule | M | M | held, conditional → B if wipe penalty adopted | - |
| AQA-4 | AP loop / Suppressing Fire board lock | M | M | narrowed (AP loop Captain-path only; grenade-pin sub-point → MINOR) | - |
| AQA-5 | Objectives/NPCs have no failure rules | M | M | widened (generated missions) | - |
| BA-1 | No scope boundary | B | B | widened (adopts Jim-review-time point) | #2 |
| BA-2 | Character creator vs art constraint | M | M | held | - |
| BA-3 | Branching + generator cost | M | M | held (reframed: 16-path matrix) | #5 |
| BA-4 | No market positioning | M | M | held (recommendation changed) | - |
| BA-5a | Two documents for two audiences | m | m | split | - |
| BA-5b | Test harness missing | m | M | split + upgraded | #4 |

Expected totals: **Round 1**: 30 findings, 5 B / 20 M / 5 m. **Final**: 34 items, 7 B / 24 M / 3 m. Per reviewer (Final): SD 1/4/0 · NC 0/5/0 · PP 2/2/1 · FL 2/5/1 · AQA 1/4/0 · BA 1/4/1.
Upgrades to a higher severity: SD-5, NC-5, PP-2, FL-3a, FL-5a, BA-5b (6). Withdrawn: 0.

## Appendix B: Cross-examination edges (Round 2, from → to)

Item labels are the reviewers' own, transcribed from each file's Round 2 section. An item that cites several reviewers counts once for each of them.

| From → To | Conflict items | Connection items |
|---|---|---|
| SD → PP | C1, C2 | K4 |
| SD → AQA | C3, C4 | K1, K3, K4 |
| SD → FL | C4 | K3, K5 |
| SD → BA | C4 | K5 |
| SD → NC | - | K2 |
| NC → SD | C2 | X1 |
| NC → PP | C3, C4 | X1, X5 |
| NC → BA | C1 | X3, X4 |
| NC → FL | C1 | - |
| NC → AQA | - | X2, X5 |
| PP → SD | C1, C2 | X5 |
| PP → NC | C4 | - |
| PP → FL | C3 | X3, X4 |
| PP → BA | - (C3 endorses BA) | X4, X6 |
| PP → AQA | - | X1, X2, X5 |
| FL → SD | Conflicts¶1 | A, B, E, F |
| FL → AQA | Conflicts¶1 | A, B, C, D, E, G |
| FL → NC | Conflicts¶2 | - |
| FL → BA | Conflicts¶3 | A, E, F |
| FL → PP | - | B, F |
| AQA → SD | Conflict (SD #1 remedy), Conflict (SD #5 severity) | B, C, D |
| AQA → PP | Conflict (PP #2 cause) | B, C |
| AQA → FL | Conflict (FL #2 vs BA #3) | A |
| AQA → BA | Conflict (FL #2 vs BA #3) | A |
| AQA → NC | - | B, E, F |
| BA → FL | C1, C2 | X3 |
| BA → SD | C3 | X1, X3 |
| BA → AQA | C3 | X1, X3 |
| BA → NC | C4 | X2 |
| BA → PP | C4 | X1, X4 |

Derived checks:
- Densest conflict pairs, counting both directions: SD↔PP (4) and SD↔AQA (4), then NC↔PP (3) and FL↔BA (3).
- Most-cited reviewer: AQA (about 20 incoming items). Next is SD (about 18).
- Most connection items written: FL (15).

## Appendix C: Disagreement position clusters (for Viz 3 Band 2 colouring)

- **A:** {SD} cost ≥ one operator · {PP, NC} capture-based · {AQA} gate on roster floor · {FL} cheapest rule / save model first → 4 clusters
- **B:** {FL, SD} finite pool (SD conditional) · {BA} out of slice · {AQA} decide jointly with roster floor → 3 clusters
- **C:** {SD} penalties · {PP} rewards · {FL} declare optional → 3 clusters
- **D:** {NC} add content · {BA, FL} subtract · {PP} sequencing condition → 3 clusters
- **E:** {BA} MAJOR · {FL} MINOR → 2 clusters
- **F:** {NC} MAJOR · {PP} MINOR/dependency · {AQA} missing game-over → 3 clusters
