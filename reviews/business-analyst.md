# Production/Business Analyst — Round 1

## 1. No scope boundary between "the game" and "the eight-week deliverable" — BLOCKING

**Problem.** The design describes a full commercial campaign, but the only production timeline is an eight-week course run by a solo developer. The document never says what already exists, what the eight weeks will deliver, or what gets cut if time runs short. Without that, nobody can judge feasibility or set priorities.

**Source.** Technical Strategy says "The eight-week course builds on the existing game through playable slices" but never lists what the existing game contains. Meanwhile the content load is large:
- 9 kits, including the Warmech.
- 4 acts with about 14 named story operations (lines 344-347).
- 4 mutually exclusive choice pairs, which add 8 more authored missions (lines 357-360).
- A procedural side-mission generator.
- A body-type character creator.
- Armoury and skins, a memorial, and solo training challenges.

The token budget pays for about 2 "reference production cycles" a week, so about 16 over the course. The document also says "A cycle can revise an existing mission; it describes an iteration budget", so those 16 cycles are not 16 new missions. 16 cycles cannot build or finish a campaign of about 22 authored missions, plus side-mission blocks, plus everything else.

**Omission.** There is no MVP or vertical-slice definition, no priority-ordered feature list, no "must / should / won't" table, and no inventory of existing work.

## 2. The character creator works against the document's own top production risk — MAJOR

**Problem.** The document names art production as "the largest technical constraint" for a solo developer. It then commits to one of the most art-expensive features in the genre, and that feature is decorative by the document's own description.

**Source.** Appearance and personal identity says "Players can choose body type and height, face, skin tone, eye color, hair, outfit pieces, and available skins. Equipment and clothing fit across the body options. Kit equipment can add distinctive worn pieces, including a helmet whose visibility the player can control." The same section says "Its choices are independent of combat effectiveness."

Cost: every outfit, kit piece, and helmet has to be fitted, rigged, and checked against every body type and height, in portraits, the HQ lineup, and close action shots (line 252). That multiplies the art work that Biggest Technical Constraint (line 591) says is already the bottleneck.

**Assessment.** The "squad with an identity" pillar is load-bearing. The full creator is not: callsigns, a small set of presets, mission history, and the memorial would deliver most of the attachment for a fraction of the cost. The document never weighs this trade-off.

## 3. Branching choices and procedural side missions add a lot of work to build and test that most players never see — MAJOR

**Problem.** Two structural features add authoring and testing work without adding much to a single playthrough. The document does not count that cost, and it does not resolve how generated missions get checked.

- **Branching.** The four choice pairs (lines 355-360) mean each player sees only half of 8 authored missions. Two pairs also lock out kits: "Bring Them Home or Chain of Command ... opening the corresponding support kit" (Medic or Captain), and "Long Reach or Heavy Hands" (precision or heavy weapons). So all 9 kits must be balanced, taught, and supported, even though any one campaign uses only a subset. Later story missions must also work for every combination of branches. The document never says how many branch combinations later missions must be tested against.
- **Generated side missions.** Lines 326-328 call for a runtime system that assembles authored blocks. Lines 406 and 412 make side missions load-bearing for the economy ("Side missions support spare equipment, a larger working roster"), so they cannot simply be cut. Line 531 also claims "Development agents produce those building blocks and check the resulting missions before they reach the player." If assembly happens at runtime, agents cannot check each generated result. The QA model is never specified: seeded pre-validation, constraint rules, or a fixed curated pool.

## 4. No market positioning, competitors, or commercial frame — MAJOR

**Problem.** The document claims a "distinctive appeal" (line 48) but never places it against the market. Its main hook is "Valid attacks hit, with damage varying within a visible range". In 2026, that sits in a crowded field of tactics games that have already moved away from hit-chance RNG or reworked it: Gears Tactics, Mario + Rabbids, Into the Breach, Marvel's Midnight Suns. The setup of an elite outnumbered squad, a resistance HQ, a war table, and a roster with permadeath-style loss and a memorial lines up closely with the XCOM 2 template. The document gives no reason a player would choose this over those titles.

**Omission.**
- No comparable titles.
- No price point or business model. The Armoury sells "available skins", and line 408 says skins are "bought where available". It is unclear whether that means in-game credits only or real money.
- No storefront or platform plan beyond "Windows and macOS".
- No expected campaign length or session length.
- No statement of whether a commercial release is a goal at all, or whether this is coursework only.

The audience statement (line 46: players who "enjoy planning coordinated turns, experimenting with squad composition, and developing recognizable characters") describes every squad-tactics fan. It does not separate this game's audience from XCOM's.

## 5. The document is two documents for two audiences — MINOR

**Problem.** Sections 1-6 are a player-facing game design. Sections 7-8 (AI Architecture and Technical Strategy) are a production-pipeline proposal for a course about AI agents, with token budgets, JSON manifests, and API rate limits. The executive summary and pillars never mention the pipeline, and the pipeline sections only loosely trace their deliverables back to the pillars. A reader cannot tell which is the primary deliverable being judged: the game, or the agent workflow that produces it.

**Related omission.** The Balance and Testing agents are expected to report "before-and-after observations from the relevant gameplay scenario" and "reproduction steps with evidence", but the document never says how an agent plays or exercises a turn-based Unity build. There is no test harness, scripted scenario runner, or headless simulation. Those two roles carry the quality promise of the whole pipeline.

**Recommendation.** Add a one-paragraph framing up front that says what is being delivered and to whom. Then link each agent role to the specific pillar and mission content it serves in the eight-week window.

## Round 2 — Cross-examination

### CONFLICTS

**C1. Feasibility Lead #5 rates customization MINOR. I hold MAJOR.**
The Feasibility Lead and I agree on the mechanism: gear from mixed vendors has to fit every body type and height, and it has to survive close action-camera framing. They then rate it MINOR, which I think is wrong for two reasons. First, the document names art as "the largest technical constraint". A feature that multiplies the cost of the stated bottleneck cannot be minor by the document's own logic. Second, their own Finding #1 lists customization as one of the items with unknown build status. If the creator is not already built, it is one of the few features that is both expensive and, by the GDD's own words ("independent of combat effectiveness"), not tied to any system. That makes it the cleanest cut on the board. Their suggested cut (one body type, swappable outfits) is the right one. The severity should match the size of the saving.

**C2. Feasibility Lead #1 proposes "Act 1 plus one side-mission type" as the week-8 target. I disagree with the second half.**
We agree on the BLOCKING finding. But putting a side-mission type in the first slice means building the generator, its block library, and seed persistence before the authored campaign exists, and Feasibility #2 shows that the generator has no validation path. For an eight-week slice, the generator is the item with the most new tooling and the least effect on the pillars. A better target is Act 1 authored missions plus the HQ loop through menus. Side missions should come later, and start as a small fixed pool of hand-checked layouts. I am now partly reversing my own Round 1 wording: I said side missions "cannot simply be cut" because the economy depends on them. That is true for the finished game, not for the slice.

**C3. Systems Designer #2 and Adversarial QA #3 both ask for limits on side-mission availability. That undercuts the business case for building a generator at all.**
Both reviewers are right that unlimited side missions allow farming. Their fix is a ceiling: limit or stop refilling the side-mission pool. But if the pool is capped at a small number per act, the reason to build a runtime procedural generator mostly goes away. A fixed list of authored or pre-baked side missions gives the same player experience for much less engineering and QA. So their balance fix and my scope concern point the same way, but the document has to choose: either the generator is a replay engine with an uncapped economy (which the Systems Designer shows is broken), or the pool is capped and the generator is overbuilt. It cannot be both.

**C4. Narrative Critic #1, #3 and #5 and Player Psychologist #4 each call for added content. Each addition increases scope I already rate BLOCKING.**
The fixes they propose are: named characters on both sides; missions that use the insider-resistance premise; later briefings that acknowledge the branch not taken; and choice-screen previews or trials of locked kits. Each is reasonable on its own. Together they add authored writing, voiced lines (through the Voiceover Agent with fixed speaker identities), and UI that the eight-week budget cannot cover. I am not arguing that their findings are wrong. I am arguing that the cheapest fix for most of them is subtraction. Narrative #5 and Psychologist #4 both get resolved, and so does Systems #4, if the four choice pairs stop locking kits and become reward or story variants. Adding acknowledgment and previews on top of the lockouts is the expensive fix.

### CONNECTIONS

**X1. The wipe exploit sinks the one market differentiator the document could claim.**
Systems #1, Psychologist #1, and QA #1 all find that a full-squad wipe costs less than losing one operator. In market terms, the closest competitor (XCOM 2) is defined by meaningful permanent loss, often with an ironman mode. My Finding #4 said the GDD offers no reason to pick this game over XCOM. The pitch line "bring your operators home", plus the explicit leave-behind decision, was the closest thing to a hook. With the wipe exploit and no save rules (Psychologist #1), that hook is gone: the game plays like XCOM with savescumming built in. Fixing the failure rule is a design matter, but it also decides whether the game has a pitch.

**X2. Narrative Critic #1 points to the positioning I said was missing.**
The insider resistance, built "from the Directorate's own logistics organization", is the only idea in the document that no listed competitor has. Missions where the squad uses inside knowledge (forged orders, known patrol schedules, supply-chain sabotage) would separate the game from the "outnumbered elite squad" template. They could also justify a distinct mechanic. The document uses this idea only in the setting paragraph. That changes my Finding #4 from "no differentiator exists" to "a differentiator exists and is not used".

**X3. Every reviewer's rule gaps land on a test harness that does not exist.**
QA #5 (objective and NPC failure states), QA #4 (AP loops), Systems #4 (16 branch paths), Feasibility #2 (generator validation), and Feasibility #3 ("playable-path checks") all assume an agent or script can run a turn-based scenario and report the result. My Round 1 Finding #5 noted that no harness is specified. Combined with those findings, it is clear the whole QA promise of Sections 7-8 depends on that one missing piece of tooling.

**X4. Psychologist #3 (onboarding overload in mission 2) is also a scope problem.**
The second mission opens the whole physical HQ: Barracks, Armoury, War Table, training, appearance. Those are the features with the most uncertain build status (Feasibility #1). Opening HQ functions in stages over Act 1 would help new players, and it would also let the slice ship with fewer HQ functions finished. The same change fixes both problems.

### REVISIONS

- **Finding #1 (BLOCKING): keep, and widen it.** Feasibility #1 adds a point I missed: the plan budgets tokens but never Jim's own review time, and that is the real throughput limit at two cycles a week. I adopt it.
- **Finding #3: reframe, keep MAJOR.** I called branching content "most players never see". Systems #4 and Psychologist #4 show it is worse than that: the kit lockouts change the difficulty curve on every path, including removing ranged revive, which is central to the loss system. The cost is not only unseen content; it is a balance matrix of 16 paths. The generated-missions half overlaps with Feasibility #2. I defer to their technical framing and keep only the cost and business-case point (see C3).
- **Finding #4: keep MAJOR, change the recommendation.** See X1 and X2. The fix is to commit to the insider-resistance premise as the hook, and to fix the failure rule so that the loss pillar is credible against XCOM.
- **Finding #5: split it.** The "two documents" framing stays MINOR. The missing test harness moves up to MAJOR, because X3 shows that five findings from three other reviewers cannot be checked without it.
