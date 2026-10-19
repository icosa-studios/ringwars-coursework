# Production/Business Analyst — Round 1

## 1. The eight-week deliverable is larger than the document's own production budget — BLOCKING

**Problem.** The course target is "a full singleplayer campaign playthrough, from the opening escape through the final assault and ending" (Technical Strategy, Production foundation). The campaign tables list these authored story operations: Act I has 4 (Breakout, A Place to Stand, Dead Air, Sever the Ring). Act II has Follow the Freight and Hold What We Took. Act III has 4 (Keep the Crossing, Silence the Guns, Empty Their Shelves, Break the Line). Act IV has 4 (Under the Wall, Keys to the Giants, Break the Bastion, Their Last Order). On top of these are **four mutually exclusive choice pairs, which is 8 more missions**. Both sides of every pair have to be built, even though a single playthrough only sees one. That makes about **22 authored missions**. Act IV is also described as "four parts" with allied NPC squads, which may add more.

The token budget allows "two reference cycles per week." Over 8 weeks that is **16 cycles**, and the document says a cycle "can revise an existing mission; it describes an iteration budget." So the plan gives fewer than one cycle per mission before counting any rework. It also has no capacity for:
- generated side missions
- rescue missions for captured operators
- headquarters solo challenges
- Act IV cinematics

**Source.** "eight-week course deliverable is a full singleplayer campaign playthrough"; the Campaign arc and Mission choices tables; the Token budget section ("Two reference cycles per week...").

**Omission.** There is no mission count, no milestone schedule, no vertical-slice gate, and no list of missions that could be cut. The only cut list covers kits.

## 2. The cut list removes features the design depends on and keeps the decorative ones — MAJOR

**Problem.** "Kits to cut if needed: Warmech, Medic, and Captain." Two of these are tied into the campaign:
- The choice **"Bring Them Home or Chain of Command"** exists to "restore a medical team or recover a field commander, opening the corresponding support kit," meaning the Medic and the Captain. If both kits are cut, that choice has nothing to offer. "Affected missions remain playable" does not fix that.
- The Warmech is how "Keys to the Giants" ("take heavy equipment") pays off in Act IV, which is the campaign's climax.
- The Captain's Field Orders and the Medic's Rescue are the examples the document itself uses to show that training changes plans.

Meanwhile, these lower-value features are not on any cut list:
- the full character creator (body type, height, face, skin, eyes, hair, outfit pieces, skins, helmet toggle, and "equipment and clothing fit across the body options")
- skin purchases in the Armoury
- achievement-unlocked skins
- operator achievements and ranks
- the memorial
- the headquarters training space with solo challenges
- the hook for a "possible DLC continuation"

The document names art as "the largest technical constraint." Even so, the body-variant clothing-fit requirement is one of the most expensive art tasks in the document, and the only scoping is "a slim assortment."

**Source.** The course delivery target table; the Mission choices table; Appearance and personal identity; Operator achievements and ranks; Headquarters; Act IV and the final assault.

## 3. Procedural side missions and the capture/rescue loop are a second game inside the first — MAJOR

**Problem.** The document admits that story progression alone "is intended to outfit a standard squad." So side missions are optional breadth ("spare equipment, a larger working roster, and alternative builds"). They still require a lot of separate systems:
- a block-based mission generator with seed sweeps
- four side-mission types plus modifiers
- random equipment reward tables
- a 45% capture roll on wipe
- captive tracking
- "later optional rescue missions" as new operations

The document never decides whether this layer is core, a stretch goal, or cuttable. It is the most XCOM-like part of the design, but it is not needed for the stated deliverable. It also competes with the authored missions for the same Level Designer and Level Builder capacity.

**Source.** Authored and generated operations; Mission outcomes; Credits and equipment ownership; Existing verification workflow ("generated-mission seed sweeps").

## 4. Market position, audience, and product purpose are not defined — MAJOR

**Problem.** The document places itself in a crowded genre (turn-based squad tactics on PC and Mac) but never names a competitor or a reference title. Its main differentiator, "valid clear shots within optimal range are guaranteed hits," is clearly a response to the hit-chance frustration of XCOM-style games. The document never makes that argument, so it is unclear whether this is the selling point.

The audience description ("enjoys planning coordinated turns...") fits every game in the genre. It gives no target session length, difficulty modes, Ironman or permadeath options, price point, or player profile. Two choices in particular need their audience stated:
- The document says "This is war. You will lose good people," yet a story-mission wipe rewinds the player to before the attempt.
- A 45% capture roll replaces outright death on side missions.

It is also unclear what kind of product this is. It is an "eight-week course deliverable" with alpha-quality cinematics and VO, but it also has a paid-skin Armoury and a "possible DLC continuation." A commercial roadmap and a coursework scope pull priorities in opposite directions, and the document never says which one wins.

**Source.** Executive Summary (audience and distinctive-appeal paragraphs); the Attacks and damage section; the Mission outcomes table; the Armoury; Victory/DLC; the course delivery target.

## 5. The production readiness claim is asserted, not shown — MINOR

**Problem.** The document says "the level-building system is complete, tested, and approved" and that "the critical path... is established." The same document then says token estimates will be refined by "actual usage from the first cycles." If the pipeline were already proven, those measurements would exist and would back up the 160,000-token level-build figure. The plan's feasibility depends on this claim, but the document gives no evidence: no count of shipped levels, no measured cycle time, and no measured per-mission cost.

Similarly, the Act characters are described only as archetypes ("a gruff man who dislikes the player"), with no names. Yet voiceover and cinematics for them are scheduled deliverables. Content that has not been written yet is being budgeted as if it were ready to produce.

**Source.** Production foundation and course scope; Token budget; Act characters.

## Round 2 — Cross-examination

### Conflicts

**C1. The Psychologist's fixes for the loss model add scope the deliverable cannot carry, and the Systems Designer's fixes pull the other way. Both are an audience decision that has not been made (Psychologist #1, Systems Designer #1, QA #2).**

Three reviewers rate the loss model BLOCKING, and I agree the logic is broken. The proposed fixes conflict, though:
- The Psychologist recommends "difficulty and save options" plus a roster floor. Those are forgiving fixes.
- The Systems Designer recommends that "story wipes carry a real carry-over cost." That is a punishing fix.

Difficulty modes are a new feature. Each mode adds a balance pass that the Balance Agent would have to run inside a 16-cycle budget that already cannot cover the missions (my #1, Feasibility #1). I oppose adding modes for the course build.

The real gap is the one in my #4. The document never says how much punishment its audience will accept, so every reviewer is picking a different player to design for. My position: pick one rule and ship one mode. The cheapest coherent option is to make a costly story-mission extraction rewindable the same way a wipe already is (the Systems Designer's "checkpoint the player chooses"). That reuses the existing rewind code path, removes the incentive to wipe deliberately, and adds no new system. Ironman and permadeath can be a post-course stretch goal.

**C2. Nobody objected to cutting cosmetics, but the Systems Designer's economy finding weakens part of my cut recommendation (Systems Designer #3 vs. my #2).**

The Systems Designer notes that "credits have almost no sink besides extra copies and cosmetics." I proposed cutting Armoury skin purchases. If they go, credits lose their last late-game use even sooner.

I am keeping the recommendation. The finding shows that the credit economy itself is under-motivated in this scope, and adding a decorative sink to rescue a currency the deliverable does not need is the wrong fix. For the course build, credits should either buy equipment copies and nothing else, or be folded into story-granted and side-mission-granted equipment entirely. Skins can return when the commercial roadmap (DLC, paid skins) becomes real. My concession is that this cut and the economy table are one decision, not two.

**C3. The Psychologist rates the cut-list and choice collision MINOR; I disagree (Psychologist #5).**

Five of six reviewers independently flagged "Kits to cut if needed: Warmech, Medic, and Captain" against "Bring Them Home or Chain of Command" and Keys to the Giants. That is the strongest agreement on the board. It is MAJOR because it is a planning error baked into the only cut list the document has. It is also the cheapest fix on the board, since it is a document decision and not a build task. The Moderator should list it as a quick win, not downgrade it.

### Connections

**X1. Side missions are not cleanly cuttable, because they are the only recovery valve for roster loss (my #3 + QA #1, Psychologist #1, Systems Designer #2).**

I called the side-mission layer "a second game" that could be a stretch goal. Combined with the softlock findings, that recommendation is dangerous as written. The document's only recovery path after story losses is "complete available side missions." Side missions are also the main source of "a larger working roster" and of credits. Cutting them outright makes the softlock QA describes worse, not better.

The production answer is a **minimum side-mission layer**:
- one or two job types
- no modifiers
- no capture roll or rescue missions (abandoned operators are simply lost, or return wounded)
- a guaranteed replacement-recruit rule

Separately, the line "Authored blocks can also enter the library used for generated side missions" (Technical Strategy) means the block content is partly paid for by story missions. The expensive part is code: the generator, reward tables, and captive tracking. That leads to X2.

**X2. Feasibility #2 (no owner for gameplay code) turns my readiness finding into a schedule hole.**

My #5 noted that "complete, tested, and approved" covers only the level pipeline. The Feasibility Lead shows that no agent or budget line covers gameplay C#: AI, Overwatch and Suppression, the generator, the character creator, persistence, and cinematics.

Together these findings mean every feature I listed as decorative in #2 and #3 is also unowned engineering work, not just art. The cut list therefore has to be ordered by engineering cost as well as art cost. On that ordering, the following are the first cuts:
- the character creator's body and height variants
- achievements, ranks, and the memorial
- the training-space solo challenges
- capture and rescue

**X3. The player-identity decision decides whether the character creator is load-bearing (Narrative #2, Psychologist #4 + my #2, Feasibility #5).**

If the Breakout prisoner is a persistent avatar, a creator is part of the identity promise and should be kept in reduced form (two body types, no height slider, per Feasibility #5). If the player is an off-screen commander, the creator is pure decoration, and presets with editable callsigns are enough. Either way, the document is paying for the most expensive version of a feature whose purpose has not been decided. The identity question is narrative, but its answer is a scope decision.

**X4. The narrative fixes have no budget, and the finale is scheduled last (Narrative #1 and #4, Feasibility #4, QA #4 + my #1).**

The Narrative Critic is right that the sacrifice choice needs named, sustained characters and visible reactions to choices. Each of those is VO, writing, and possibly cinematics. Voiceover is budgeted per mission cycle. Character presence between missions (HQ, War Table) and branch-dependent reaction lines are not.

Their Last Order is also the mission with the most undefined systems: 8 friendly units, NPC Downed rules, scripted deaths, and DLC save fields. It depends on all four Act characters and comes last in the schedule. A campaign where the final mission is both the riskiest and the latest has no vertical-slice gate, which is the omission I flagged in #1.

My recommendations:
- Build a cut-down Their Last Order early, as the vertical slice.
- Deliver character continuity through cheap channels (War Table briefings and HQ lines) rather than cinematics.

**X5. The DLC hook damages the course ending (Narrative #4 + my #4).**

The Narrative Critic notes that the finale's only major branching decision is "record[ed]" for "a possible DLC continuation" and has no in-game payoff. The deliverable is defined as a playthrough "through the final assault and ending." Deferring the climax's consequence to a product that does not exist trades the course grade for a commercial hope. This is the clearest example of the coursework-vs-commercial tension in my #4. The fix is cheap: an epilogue card or War Table beat that acknowledges the choice.

### Revisions

- **#1 (mission count): keep BLOCKING, and narrow the count.** The Act II row lists "rescue and weapons choices" as its representative operations, and some later choice pairs may map onto named Act III or IV missions, as Feasibility #1 also allows. The defensible figure is **18-22 authored missions**, not 22. Even at the low end, 16 cycles cannot cover it, and the Feasibility Lead independently reaches the same conclusion. Also, "representative operations" suggests the list may not be exhaustive, so the count could be higher.
- **#3 (side missions): keep MAJOR, and change the recommendation** from "decide whether to cut" to "define a minimum layer," per X1. I withdraw the implication that the layer is cleanly decorative.
- **#4 (market and audience): split it.** The competitor, price, and reference-title points drop to **MINOR** for a coursework deliverable. The audience punishment-tolerance point rises to **MAJOR, close to BLOCKING**, because it is the root decision behind the three BLOCKING loss-model findings (C1). The commercial-vs-coursework conflict stays MAJOR via X5.
- **#5 (readiness): upgrade MINOR to MAJOR.** Combined with Feasibility #2, the unproven readiness claim covers all gameplay code, not only the token estimates, so the plan's feasibility cannot be judged until a system status table exists.
- **#2 (cut list): unchanged at MAJOR.** I concede C2 (the skins cut must be decided together with the economy), and X2 and X3 add an engineering-cost ordering and an identity dependency to the cut list.
