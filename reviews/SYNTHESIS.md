# Review Moderator — Synthesis

Source: `gdd.txt` · Reviewers: systems-designer (SD), narrative-critic (NC), player-psychologist (PP), feasibility-lead (FL), adversarial-qa (AQA), business-analyst (BA) · Rounds 1–2 · 2026-10-19

Every point below traces to the six review files. Finding numbers refer to each reviewer's Round 1 numbering; C/X/K/A–G refer to their Round 2 labels.

---

## 1. Top 5 issues (severity × confidence)

### #1 — A full-squad wipe costs less than losing one operator, so failing on purpose beats a successful extraction. **BLOCKING**
- **Flagged by:** SD #1, PP #1, AQA #1, NC #4. BA X1 and FL B build on it in Round 2.
- **Cross-examination: STRENGTHENED.** Four reviewers found it independently in Round 1, and in Round 2 every reviewer called it the board's strongest finding. Round 2 added four enablers:
  - Friendly fire turns the wipe into a one-click reset (SD K1).
  - A deliberate wipe returns the player to "mission choices", so they can scout both sides of an exclusive branch (AQA B).
  - With no save model, quitting before the mission ends gets around any loss rule (PP #1, FL B, new FL MAJOR).
  - The exploit removes the only hook the game has against XCOM 2 (BA X1).

  One calibration: NC notes that line 380 ("A mission's conclusion resolves its rewards and losses") *might* cover failure, so this is an ambiguity between lines 312 and 380 rather than a stated rule. The diagnosis is agreed. The remedy is disputed (see Disagreement A).

### #2 — No scope boundary: what exists, what week 8 delivers, and what gets cut are never stated. **BLOCKING**
- **Flagged by:** FL #1, BA #1.
- **Cross-examination: SURVIVED INTACT, slightly STRENGTHENED.** Both reviewers held BLOCKING. BA adopted FL's point that the plan budgets tokens but never Jim's review time, which is the real throughput limit at two cycles a week. The numbers are uncontested: about 22 authored missions, 9 kits, a generator, a creator and the HQ, against about 16 iteration cycles. FL and BA disagree only on the week-8 target (see Disagreement B). In Round 2 they used this finding to argue against the additive fixes other reviewers proposed (FL Conflicts, BA C4).

### #3 — The extraction rules contradict each other: line 117 promises Downed operators are revived or explicitly left behind; line 308 abandons them silently and automatically. **BLOCKING**
- **Flagged by:** AQA #1, PP #2. NC X5 and SD K3 build on it in Round 2.
- **Cross-examination: STRENGTHENED.** PP upgraded it from MAJOR to BLOCKING after AQA showed that the document's own Example of Play promises the opposite rule (PP X1, R1). AQA narrowed the cause: line 507 already separates confirm from End Turn, so the defect is the rule in line 308, not the input scheme. NC gives a tiebreaker: line 117 states the design intent. SD notes that extraction is the mission's only pressure phase, and both its ending rules and the uncapped Suppressing Fire that can freeze reinforcements are undefined (SD K3; SD #5 upgraded to MAJOR).

### #4 — No playthrough or test harness exists, so the Level Builder, Testing and Balance agents' quality gates can't run. **BLOCKING (FL) / MAJOR (BA)**
- **Flagged by:** FL #3, BA #5. AQA #5 and SD #4 supplied dependent cases in Round 2.
- **Cross-examination: STRENGTHENED.** In Round 1 this was a sub-point in two reviews. In Round 2, FL split it out and upgraded it to BLOCKING (Connection A), and BA moved it up from MINOR to MAJOR (X3). Both note that at least five findings from three reviewers can't be checked without it: AQA #4, AQA #5, SD #4, FL #2 and FL #3. FL also notes that generated missions and seeded retries make the gap worse (FL #2, FL B, AQA A).

### #5 — Branch choices permanently lock whole kits (Medic vs Captain), splitting balance into a 16-path matrix and removing the main safety tool on one path. **MAJOR**
- **Flagged by:** SD #4, PP #4, BA #3, NC #5. FL F and AQA C build on it in Round 2.
- **Cross-examination: STRENGTHENED.**
  - NC upgraded #5 from MINOR to MAJOR (X1): the branch named after the tagline, "Bring Them Home", is the one that removes ranged Rescue if the player chooses against it.
  - SD added the "lose it twice" death spiral: the only Medic kit can be lost along with its carrier (K4).
  - AQA showed the two paths are different exploit surfaces: the Field Orders AP loop on the Captain path versus Downed gaps on the Medic path (AQA C).

  The one counterpoint: AQA B argues the lockout isn't truly blind if a deliberate wipe lets players scout both sides, but that depends on Issue #1. FL and BA both name "choice pairs vary rewards, never lock kits" as the cheapest fix.

*Just outside the top 5:* undefined save/persistence model (FL new MAJOR, PP #1); customization art cost (BA #2, FL #5, which FL upgraded to MAJOR, resolving the Round 2 severity conflict); the economy has no numbers and no farming limit (SD #2, AQA #3); objectives and NPCs have no failure rules (AQA #5); unused setting hooks (NC #1).

---

## 2. Unresolved disagreements

### A. What should a full-squad wipe cost?
- **SD:** The cost must be at least as bad as losing one operator. Downed operators are captured or lost on a wipe, or the operation closes or escalates. Fix the cost first and add any confirmation prompt after it, or the prompt shows players when to throw the mission (SD C1).
- **PP:** A wipe should cost *more than a successful extraction and less than four permanent deaths*. Losing everyone at once creates a death spiral for players who were never taught the rules. Offers capture plus a time-limited rescue mission, or the operation closes and its rewards are lost (PP C1).
- **NC:** Capture, yes. "Closes", no: Sever the Ring, Break the Bastion and Their Last Order are single-path story missions and can't close (NC C2).
- **AQA:** Any wipe penalty without a roster floor turns an exploit into a softlock. In Breakout, where the squad is one prisoner, a single failure would end the campaign. AQA #3 becomes BLOCKING once any penalty is adopted (AQA Conflicts, Revisions).
- **FL:** Use the cheapest rule. Its real cost depends on the save model, which isn't defined (FL B).

**Escalated decision:** Choose the wipe outcome (capture, loss, or forfeit of the operation or its rewards). Decide at the same time on a roster floor and a save model, and on how story-critical missions behave after a failure.

### B. Side missions: runtime generator, curated pool, or not in the slice at all?
- **FL:** Use a curated pool of pre-generated, agent-verified missions. It covers verification, economy and the farming cap together. The week-8 target is "Act 1 plus one side-mission type" (FL #1, E).
- **BA:** Leave side missions out of the slice. The generator has the most new tooling and the least effect on the pillars. If the pool is capped, the generator is overbuilt: "It cannot be both" (BA C2, C3).
- **SD:** A finite pool is fine only with a pool size worked out from the progression target plus a guaranteed-recruit floor (SD C4).
- **AQA:** A fixed pool makes the roster softlock real once it runs out, and an unlimited generator makes losses trivial. The generator choice and the roster floor and ceiling must be decided together (AQA Conflicts).

**Escalated decision:** Decide whether side missions are in the week-8 slice, and whether they come from a runtime generator or a finite curated pool. Work out the pool size against the progression and loss-recovery targets.

### C. How should the bench get used: penalties, rewards, or nothing?
- **SD:** Add a carry-over cost such as recovery time. Shared bench XP would make rotation purely cosmetic (SD #3, C2).
- **PP:** Use rewards instead (partial bench XP, side missions suited to B-team kits). With no campaign clock, injury timers just add friction and double-punish anxious players (PP C2).
- **FL:** Say plainly that rotation is optional and the bench exists to recover from losses. That's the only option that fits the schedule (FL Conflicts).

**Escalated decision:** Is roster rotation a designed pressure, and if so, is it driven by penalties or rewards? Or is it explicitly cosmetic?

### D. Should narrative gaps be fixed by adding content or by cutting systems?
- **NC:** Cutting the character creator only works if cheap narrative content replaces it: generated backgrounds, briefing and HQ lines that react to loss, and minimal named voices (a handler, a Directorate commander, one line each for rescued characters). Branch previews should show the people affected before the kit (NC C1, C4, #3 revision).
- **BA / FL:** Each addition stacks scope onto a BLOCKING plan. Subtraction is cheaper: stop the kit lockouts, and use text plus one voiced handler, with the antagonist appearing through intercepted orders (BA C4, FL Conflicts).
- **PP:** Moral framing on the branches has to come *after* the kit lockouts are softened, or it makes players resent the choices more (PP C4).

**Escalated decision:** What is the minimum authored narrative needed to carry the loss and rescue pillars within the eight-week scope?

### E. Severity of market positioning
- **BA:** MAJOR. The wipe exploit sinks the only hook against XCOM 2, and the insider-resistance premise is an unused differentiator (BA #4, X1, X2).
- **FL:** MINOR until the document says commercial release is a goal. Positioning doesn't change what can be built in eight weeks (FL Conflicts).

**Escalated decision:** State whether commercial release is a goal or whether this is coursework only (BA #4 omission, BA #5).

### F. Severity of the undefined opening prisoner
- **NC:** MAJOR. It decides who the protagonist is and has to be settled before any voiceover script (NC C3).
- **PP:** MINOR, treated as a dependency. If the prisoner is the player's avatar, it either can't die permanently, which undercuts the loss pillar, or it can, which breaks the avatar framing (PP R5).
- **AQA:** It's also a missing game-over condition (AQA E).

**Escalated decision:** Is the player an operator, the commander, or the prisoner? Can that character be permanently lost?

---

## 3. Quick wins

1. **Make line 308 require the same explicit leave-behind commitment for Downed operators as for standing ones,** matching line 117. Proposed by AQA (Conflicts with PP); PP R1 and NC X5 agree. This resolves Issue #3 without new systems.
2. **Make mission objectives indestructible engine-wide.** FL D calls this "a one-line rule" that removes a whole class of dead-end states (AQA #5, AQA A).
3. **Let choice pairs vary rewards or timing but never lock a kit,** or at minimum make any kit a branch opens always buyable once opened. Proposed by FL F, BA C4 and SD K4. It cuts the 16-path balance matrix to one target and addresses SD #4, PP #4 and part of NC #5.

---

## 4. Verdict

The board does not consider this document ready to drive production. Two clusters block it. The core loss rules contradict each other (line 117 vs line 308) and can be beaten by failing on purpose (Issues #1 and #3), which undercuts the "bring your operators home" pillar that every reviewer treated as central. And the eight-week plan has no stated inventory of existing work, no week-8 target and no cut list (Issue #2). The loss-rule cluster has the widest agreement, but its remedies are still disputed (Disagreement A), and FL and BA showed that each proposed remedy adds state, UI, save data and testing to a plan that hasn't cut anything yet. That makes the scope boundary the single change that matters most. Write the inventory, the must/should/cut list and the week-8 target first, because they decide which loss-rule fix, side-mission model and narrative minimum the project can afford.
