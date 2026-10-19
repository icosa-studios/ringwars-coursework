# Technical Feasibility Lead — Round 1

Scope reviewed: `gdd.txt` (Ring Wars GDD, draft dated 2026-10-19). I judge it against what it says it will ship: a full campaign playthrough in eight weeks, built by one developer with AI agents, in Unity 6/URP.

---

## 1. The token budget cannot pay for the authored campaign the deliverable promises — BLOCKING

**Problem.** The document's own numbers don't produce enough missions for a "full singleplayer campaign playthrough, from the opening escape through the final assault and ending."

**Evidence.**
- Throughput: "Two reference cycles per week," each covering one mission's design, build, voiceover, balance and verification (320k tokens). Over eight weeks that is **16 cycles**. The document also says "A cycle can revise an existing mission," so rework uses up the same cycles.
- Content required (Campaign arc and Mission choices tables): Act I has 4 named missions (Breakout, A Place to Stand, Dead Air, Sever the Ring). Act II has Follow the Freight and Hold What We Took. Act III has 4 named missions. Act IV has 4 named missions and is also described as "four parts, each centered on one of the Act characters." That makes **about 14 authored missions on the critical path**.
- The four mutually exclusive choices (Open the Cages / Take the Assembly Line, Long Reach / Heavy Hands, Fuel for the Fire / Hard Shell, Bring Them Home / Chain of Command) mean **both branches have to be built** for every playthrough to be possible. That adds up to 8 more missions, though some may overlap with the "representative operations."
- Not counted in any cycle: generated side missions (4 job types plus modifiers, built from "hand-authored spatial blocks"), headquarters (Barracks, Armoury, War Table), and the "training space" with "optional solo challenges."

The total is roughly 18-22 authored missions plus HQ and side-mission blocks. Even with perfect first-pass results, 16 cycles can't cover that. The 360k/week "for integration, investigation, and rework" adds up to about 2.9M, which is about 9 more cycles if it were all spent on new missions. That still leaves no rework.

**What's missing.** The cut list covers kits and polish only. It doesn't say which missions get cut, merged or collapsed, or whether choice branches can be stubbed. The plan needs a mission-level cut order. One example: make the branch choices share one map with a different reward.

---

## 2. Nobody is assigned to build or pay for the game's systems, and their current state isn't stated — BLOCKING

**Problem.** All five agents (Voiceover, Level Designer, Level Builder, Balance, Testing) produce or check content. No agent, budget line or schedule covers the gameplay code the GDD depends on.

**Evidence.** "Unity executes the tactical rules and enemy behavior described in Game Mechanics" says what runs the systems, not who builds them. Systems specified without an owner or budget:
- free-position movement with AP-band previews and waypoints
- direction-dependent destructible cover
- control cones that "narrow with aim distance" and are "cut off" by walls
- Overwatch and Suppressing Fire reaction systems
- lobbed-grenade arcs
- multi-floor roof cutaways
- role- and orders-based enemy AI with "remembered contact"
- the procedural side-mission assembler
- directed action-shot camera
- the character creator
- achievements and ranks
- campaign persistence and economy
- cinematics (an "Alpha-quality" deliverable with no agent and no tokens)

The only system the document says is finished is the level-building pipeline: "complete, tested, and approved." "Existing verification workflow" suggests that movement, combat, objectives, extraction and the HQ return exist in some form, but the document never lists what is done and what is left. Without that list, nobody can tell whether eight weeks is a content sprint, which might work, or a systems-plus-content build, which won't.

**Recommendation.** Add a system status table (done / partial / not started) and say who writes gameplay C#, whether that is Jim or an agent, and what it costs in tokens or hours.

---

## 3. The kit cut list breaks the campaign structures that depend on those kits — MAJOR

**Problem.** "Kits to cut if needed: Warmech, Medic, and Captain," along with "affected missions remain playable with the available equipment." That addresses whether a mission can be played, but not that the campaign design is built around these kits.

**Evidence.**
- "Bring Them Home or Chain of Command — Restore a medical team or recover a field commander, **opening the corresponding support kit**." If Medic and Captain are both cut, both sides of this choice give nothing, so the choice is empty.
- "Keys to the Giants" ("take heavy equipment") and "Mission-supplied equipment supports specific scenarios, **including the Warmech assault**." Cutting Warmech means redesigning at least one Act IV mission, not just removing an item. The Warmech is also the most expensive of the three to build (new rig, animation set, scale, navigation footprint, camera framing).
- The design leans on these kits elsewhere. Captain's Field Orders and Medic's Rescue are the doc's examples of training that changes the plan. The canonical example operation brings a Medic.

**Recommendation.** For each cut kit, name the replacement reward for its choice mission and the fallback design for the Warmech mission. Decide the cut early, because content built around these kits would be wasted.

---

## 4. The Act IV allied squads and the final mission need systems the document never specifies — MAJOR

**Problem.** The ending needs new runtime features that appear nowhere in Game Mechanics.

**Evidence.**
- "Each character brings **2-3 NPC operators** from their own squad to assist. The closing missions bring several of those allied squads together."
- "In Their Last Order ... the assault team consists of the player's 4 operators and the four principal characters." That is eight friendly units against a standard squad of 4. The UI, AP pacing and balance are all tuned for 4.
- Game Mechanics only describes the player's operators and Directorate AI. It never says whether allied NPCs are player-controlled (does the HUD scale? how does Tab cycling and the squad lineup handle them?) or AI-controlled (which means a whole new friendly-AI behavior set that has to respect the player's cones, smoke and blast zones).
- Scripted story events during combat: "The resistance leader dies, and at least one of the other three characters also dies." There is also a player choice that "dooms one of those other characters," recorded for DLC. That needs scripted encounter-state hooks, branching outcomes and save-data fields, none of which the AI Architecture or Technical Strategy sections mention.

This content comes last in the schedule, depends on all four Act characters' content being finished, and has no fallback.

---

## 5. Two "low-cost" claims hide big costs: the capital asset set and the character creator — MAJOR

**Problem.** Two places where the doc presents something as already handled or reduced in scope, while the expensive part is still there.

**Evidence.**
- *Capital environments.* The level-building system is "complete," but "additional settings and asset sets are added **as time allows**." Act IV is set in a capital with "art deco architecture, elaborate doors, polished surfaces, and ornament," which is a separate asset vocabulary from the "concrete, gunmetal" facilities. The doc names art production as "the largest technical constraint." The campaign's climax therefore depends on an asset set the plan treats as optional.
- *Unvalidated estimates.* If the level-build pipeline is "complete, tested, and approved," real per-mission token usage should already be known. Instead, the 160k-token build figure is an "initial planning estimate" that "actual usage from the first cycles will refine." Either the pipeline hasn't been used at production volume, or the numbers already exist and should replace the guesses.
- *Character creator.* Cosmetics are cut to "a slim assortment," but the feature still needs "body type and height," and "Equipment and clothing fit across the body options," with kit-specific worn pieces and a toggle for helmet visibility. Fitting gear across body types and heights is a rigging and skinning problem that grows with every outfit and kit piece. Fewer cosmetics doesn't make it cheaper. It also hits the directed close-up shots and portraits.

**Recommendation.** Put the capital asset set on the critical path or plan Act IV around existing facility assets. Fix the body-type count (for example, two body types and no height slider) as an explicit scope limit.

---

## Round 2 — Cross-examination

### CONFLICTS

**C1. Business Analyst #3 (cut the side-mission layer) vs. Systems Designer #2, Psychologist #1, QA #1 (side missions are the way to recover from roster losses).** I side with the Business Analyst, and I would go further. The three roster-floor findings all assume side missions are how a depleted player recovers ("complete available side missions"). From a build standpoint, the side-mission layer is the most expensive optional system in the document: a block assembler, seed sweeps, 4 job types plus modifiers, reward tables, the capture roll, captive tracking, and rescue operations. My Round 1 Finding 1 already shows the 16 cycles can't cover the story missions. A recovery path that depends on a second content pipeline that won't get built is not a real recovery path. The cheaper and more reliable fix for the roster softlock is a hard rule: an emergency recruit fills the squad up to 4 at the start of any story mission. That is a few lines of persistence logic, not a content pipeline. With that rule in place, side missions can move to stretch scope. That also removes the side-mission wipe roll, the 45% capture branch, and the grind ceiling the Systems Designer worries about in #2. I disagree with the implied position that the roster problem should be solved by adding more side-mission supply.

**C2. Systems Designer #1 fix option "Story-mission retries also roll back after costly wins (a checkpoint the player chooses)" and QA #2 "Define save points."** I agree with the diagnosis that wiping beats extracting. I disagree with any fix that adds mid-mission saves or player-chosen checkpoints. Saving a mission in progress means serializing AP state, live control cones, destructible cover damage, AI "remembered contact," grenade response windows and partial movement. That is a large new persistence system, and it is unowned (see my Finding 2). The document already has a pre-mission snapshot ("returns to before the failed attempt"). The cheapest consistent fix is to offer that same snapshot after a costly story-mission success ("Accept losses / Retry from deployment"), or to make story wipes cost something. Either one reuses existing state and adds no new save technology. The board should recommend the cheap option explicitly so Round 3 doesn't endorse a fix that turns into a hidden systems task.

**C3. Narrative Critic #4 (choices need visible story reactions) and #1 (characters need much more depth).** As story critique these are fair, but they are scope increases on a plan that is already over budget. Every reaction to a choice or road not taken is branching VO. The Voiceover Agent sits inside each 320k cycle, and a reaction to an earlier choice multiplies lines per later mission by the number of branches. If the board recommends this, it has to come with a cost limit: text-only or HQ-only reactions (one line from the Act character at the War Table per choice), not per-mission branched VO. I'd also push back on the idea that the Act characters can't be voiced yet. That point (also Business Analyst #5) is right, but it makes the problem a scheduling dependency: character writing has to finish before the first VO cycle, and nothing in the plan schedules it.

**C4. Business Analyst #5 rates "readiness asserted, not shown" MINOR. I rated the same evidence as part of a MAJOR.** My BLOCKING Finding 1 and the Business Analyst's BLOCKING #1 both rest on the 160k/320k cycle figures. The document itself calls those an unvalidated "initial planning estimate." If the base number for the board's top-ranked finding is unvalidated, that matters to every other number, and the Business Analyst should rate it MAJOR. The uncertainty also probably runs one way. First-cycle estimates for an agent pipeline usually leave out failed generations and verification reruns, so actual cost is more likely to be higher than lower.

### CONNECTIONS

**X1. Systems Designer #4 + my Finding 1: kit choices multiply the testing and balance matrix.** The Systems Designer notes that every later encounter must be beatable "both without the Sniper and without the Minigun." Combine that with the other pre-finale exclusive choices (Open the Cages / Assembly Line, Long Reach / Heavy Hands, Fuel / Hard Shell) and each Act III-IV mission has up to 2^3 = 8 loadout states to balance and verify. The Bring Them Home choice adds a fourth axis for the finale. The 320k cycle budgets one Balance pass and one Testing pass per mission, not one per branch state. So the branch structure costs more than the 8 extra missions I counted in Round 1, because it also multiplies verification on every mission after it. The plan should either make branch rewards overlap (a sidegrade, with the unchosen kit purchasable later in the Armoury) or accept that balance is only checked on one path.

**X2. Systems Designer #3 (no economy numbers) + the Balance Agent in Technical Strategy.** Each cycle spends Balance Agent tokens to produce "before-and-after observations," but the design gives no target to compare them against. Until an economy table exists, Balance spend in every cycle has nothing to measure progress against, and some share of 16 x 320k is spent without a target. The economy table is a production prerequisite, not just a design nicety. It has to exist before cycle 1.

**X3. QA #5 (undefined control-cone rules) + my Finding 2 (unowned systems).** In Round 1 I said nobody is assigned to build cones and reactions. QA shows the spec also can't be implemented as written: stacking, reaction counts, AP forfeiture and Revive triggers are all undefined. That makes the risk worse. It isn't only an unowned system but an underspecified one, so whoever builds it will make design calls in code. Enemy use of cones also has an AI cost QA didn't mention. Directorate AI has to reason about where to place Overwatch and Suppressing Fire against free-position movement, which is the hardest AI problem in the document. AI Architecture covers roles and orders only.

**X4. QA #4 + Narrative #2 + Psychologist #4 + my Finding 4: the finale needs persistent-identity flags that the codebase doesn't define.** Both "who is the player" and the scripted Act IV deaths come down to data the document never specifies: an is-protected flag on the Breakout operator, death-override hooks on principal NPCs, and a DLC-recorded choice field. Each one is cheap alone. Together they touch the Downed system, extraction resolution, the wipe check and save data, and all of that is needed in the last mission built. If the decision comes late, finished systems get reworked late. The identity decision has to be made in week 1, not when Act IV is built.

**X5. Psychologist #3 (no tutorial or tooltip layer) + my Finding 2.** Contextual help, first-exposure tooltips and a glossary are one more UI system with no owner or budget. If this becomes a board recommendation, it belongs on the unowned-systems list.

### REVISIONS

- **Finding 1 (token budget): stays BLOCKING, made stronger** by X1. Branching multiplies verification cost as well as mission count. I also adopt the Business Analyst's tighter count of 22 missions as the upper bound of my 18-22 range.
- **Finding 2 (unowned systems): stays BLOCKING**, and I add tooltips/tutorial (X5) and Overwatch/Suppression AI (X3). I'd also ask Round 3 to note that several colleague fixes (checkpoints, reaction VO, rescue missions, tooltip layers) quietly add to this list.
- **Finding 3 (kit cut list): downgraded MAJOR to MINOR from the feasibility lens.** Five of six reviewers flagged this, so it is clearly real, and I don't want the synthesis to read that consensus as production severity. Fixing it costs one paragraph in the document, such as a replacement reward per choice and a Keys to the Giants fallback. The production risk only appears if Warmech or Act IV content is built before the cut decision. That timing point is the part worth keeping: decide the kit cuts before Act III-IV cycles begin.
- **Finding 4 (Act IV allies): stays MAJOR, with an added recommendation.** QA #4 adds the Downed, wipe and extraction gaps for NPCs, and I accept them. Because this is the costliest new system and comes last, I now recommend a specific fallback for the cut list: principal characters fight as player-controlled operators under normal rules (squad of 4 + 4, no AI allies), and the 2-3 NPC escorts per character are cut. That removes the friendly-AI requirement completely.
- **Finding 5 (hidden costs): stays MAJOR.** The Business Analyst's #2 independently reached the same view of the character creator's clothing-fit cost, which supports it. I'd separate it from the other items on the Business Analyst's list: the memorial, achievements and ranks are cheap UI and persistence work and are not worth cutting first. The cuts that save real money are clothing fit across body variants, the side-mission generator (C1), and the capital asset set.
