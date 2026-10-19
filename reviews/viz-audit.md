# Visualization Audit: review-viz.html (Round 5)

Audited `review-viz.html` against `reviews/viz-data.json`, `reviews/viz-spec.md`, the six reviewer files and `reviews/SYNTHESIS.md`. Interactivity (filters, search, finding trails, keyboard) was already confirmed in a browser by the user, so this audit only re-checks interactions where they affect what a reader understands.

## 0. Baseline checks (pass)

- **Metadata.** Title "Ring Wars Game Design Document", source link `https://github.com/icosa-studios/ringwars-coursework/blob/0ddab88b645e07ed0874157bd81080bcc701a8b8/GDD.md` (text "GDD.md @ 0ddab88", new tab, `rel="noopener"`), review date 2026-10-19 (read from JSON). All correct. The line-reference footnote is present, and no `#L###` anchors are generated.
- **Embedded data.** The inline `DATA` block matches `viz-data.json` in every section (findings, new finding, conflicts, connections, revisions, top issues, near misses, disagreements, positions, quick wins, verdict, aggregate counts).
- **Round 1 severities and reviewer attribution.** All 30 findings carry the correct reviewer, number, title and Round 1 severity, checked against each reviewer file. Round 1 totals are 5 B / 20 M / 5 m.
- **Final severities.** All 30 match the reviewers' Revisions sections: SD-5, NC-5, PP-2, FL-3 (harness part), FL-5 (customization part) and BA-5 (harness part) are upgraded, and nothing is downgraded at finding level.
- **Top 5 cards.** Titles, rank order, severity (including the #4 split pill "BLOCKING (FL) / MAJOR (BA)"), outcome badges (#2 reads "SURVIVED INTACT, slightly STRENGTHENED", the other four read STRENGTHENED), disagreement links (#1 to A, #2 to B) and quick-win attachments (#3 gets QW1, #5 gets QW3, #4 gets none) all match SYNTHESIS.md.
- **Disagreements A–F.** Every position text and citation matches SYNTHESIS §2, and each escalated decision is reproduced verbatim in substance.
- **Cross-exam counts.** 23 conflict items and 33 connection items. Per-reviewer counts (SD 4/5, NC 4/5, PP 4/6, FL 3/7, AQA 4/6, BA 4/4) match the source files. The derived "most cited" figure (AQA 19, then SD 18) and "most connections written" (FL, 7) reproduce from the JSON.
- **Quick wins and verdict.** Proposers and endorsers match SYNTHESIS §3. The full verdict text matches SYNTHESIS §4.

### Counting scheme (the known risk)

The page uses **neither** Phase 1 scheme on its own. It shows a third total: **31 items = 30 Round 1 findings at final severity (7 B / 22 M / 1 m, the JSON scheme) + FL-NEW1 (MAJOR), giving 7 B / 23 M / 1 m.** Split findings count once, at their highest part.

- **Reproducible from the JSON?** Yes. `findings[]` (30) plus `round2_new_findings[]` (1) gives exactly the numbers on the bars, the Viz 4 band labels ("5 → 7", "20 → 23", "5 → 1"), the table count and the filter bar ("of 31 items").
- **Labelled clearly?** Mostly yes. The header count note, the Viz 1 sub-caption, the Viz 4 axis ("30 findings" / "31 items"), the table count line and the "About the counts" paragraph all explain the scheme. The About paragraph also names the spec's 34-item / 7-24-3 alternative.
- **Remaining problems** are covered below: accuracy error 3 (the split count is inconsistent across the page) and usability issues U3 and U4.

---

## 1. Accuracy errors

**A1. Issue #4 credits AQA and SD with Round 2 work they didn't do.**
- **HTML:** Card #4 shows "Built on in R2: AQA, SD" as outlined chips. Viz 3, Band 1, row #4 draws hatched "built on in R2" cells for AQA and SD, each labelled just "R2".
- **Source:** Neither `adversarial-qa.md` nor `systems-designer.md` has a Round 2 item about the test harness. SYNTHESIS #4 says "AQA #5 and SD #4 supplied dependent cases". Those are their *Round 1* findings, which FL Connection A and BA X3 cited. The page's own tooltip admits it: "no AQA/SD Round 2 item in viz-data.json cites its source findings directly."
- **Origin:** Inherited from `synthesis_top_issues[3].built_on_in_round2_by` in the JSON. It appears on the main payload of the page.
- **Fix:** Show the two as "R1 findings cited as dependent cases (AQA-F5, SD-F4)", using a different cell style or an empty cell with a note. Don't present them as R2 authors.

**A2. "Held" status contradicts the reviewers' own "widened" revisions.**

The page sets status from `change_type` alone. Several findings are therefore labelled **held** even though their authors widened them, and in some cases the revision note shown in the same tooltip or row says so.

| Finding | HTML status | Source revision |
|---|---|---|
| SD-F1 | held | "stays BLOCKING, **with a wider scope**" (K1, C1, L310) |
| SD-F2 | held | "absorbing QA F4's AP loop", adds pool-size condition |
| SD-F4 | held | "adding the lose-it-twice death spiral (K4)" |
| PP-F3 | held | R3 "adding X2 … as its most severe instance" |
| PP-F4 | held | R4 "stays MAJOR, **with broader scope**" |
| AQA-F1 | narrowed only | narrowed misclick sub-point **and** "adding Connection B" |

- **Effect:** The Status filter returns 2 "widened" findings, when the sources support about 7. The Viz 4 caption ("2 widened · 18 held") is wrong for the same reason.
- **Agreement with spec:** Appendix A in the spec agrees with the sources for SD-1, SD-2, SD-4, PP-3 and PP-4.
- **Fix:** Add a status override from the revision text, or apply the spec's Appendix A statuses, which the page already embeds as `APPX.status` but uses only for `console.warn`.

**A3. The page names a different set of split findings in different places.**
- **HTML:** The header count note says "Findings split in Round 2 (PP-F5, FL-F3, FL-F5, BA-F5) count once, at their highest part." The Viz 4 caption says "4 split".
- **JSON and spec:** The "About the counts" paragraph quotes the JSON's `post_round2_severity_note`, which names **three** (FL-F3, FL-F5, BA-F5). The spec also lists three.
- **Source:** PP does write "#5 split" (R5). But the handed-off half went to SD-F3, so PP-F5 has no second part that could be "counted at its highest part". The note's wording doesn't fit it.
- **Fix:** Pick one rule. Either list PP-F5 separately ("narrowed / point handed to SD-F3"), or say "4 split, of which 3 keep two parts".

**A4 (minor). AQA-F4's sub-point downgrade and SD-F5's partial withdrawal are missing from the summary captions.**
- **HTML:** The Viz 1 caption reads "downgraded 0, and withdrew none."
- **Source and JSON:** At finding level that is correct, but AQA R2 downgraded the grenade-pin sub-point to MINOR, and SD R2 records a "partial withdrawal" on F5. The JSON records both: `sub_point_downgrades: 1`, `partial_withdrawals: 2`.
- **Fix:** Add a short clause such as "(1 sub-point downgraded, 2 partial withdrawals)" so the caption doesn't overstate how one-directional the debate was.

No numbers on the page are invented. No findings are missing or duplicated. All other severity labels, reviewer attributions, cross-exam outcomes and disagreement positions match the sources.

---

## 2. Usability issues

**U1. Viz 5 node sizes exaggerate small differences. SHOULD-FIX.**
- **Problem:** Radius is scaled min-to-max over 8–10 items written, mapping to 28–44 px. BA (8 items) gets a circle about 2.5× smaller in area than PP, FL and AQA (10 items). That reads as "BA barely took part", which is false: BA engaged all five colleagues.
- **Fix:** Scale area from zero, or use a narrower range.

**U2. Top-5 cards contradict themselves on "Built on in R2". SHOULD-FIX.**
- **Problem:** The card header comes from the synthesis (for example, #2 says "Built on in R2: none"). The expanded "Round 2: cross-examination" list instead includes **every** R2 item that cites any source finding. For #2 that is SD K5, PP X4, FL F, FL G, BA X4 and BA C2, so a card that says "none" then lists six items. #1 similarly pulls in loosely related items (SD K2, PP X6, and others).
- **Fix:** Label the list "R2 items that cite these findings" and visually separate the synthesis-named items from the incidental ones. Or filter to the synthesis-named ones.

**U3. The MINOR remainders of split findings disappear from the charts. SHOULD-FIX.**
- **Problem:** Viz 1 Final and Viz 4 show MINOR falling 5 → 1. The board actually still holds MINOR items for FL-5 (cameras and macOS), BA-5 (two-documents framing) and the AQA-4 grenade-pin sub-point. A first-time reader will read "1 MINOR left" literally. The rule is stated in small muted captions, but the chart itself gives no cue.
- **Fix:** Add a small "+2 split remainders" marker in the Final MINOR band and segment.

**U4. The Viz 4 caption's status counts don't add up to the item count. NICE-TO-FIX.**
- **Problem:** The caption reads "6 upgraded · 3 narrowed · 2 widened · 4 split · 1 new · 0 withdrawn · 18 held". These sum to 34 for 31 items, because statuses overlap (FL-F3, FL-F5 and BA-F5 are both upgraded and split). By coincidence, 34 is the spec's competing total, which invites confusion.
- **Fix:** Add "(statuses overlap)", or report split as a sub-tag of upgraded.

**U5. Clicking a Viz 4 line scrolls the reader away from the chart they were using. SHOULD-FIX.**
- **Problem:** The lede says "click to pin it and jump to its row". Pinning is meant for studying a line, but the jump immediately scrolls to the table, so the pin is never seen. When filters are active and the row is hidden, `jumpToFinding` also silently clears every filter (`if (!keepFilters || true)`).
- **Fix:** Pin on click and add a separate "open in table" link in the tooltip. Remove the `|| true` so filters are kept.

**U6. Viz 3 Band 2 position labels truncate at typical laptop widths. NICE-TO-FIX.**
- **Problem:** Cell text is wrapped to `charsPerLine - 4`. At the 1200 px max it fits about 15 characters per line, so "cheapest rule; save model first" becomes "cheapest rule; save model…". Around 1000 px it is about 9 characters ("capture +" / "rescue…"). Tooltips hold the full text, but the band's whole purpose is reading positions side by side.
- **Fix:** Drop the −4 margin (the P-tag only needs about 20 px on line 1), or allow 3 lines.

**U7. Position shades in Viz 3 Band 2 are nearly indistinguishable in dark mode. NICE-TO-FIX.**
- **Problem:** `--p1` #2B3039 and `--p2` #3B414D are very close on the dark background. The P1–P4 text tags carry the meaning, so nothing relies on colour alone, but the "same shade = same position" cue in the lede doesn't work visually.

**U8. B / M / m depends on letter case. NICE-TO-FIX.**
- **Problem:** "M 4 · m 0" in the bar totals and table pills is easy to misread, especially in monospace at 12 px. The spec mandated this convention, but "Mn" or "MIN" would remove the ambiguity.

**U9. Viz 3 Band 1 legend swatch is always red. NICE-TO-FIX.**
- **Problem:** "Flagged R1, letter = R1 severity" uses a BLOCKING-red swatch, but flagged cells can be orange or grey. Use a three-colour swatch or a neutral one.

**U10. Viz 3 column headers are focusable but do nothing. NICE-TO-FIX.**
- **Problem:** The headers take a Tab stop. Focusing one dims the other columns, but Enter does nothing and there is no role. Either give them a filter action (consistent with Viz 1 labels and Viz 5 nodes) or remove the tabindex.

**U11. Information that disappears into "held". NICE-TO-FIX.**
- **Problem:** SD-F3 and BA-F3 were "reframed", and FL-F2's recommendation was withdrawn and replaced. All three show only as "held". The notes contain this, but a "reframed" or "remedy changed" tag would make Viz 4 and the table more honest about what the debate did.

**U12. Naming drift from the spec. NICE-TO-FIX.**
- **Problem:** The new finding is "FL-NEW1" on the page and in the JSON, but "FL-N1" in the spec and the brief. Pick one.

There are no MUST-FIX usability issues. The page reads well for a first-time visitor:
- The verdict banner leads, and the section order follows the reader's questions.
- Every chart has a lede saying what to click.
- Severity is never shown by colour alone.
- The count scheme is explained in several places.

---

## 3. Verdict

**Needs one short targeted pass, not a redesign.** The data plumbing is sound: every count reproduces from the JSON, the embedded data matches the file, and the metadata is correct. The problems before showing it:

- **A1** misattributes Round 2 work on a top-5 card. Treat this as must-fix: it is a wrong claim in the page's main payload.
- **A2** gives status labels that contradict the revision notes shown beside them. Must-fix: the fix is small, because the correct statuses are already embedded in `APPX.status`.
- **A3** reports an inconsistent split count.
- **U1, U2, U3 and U5** are should-fix items that change what a reader takes away.

A1 and A2 come from the JSON, so they should also be corrected in `viz-data.json`.
