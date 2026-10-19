# Technical Feasibility Lead — Round 1

Context judged against: one developer ("Jim", "A solo developer"), an eight-week course, Unity 6 / URP, a contemporary LLM/agent toolchain, Windows and macOS targets.

## 1. The document never says what the eight weeks will deliver, what already exists, or what gets cut. BLOCKING

**Passage:** Technical Strategy: "The eight-week course builds on the existing game through playable slices." Token budget: "Two reference cycles per week... A cycle can revise an existing mission; it describes an iteration budget."

**Problem:** The design describes a full commercial-scope campaign:
- 4 acts with about 14 named story operations, plus 4 mutually exclusive mission pairs (8 more authored missions, most of them gated content that only some players will see).
- 9 kits, each with ordered training lines.
- Generated side missions with modifiers.
- Customizable operators with body types and heights.
- A physical headquarters with Barracks, Armoury, War Table, and a training space with solo challenges.
- A memorial, skins and achievements.
- A mission-supplied Warmech.
- Directed action cameras.
- Two desktop platforms.

Against that, the production plan allows at most 16 "reference cycles" in eight weeks. The document says outright that a cycle is an iteration, not a finished mission. Nothing lists which systems from the "existing game" already work, so a reader cannot tell whether destructible cover, the generator, customization or the HQ are built or still planned.

There is no cut list, no priority order, and no definition of what counts as done at week 8. Missions that sit on only one branch of a choice pair are an expensive kind of content, and the document does not mention that. The plan budgets tokens but never budgets Jim's time. Under this plan Jim approves creative direction, judges every playable result through play, and reviews art from two camera modes. At two cycles a week that is the real throughput limit, and nothing estimates it.

**Needed:** An inventory of what exists, a must/should/cut list, and a stated target for week 8 (for example, Act 1 plus one side-mission type).

## 2. Generated side missions cannot be verified the way the pipeline claims. MAJOR

**Passage:** AI Architecture: "Generated side missions assemble authored spatial blocks and encounter definitions. Development agents produce those building blocks and check the resulting missions before they reach the player." Missions and tactical spaces: "Variation changes routes, approach angles, objectives, cover decisions, and enemy placement while retaining a coherent facility. Each offered mission retains its setup across retries."

**Problem:** Unity assembles these missions at runtime with "zero generative-AI tokens". So no agent ever sees the specific mission a player gets. Agents can check individual blocks but not every possible combination of blocks.

Each assembled site still has to meet a lot of requirements:
- Navigation has to connect across block seams.
- Ladders and rooftops have to join up, and Page Up/Down floor viewing has to work.
- Reinforcement entry points have to sit on "believable exterior approaches".
- Extraction has to be reachable from the objective.
- Tall surroundings must not block the tactical camera.
- Seeds must persist so a retry gets the same setup.

The plan names no validation step for any of this: no generator-level solvability checks and no automated reachability or seed tests. The Testing Agent's contract ("the changed feature or mission path") is written for a single authored path, not for a generator. This is a separate system with its own tooling cost, and it should either be scoped explicitly or cut to a small set of pre-baked, agent-checked layouts.

## 3. The Level Builder Agent is the critical path, and its tool integration and budget are not specified. MAJOR

**Passage:** Agent table: "this agent sources assets and builds the playable location". Contracts: "Blender and Unity deliverables, and findings from import, navigation, cover, lighting, and playable-path checks". Budget: "Level build and Unity integration pass for one mission | 160,000". "Existing specialist skills supply the procedures."

**Problem:** This agent carries the riskiest work in the pipeline. In Blender and Unity it has to assemble and adapt licensed assets, set up destructible cover and its durability, bake navigation, set up roof cutaways, and light the scene. The document calls it "the most visible output".

Yet the document never says how an agent actually drives the Unity Editor or Blender: editor scripting, batch mode, MCP bridge, or something else. It also never says how "playable-path checks" run in a turn-based game. That needs a scripted or headless playthrough harness, which the plan does not mention anywhere.

160k tokens for a whole build-and-integrate pass looks optimistic. The pass involves scene and prefab data, image references fed into context, and repeated tool round-trips, and a single failed check sends the work back to the specialist. The document admits the estimate is a first guess ("Actual usage from the first cycles will refine the estimate"). But it gives no fallback, such as Jim building levels by hand, for the case where the agent cannot meet the art quality bar. That bar is subjective and set by Jim's review.

## 4. The combat systems are tightly coupled and gameplay AI has no technical design. MAJOR

**Passage:** Movement "uses free positions along traversable routes" (not a grid). Other parts of the combat spec:
- Directional cover is "destructible" and "loses durability".
- Control cones are cut off by solid walls and "narrow with aim distance".
- Overwatch triggers on an enemy "entering the cone or spending AP within it" partway through its path, after which the target "can continue its movement".
- Smoke blocks sight, grenades follow lobbed arcs, and elevation gives views over lower obstacles.

Enemy behavior: "Enemies assess the battlefield through their role and orders. They seek useful firing positions, protection..."

**Problem:** Each of these is manageable alone. Together, on a gridless map with terrain that changes as cover is destroyed, they create a large interaction surface:
- Cover direction has to be computed for any point, not looked up per tile.
- Destruction invalidates cached cover, line of sight and navigation in the middle of a turn.
- Movement previews have to forecast reaction fire along a continuous path.
- Enemy AI has to score continuous candidate positions against all of the above.

The section titled "AI Architecture" is only about development agents. It contains no gameplay-AI design (utility scoring, influence maps, candidate-point sampling, performance budget per enemy turn). This is the system most likely to slip or ship weak, and the document does not mark it as a risk. If it is not already built, it alone can take up the eight weeks.

## 5. Customization, action cameras and cross-platform support add art and engineering scope the stated constraint ignores. MINOR

**Passage:** "Players can choose body type and height, face, skin tone, eye color, hair, outfit pieces, and available skins. Equipment and clothing fit across the body options." Also "Directed action shots bring the camera closer for targeting, movement, attacks, and important enemy actions". Platforms: "Windows and macOS".

**Problem:** The document correctly names art production as the biggest constraint. But its answer, mixing "licensed environment, character, equipment, and animation packs", runs straight into the customization promise:
- Gear from different vendors has to fit every body type and height, which means blend shapes or re-skinning per item.
- That fit has to hold across 9 kits plus worn kit pieces and helmet toggles.
- It also has to hold up in close action-camera framing, where clipping shows.

Directed action shots also need per-action camera logic that avoids obstruction on generated maps. macOS support means a second build and test target (Metal/URP, input differences), and no agent or check covers it. None of this appears in the constraint section or the token or credit plans.

**Suggested cut:** A single body type with tinted or swappable outfits, and macOS deferred, would remove most of this risk.

## Round 2 — Cross-examination

### CONFLICTS

**Systems Designer #2, #3, #5, and Adversarial QA #3: the proposed fixes add systems that the schedule cannot absorb.**
The Systems Designer is right that the economy has no numbers, that nothing carries over between missions, and that reinforcements have no model. But the suggested fixes are new features: recovery time for Downed operators, a side-mission refill rule, a late-game credit sink, alert levels or soft turn limits, and a full reinforcement model with trigger, wave size, interval and cap. Adversarial QA #3 adds a guaranteed-recruit floor and replaceable story equipment. Each one needs state, UI, save data and testing. My Round 1 Finding 1 is that nothing has been cut yet, so stacking more systems onto an uncut eight-week plan makes the blocking problem worse.

My position: each gap should be closed with the cheapest rule that removes the exploit, not with a new subsystem.
- **Bench (SD #3):** Say plainly that rotation is optional and the bench exists to recover from losses. The Systems Designer offers this as an acceptable alternative, and it is the only one that fits the schedule.
- **Reinforcements (SD #5):** Use a fixed rule per mission, such as N enemies every K turns from the authored approaches, until extraction. That is one data field per mission.
- **Economy (SD #2):** A numbers table costs nothing to write and should be added. A new late-game credit sink should be deferred.

**Narrative Critic #3: named, faced characters cost art and voice work.**
The Narrative Critic wants a named Nova leader, a handler, and a Directorate commander the player meets. Faced characters who appear in "directed shots" need bespoke or heavily customized character art, facial animation for dialogue, and fixed voice identities. That is the same art bottleneck the document calls "the largest technical constraint", and the customization system is already using it up. I am not disputing the story need. I am disputing the delivery method. Briefing text plus a single voiced handler, with an antagonist who exists through intercepted orders and is shown only on the final mission, gets most of the effect at a fraction of the cost. The Ring payoff (NC #1) can be handled in briefing copy and costs almost nothing, so I would prioritize it.

**Business Analyst #4: market positioning does not block feasibility in this context.**
The BA rates the lack of competitors and pricing as MAJOR, and also notes that it is unclear whether a commercial release is a goal. The only production frame the document gives is an eight-week course built on "the existing game through playable slices". Positioning against XCOM 2 or Midnight Suns changes nothing about what can be built in eight weeks. From my lens it is MINOR until the document says commercial release is a goal. BA #5 (two documents for two audiences) points at the more urgent fix: decide what is being judged.

### CONNECTIONS

**A. Nobody specified a test harness, so the Level Builder, Testing Agent and Balance Agent all rest on the same missing piece.** (my #3, BA #5, AQA #5, SD #4)
I raised the harness gap only in the context of the Level Builder's "playable-path checks". BA #5 found the same gap independently for the Balance and Testing agents. AQA #5 shows that without defined failure states the Testing Agent has "no expected result to check against". SD #4 notes the Balance Agent has no target across 16 branch paths. Taken together, every quality gate in the pipeline assumes an agent can load a scenario, run turns and read the outcome, and the document never says how. This is a single piece of infrastructure that has to exist before week 2 or the whole verification story fails. See Revisions.

**B. Fixing the failure exploit is cheap, but it exposes an unspecified save system.** (SD #1, PP #1, AQA #1, plus my lens)
Three colleagues found the same BLOCKING exploit: a full wipe costs less than losing one operator. The rule fix is trivial (Downed operators are lost on a wipe, or a wipe costs the reward). The harder problem is technical. PP #1 notes there are no save or reload rules. Without them, any loss rule can be beaten by quitting before the mission ends. Enforcing loss means saving during or at the end of a mission. On this design, a mid-mission save has to serialize:
- destroyed and partly damaged cover durability on a gridless map;
- grenade markers that are waiting to go off;
- Overwatch cones;
- Downed states;
- the generator seed that line 326 requires to persist.

None of that is scoped. The deterministic retry rule also means enemy AI and damage-range rolls must be seeded, or a "retained setup" will play out differently on each retry. The document should state the save model (for example, auto-save between missions only, with no mid-mission save) because that choice decides how expensive this is.

**C. Unbounded control effects make my combat-coupling risk worse.** (AQA #4 + my #4)
AQA #4's Suppressing Fire board lock and Field Orders AP loop are design holes, but they also hit the gameplay AI I flagged. On a gridless map the enemy AI must score candidate positions against suppression cones and Overwatch cones that change mid-turn as cover is destroyed. Once cones can permanently hard-stop movement, a reinforcement AI with no technical design will path into them every turn and look broken. Use limits on control abilities are a balance fix and also a requirement for keeping the AI tractable.

**D. Destructible objectives multiply the generator verification problem.** (AQA #5 + my #2, #4)
AQA #5 asks whether a frag can destroy a required console or cache. Combine that with my #2: on runtime-generated missions, the generator may put a required objective next to destructible cover or inside an Orbital Strike footprint. No agent ever sees that layout. That creates unwinnable missions that cannot be checked before release. Objectives need to be flagged indestructible engine-wide. That is a one-line rule and it removes a whole class of dead-end states.

**E. A curated mission pool fixes verification and farming together.** (BA #3, SD #2, AQA #3 + my #2)
BA #3 argues correctly that side missions cannot simply be cut, because the economy depends on them. That weakens my Round 1 suggestion. But SD #2 and AQA #3 both point out that an unlimited refill turns side missions into a grind that flattens loss and progression. A fixed, curated pool of pre-generated, agent-verified side missions handles all three problems: agents can verify every mission, the economy keeps its income source, and the pool caps farming. Runtime assembly can come back after week 8.

**F. Branch-locked kits are double the cost for half the use.** (SD #4, PP #4, BA #3 + my #1)
Three colleagues flag the Medic/Captain lockout from design, player and production angles. From my lens, it means building, animating, teaching and balancing a kit that roughly half of players never see, and then balancing later missions against both kit sets. The cheapest change that fixes all four reviews is for choice pairs to change rewards or timing but never lock a kit. That turns a 16-path balance matrix into a single target.

**G. The Warmech is a scope item with its own failure case.** (AQA #3 + my #1)
AQA asks what happens if the Warmech pilot is lost and a later mission depends on it. Technically the Warmech is also a large unit on free-position navigation. It needs separate nav-agent sizing, separate cover rules, its own animation set and its own camera framing. It appears in only a few operations. It is the clearest single cut candidate in the document, and cutting it also removes AQA's softlock.

### REVISIONS

- **Finding 3 (Level Builder): split it, and upgrade the harness part to BLOCKING.** With BA #5 and AQA #5 finding the same gap independently, the missing playthrough or test harness is not a Level Builder detail. It blocks every agent-based quality claim in the pipeline. BA #5 also suggests the pipeline may be the deliverable being graded. The token-budget part (160k per pass) stays MAJOR.
- **Finding 5 (customization / cameras / macOS): upgrade customization to MAJOR.** BA #2 adds what I underweighted: the document itself says appearance choices are "independent of combat effectiveness", so this is pure cost against the stated top constraint. It can be replaced by presets plus callsigns with little loss to the identity pillar. Action cameras and macOS stay MINOR.
- **Finding 2 (generated side missions): keep at MAJOR, revise the recommendation.** Because of BA #3, I withdraw "cut to pre-baked layouts" as a cut and restate it as Connection E: a curated, pre-verified pool that keeps the economy working.
- **New finding: the save and persistence model is unspecified. MAJOR.** See Connection B. Fixing the BLOCKING failure exploit that three colleagues found depends on it, and its cost depends on serializing destructible gridless state.
- **Finding 1 and Finding 4 unchanged.** BA #1 independently reached the same BLOCKING scope finding, and nothing in other reviews reduces the combat-AI risk. Connection C increases it.
