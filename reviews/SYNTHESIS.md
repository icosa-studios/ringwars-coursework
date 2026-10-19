# Review Board Synthesis — Ring Wars GDD

Moderator synthesis of six reviews (systems-designer, narrative-critic, player-psychologist, feasibility-lead, adversarial-qa, business-analyst) across Round 1 and Round 2. Every point below traces to those files; the moderator adds no critiques of its own.

---

## 1. Top 5 issues (ranked by severity × confidence)

### #1 — On story missions, wiping is better than a costly extraction, and no save/quit rule closes the gap — BLOCKING
A full-squad wipe on a story mission rewinds to before the attempt at no cost. A successful extraction permanently loses every operator left outside the zone, including Downed ones. So the best play is to let the last operator go down.
- **Flagged by:** systems-designer (#1), adversarial-qa (#2). In Round 2 it was taken up by player-psychologist (merges their #2 into it), narrative-critic (new MAJOR: "You will lose good people" is mechanically optional on story missions) and business-analyst (C1).
- **Cross-examination:** **STRENGTHENED.** Adversarial-qa showed the wipe can be forced whenever the player wants, by hitting their own squad with an area attack (X1). They also showed the rules never say which wins if the last operator is Downed while entering the zone (X2). Systems-designer widened the finding to the missing save/quit rule, which lets players dodge losses on side missions too (X2). One part weakened: adversarial-qa's expected-loss math (C1) reduced the *side-mission* version to a MINOR edge case, and systems-designer withdrew the claim that side missions push players to keep a doomed squad fighting.

### #2 — Losses can leave the roster below 4 with no way to recover, softlocking the campaign — BLOCKING
Operators are lost at extraction, captured or killed in side-mission wipes, and rescue only "may" be offered. Recruits arrive only at story milestones. The story-mission retry returns to a roster that is already depleted.
- **Flagged by:** adversarial-qa (#1), systems-designer (#2), player-psychologist (#1). In Round 2, feasibility-lead (C1) and business-analyst (X1) engaged with it.
- **Cross-examination:** **STRENGTHENED.** Systems-designer and player-psychologist both upgraded from MAJOR to BLOCKING after seeing that the others had reached the same softlock independently. Adversarial-qa (X3) and systems-designer (C1) showed that cutting side missions would take away the only recovery path the document names. All three proposals for a fix include a guaranteed roster floor (feasibility-lead C1, adversarial-qa C2, business-analyst X1).

### #3 — The eight-week plan can't pay for the campaign it promises, and nobody is assigned to build the gameplay systems — BLOCKING
The plan funds 16 mission cycles, and rework comes out of the same cycles. The campaign needs roughly 18–22 authored missions, plus side missions, HQ and cinematics. No agent, budget line or status table covers the gameplay code: cover, control cones, AI, the generator, the character creator, persistence and cinematics.
- **Flagged by:** feasibility-lead (#1, #2), business-analyst (#1, #5).
- **Cross-examination:** **STRENGTHENED**, with a narrower mission count:
  - Feasibility-lead (X1) and systems-designer (X3) showed that the exclusive kit choices multiply balance and test passes for every later mission, on top of the extra build cost. That makes the gap wider than a simple mission count suggests.
  - Business-analyst upgraded the readiness finding from MINOR to MAJOR once feasibility-lead pointed out that no one owns the gameplay code.
  - Adversarial-qa (C4) pointed out that the 22-mission figure partly double-counts the Act II choice missions, so business-analyst narrowed it to 18–22. Both reviewers note that 16 cycles fall short even at the low end.
  - Feasibility-lead added that several colleagues' fixes (checkpoints, reaction VO, tooltips, rescue missions) quietly add more unowned systems.

### #4 — The document never decides who "the player" is: one operator in the story, or a commander of expendable operators — BLOCKING
The story treats the player as a specific person: the Breakout prisoner, liked or disliked by the Act characters. The rules treat the player as commander of a customizable roster where anyone can die permanently. The document never says whether that prisoner can be lost, or who the characters are reacting to if they are.
- **Flagged by:** narrative-critic (#2), player-psychologist (#4). In Round 2, systems-designer (X6), feasibility-lead (X4), adversarial-qa (X4) and business-analyst (X3) all connected it to their own areas.
- **Cross-examination:** **STRENGTHENED.** Player-psychologist upgraded from MAJOR to BLOCKING because voiceover and cinematics are scheduled deliverables and every line spoken "to the player" depends on this decision. Feasibility-lead says the decision has to be made in week 1. Business-analyst says it decides whether the character creator earns its cost. Systems-designer and adversarial-qa showed that the "protected avatar" option creates its own exploit and its own economy problem, and narrative-critic argued against that option in C4.

### #5 — The finale puts the story's payoff on undeveloped characters and unspecified systems, in the last and riskiest content scheduled — BLOCKING / MAJOR
*Their Last Order* rests on a sacrifice choice between characters sketched with one adjective each, and the resistance leader is introduced only in Act IV. The mission fields 8 friendly units but never says who controls the allies or how the Downed, wipe and extraction rules apply to them. It has scripted deaths with no technical hooks, and its choice is recorded for a DLC.
- **Flagged by:** narrative-critic (#1, BLOCKING), feasibility-lead (#4, MAJOR), adversarial-qa (#4, MAJOR). In Round 2, player-psychologist (X5) and business-analyst (X4) took it up.
- **Cross-examination:** **STRENGTHENED.** Narrative-critic (X1) showed that nearly all character development is deferred to Act IV, the content most likely to be cut or rushed. Narrative-critic (X2) and player-psychologist (X5) found that a player could revive a character the script then kills. Adversarial-qa (X5) showed the scripted deaths can trigger the wipe definition, and with it the #1 reset exploit. Systems-designer (X5) noted the finale's choice can be retried at will. Business-analyst recommends building a cut-down version early as the vertical slice. Feasibility-lead proposes a fallback: the four principals fight as player-controlled operators and the NPC escorts are cut.

---

## 2. Unresolved disagreements

### D1 — How to fix the wipe/extraction inversion: let costly wins rewind, or make wipes cost something?
- **Make costly extractions rewindable** (player-psychologist C1, business-analyst C1, feasibility-lead C2). Offer the existing pre-mission snapshot after a costly story win too, so the player owns any losses they accept. This reuses existing code and adds no new save technology. Making wipes cost something would add a second route into the death spiral (player-psychologist).
- **Make story wipes carry a real cost** (narrative-critic C1). A default rewind makes every loss in the authored campaign optional, so the tagline "You will lose good people" would only hold in generated side missions. A rewind safety net should be an explicit difficulty option.
- **Constraints raised by others:** feasibility-lead opposes any mid-mission checkpoint as an unowned persistence system. Business-analyst opposes adding difficulty modes. Systems-designer and adversarial-qa insist the extraction warning must not ship before this rule is fixed.
- **Escalated decision:** How much punishment will the target player accept? Business-analyst names this as the root decision behind all three loss-model BLOCKING findings. The designer must choose one loss rule for the course build.

### D2 — Side missions: move them to stretch scope, or keep a minimum version?
- **Move to stretch scope** (feasibility-lead C1). This is the most expensive optional system in the document and won't fit 16 cycles. A recovery path that depends on content that won't be built isn't a real recovery path. Fix the softlock with a hard rule that tops the squad up to 4 recruits at the start of each story mission instead.
- **Keep a reduced version** (systems-designer C1, player-psychologist C2, adversarial-qa X3, business-analyst X1 after withdrawing their Round 1 "decorative" view). Side missions are the only recovery path the document names and they hold the capture/rescue loop. Business-analyst's minimum version: one or two job types, no modifiers, no capture roll, guaranteed replacement recruits.
- **Escalated decision:** Are side missions core scope for the course deliverable? Both positions require a roster floor whatever the answer.

### D3 — What to cut from the identity features: the memorial, callsigns and ranks, or only the body-fitting work?
- **Cut first** (business-analyst #2, X2). The character creator's body variants, achievements, ranks, the memorial, solo challenges, and capture/rescue are unowned engineering work and should be cut before kits.
- **Protect the cheap pieces** (narrative-critic C2, player-psychologist C3, feasibility-lead Round 2 #5). The memorial, callsigns and ranks are cheap and carry most of the emotional weight of losing someone; the memorial is the only place a loss is acknowledged. Feasibility-lead calls them cheap UI work that isn't worth cutting first.
- **Common ground:** Everyone agrees on cutting body-type and height fitting hard (two body types, no height slider).
- **Escalated decision:** Is the memorial/callsign/rank layer protected scope? Business-analyst (X3) says this also depends on the player-identity decision in #4.

### D4 — How severe is the kit cut-list conflict?
- **MINOR** (feasibility-lead Round 2 #3; player-psychologist narrowed theirs and left it at MINOR). It's real, but fixing it is one paragraph in the document. Consensus shouldn't be mistaken for production severity.
- **MAJOR** (business-analyst C3; adversarial-qa and narrative-critic keep it at MAJOR). Five of six reviewers flagged it independently. It is a planning error built into the document's only cut list.
- **Escalated decision:** None on substance, since everyone agrees on the fix. What's open is whether it counts as a production risk or a quick win. Feasibility-lead adds a timing condition: decide the cuts before the Act III–IV cycles begin.

---

## 3. Quick wins

1. **Name a fallback for every kit on the cut list.**
   - Give each of Bring Them Home / Chain of Command a replacement reward, plus a fallback for Keys to the Giants (feasibility-lead #3, adversarial-qa #3, business-analyst C3).
   - Cut in this order: Warmech first, then at most one of Medic or Captain, together with a redesign of the final choice (systems-designer C4).
   - Rewrite the "captured machinery" line in the narrative summary if the Warmech goes (narrative-critic Round 2 #3).
2. **Make "Open the Cages" pay off by having the rescued workers join the roster or raise the recruit training level** (systems-designer X4, player-psychologist X4). This gives the moral choice a consequence (narrative-critic #4), adds recruits between milestones (#2 above), and gives the player something concrete to choose between.
3. **Add an epilogue card or War Table beat that acknowledges the finale's choice inside the base game** (narrative-critic X4, business-analyst X5). Right now the climax's only branching consequence pays off in a DLC outside the graded deliverable.

---

## 4. Verdict

The document isn't ready to drive production. All six reviewers agree the premise and tactical core are worth building, but the board found five BLOCKING-level problems that have to be settled on paper before cycle 1:
- a loss model that rewards failing on purpose;
- a roster that can softlock;
- a budget that can't cover the mission count, with no one assigned to build the gameplay systems;
- no decision on who the player is;
- a finale that rests on undeveloped characters and unspecified systems.

The issues are tightly linked. Systems-designer, adversarial-qa and player-psychologist each warn that fixing one in isolation, like adding the extraction warning or cutting side missions, makes another worse. The single change that matters most is a single, written loss model covering four things:
- what a wipe costs compared with a costly extraction;
- a guaranteed roster floor;
- a save/quit rule;
- how scripted and NPC deaths fit in.

That loss model should come from an explicit decision about how much punishment the target player will accept. It is the convergence point of the #1 and #2 issues. It decides whether side missions are core scope (D2), and both the player-identity question (#4) and the finale's rules (#5) have to answer to it.
