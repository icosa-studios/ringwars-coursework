# Systems Designer — Round 1

Scope: core loop, progression structure, campaign pacing, difficulty curve, resource and economy math.

---

## 1. The loss rules reward failing on purpose (wiping beats a costly win)

**Severity: BLOCKING**

**Source:** Mission outcomes table (lines 324-327) and Extraction rules (line 314).

- On a **main story mission**, a full wipe means "Game Over," but "Trying again returns to before the failed attempt, where the player can revise loadouts, change the squad..." Nothing is lost.
- On the same mission, a **partial success** is permanent. Under line 314, "Any operator still outside the zone, including a Downed operator, is lost when the successful extraction concludes."

So when a story mission goes badly (one or two operators Downed and out of reach), the best play is to let the whole squad go down. A wipe gives a free reset. A hard-fought extraction keeps the deaths. The punishment runs backwards: the worse result costs nothing, and the better result costs operators for good. That undercuts the pillar "You will lose good people" (line 70) and the "bring your operators home" premise (line 7). The game has no other source of tension on story missions, because losses are the stakes.

Side missions have the opposite problem. A Downed operator who is abandoned at extraction is **100% lost**. In a full wipe, each operator has a **45% capture** chance and can be rescued later. So the player is pushed to keep a doomed squad in the fight and avoid a partial extraction. The two loss paths were clearly designed separately and were never compared against each other.

**Needed:** One loss model that makes extracting at least as good as wiping in every case. Options:
- Story-mission retries also roll back after costly wins (a checkpoint the player chooses), or
- Story wipes carry a real carry-over cost, and
- On side missions, abandoned Downed operators use the same capture roll as a wipe.

---

## 2. Roster attrition has no floor, and side-mission supply is undefined. The campaign either becomes a grind or a death spiral

**Severity: MAJOR**

**Source:** Recruitment (line 262: "Campaign milestones expand the roster"; line 264: "Recruitment fills available roster space"), Mission outcomes (line 320: "Resolved operations leave the available mission set"), and Return (line 121: "a completed side mission is removed from the current set of offers").

Operators are lost permanently or captured. Recruitment happens only at milestones. Rescue missions only "may" exist (line 329). The document never says:

- whether generated side missions **replenish**, how fast, or whether any clock limits them;
- what happens if the roster falls **below 4** before a story mission that requires a standard squad;
- whether a lost or captured operator's **equipment** is lost too. This matters because owned copies are a scarce resource (line 427: "making the number of available copies relevant").

Each answer breaks something:
- If side missions replenish without limit and nothing costs time, XP and credits have no ceiling. The player can grind past every story difficulty step, and "Story progression is intended to outfit a standard squad" (line 428) stops being a real tuning target.
- If side missions are finite, a run of losses can leave the player short of operators or gear with no recovery path. Story-mission rollback (Finding 1) only restores the state from just before the attempt, and that state is already depleted. The player could have a soft-locked campaign with no way of knowing.

**Needed:** State the side-mission generation rule (count, refresh trigger, expiry), a minimum roster guarantee or emergency recruitment, and the equipment-on-loss rule.

---

## 3. The economy has no numbers, so the stated pacing goals can't be built or checked

**Severity: MAJOR**

**Source:** Progression and economy (lines 403-437), especially Progression pace (line 435: "The story path should support a focused operator's development through a kit line by the later campaign") and Credits (lines 427-431).

The section names every currency (XP, credits, equipment copies, skins) and every sink (training steps, Armoury purchases) but gives no amounts. Missing:

- XP per mission, and how it is split. Per deployed operator? Shared? Do Downed or lost operators earn any? How much does an optional objective add?
- How many steps a kit line has, and what each step costs.
- Credit income per story and side mission, and equipment prices.
- How many copies of each item the story grants. Without this, "outfit a standard squad" can't be checked.
- How recruits' "training foundation based on story progress" (line 262) compares with a veteran's earned XP. This decides whether veterans are actually worth more than fresh recruits (line 437) or whether catch-up flattens the difference.

Without these numbers, nothing defines the difficulty curve, which "grows through enemy composition..." (line 298), relative to player power. The Technical Strategy section claims "content and economy validation" tooling (line 612) and a Balance Agent with before-and-after observations (line 643), but the design gives that tooling no target to validate against. Also, credits have almost no sink besides extra copies and cosmetics. After the squad is equipped, credits likely lose their purpose by mid-campaign, and the document has nothing to catch that.

**Needed:** A first economy table covering income and cost per mission, the kit-line length and cost curve, the per-act power target, and a stated target for the number of side missions per act.

---

## 4. The mutually exclusive kit choices collide with the cut list, and the kit-unlock rules are unclear

**Severity: MAJOR**

**Source:** Mission choices table (lines 374-379), Course delivery table (line 606: "Kits to cut if needed: Warmech, Medic, and Captain"), Kits table (lines 230-240), and Experience and kit training (line 405: "ordered training steps within unlocked kit lines").

- The last choice, **Bring Them Home or Chain of Command**, exists to open the Medic or Captain kit. **Both** are on the cut list. If they are cut, that choice offers two empty rewards, and a story branch loses its systemic reason to exist. The document says "affected missions remain playable" (line 608), but it doesn't address a choice whose only payoff has been removed.
- **Long Reach or Heavy Hands** splits Sniper and Minigun. Every later encounter therefore has to be beatable both without the Sniper and without the Minigun. Yet the example operation (line 109) and the Shock Sword "flank" design both assume a Sniper is available. The design doesn't say whether the unchosen kit can still be acquired later, for example through "random equipment rewards" (line 431), which "draw from appropriate discovered items." If it can, the exclusive choice is weak. If it can't, difficulty tuning needs two branches.
- The Medic overlaps heavily with shared systems. **Any** operator can Revive (line 210), and medkits are available to everyone from the first squad mission. The Medic adds Stim and ranged Rescue on top. So the Medic branch of the final choice is fairly weak compared with a whole command kit, which tilts that choice toward the Captain.
- The document never says how the **Grenade Launcher** and **Pistol** kits are acquired.
- "Unlocked kit lines" doesn't say whether unlocking applies to the **whole campaign** or to **each operator**, or whether switching kits keeps training. That decides whether "training across kits" (line 411) is a real strategy or a trap.

**Needed:** A table of every kit's unlock source, a scope rule for unlocks and training, and a fallback reward for each choice in case its kit is cut.

---

## 5. Missions have no failure conditions other than a wipe, and secure-type missions don't say how they resolve

**Severity: MAJOR**

**Source:** Mission outcomes (line 322: "A full-squad wipe means every deployed operator is Downed"), Extraction (lines 312-316), Objective structure (line 304: escort, hold a position), and Reinforcement pressure (lines 294-298).

The only failure state the document defines is a full wipe. So it doesn't answer:

- what happens when an **escort** target dies, or a **hold** position falls;
- whether the squad can **abort** before finishing the objective, and with what result (does the side mission close? do Downed operators count as lost?);
- how **secure-the-location** missions (line 316) treat Downed operators at the end, since the extraction-zone rule doesn't apply there;
- whether reinforcement pressure has a cap or a schedule. "Sustained reinforcement pressure" (line 86) with no limit and no timer means a slow but careful squad faces endless waves, while no timer at all means turtling is always safe. The document gives neither.

These rules set the mission's difficulty curve. The pacing section's "approach, commitment, objective pressure, and resolution" (line 351) depends on objective pressure escalating at a known rate, but no turn limit, wave schedule, or alarm state is specified. That also leaves the "optional cache vs. withdrawal" tradeoff (lines 117, 308) without anything to measure the cost of the detour.

**Needed:** For each objective type, a list of failure conditions, an abort rule, the Downed-operator resolution for secure missions, and a reinforcement model (trigger, cadence, cap) that turns extra turns into a measurable cost.

---

## Round 2 — Cross-examination

### CONFLICTS

**C1. Business Analyst #3 ("side missions are a second game", cuttable): I disagree. Side missions carry weight in the loss model.**
The Analyst reads line 429 ("Story progression is intended to outfit a standard squad") as saying side missions are optional breadth that could be cut. But the only recovery path the document gives after a story-mission Game Over is in the same table cell: "revise loadouts, change the squad, or **complete available side missions** before attempting the story operation" (line 326). Side missions are the one way to rebuild between failed story attempts. They also hold the whole capture/rescue loop (lines 327-329), which is the only thing that softens permanent loss. If they are cut, a depleted roster has nowhere to go, and Game Over becomes a hard wall. That is the death spiral that Player Psychologist #1, Adversarial QA #1 and my #2 all describe, with the one partial exit taken away. My position is that side missions can be **reduced** (one job type, a fixed small pool per act) but not cut unless the loss model is redesigned at the same time. The Analyst's scope concern is real. The proposed fix moves the cost into a broken campaign.

**C2. Player Psychologist #2 (warn before Downed operators are lost at extraction): a warning makes my Finding 1 exploit easier to see.**
I agree the silent loss is a readability bug. But a mandatory "these 3 operators will be lost" prompt on a story mission tells the player exactly when to stop moving into the zone and let the last operator go down for a free retry. The warning fixes the feeling of unfairness and makes the incentive problem worse. The order matters: the loss model has to be fixed first (extracting must never be worse than wiping), and then the warning becomes good UX. If the warning ships alone, the exploit becomes a feature everyone learns.

**C3. Player Psychologist #5 rates the exclusive kit choices MINOR and treats them as an information problem. I keep them at MAJOR, for systems reasons.**
Previewing the branch helps with buyer's remorse. It does not fix the tuning cost. Each exclusive kit choice splits every later encounter into versions that must be balanced with or without that kit. The Psychologist suggests letting the locked-out option be bought later in the Armoury. That empties the choice, because line 421 ties Armoury availability to the unlock itself ("An unlock can provide equipment and make additional copies available in the Armoury"). The Armoury follows the lockout; it can't be used to get around it. Either the choice is real and needs branch-aware balance, or it isn't real and should be reframed as a timing choice (which kit you get first).

**C4. Feasibility #3 and Business Analyst #2 treat the Warmech cut as one of the worst. From the systems side it is the cheapest of the three.**
The kits table calls the Warmech "a supplied powered combat suit for selected heavy assault operations" (line 240). Line 421 says "Mission-supplied equipment supports specific scenarios, including the Warmech assault." It sits outside the owned-equipment economy, kit training and the choice table. Cutting it costs one Act IV mission and its art (I accept the Feasibility Lead's rig cost and the Narrative Critic's point about "captured machinery"), but nothing in progression collapses. Medic and Captain are the opposite case: each is the whole reward of a story choice, and each is a kit line that XP flows into. If something must go, the cut-list order should be **Warmech first, then one of Medic or Captain together with a redesign of the final choice, never both.**

**C5. Business Analyst #4 calls it a "paid-skin Armoury", but the document doesn't support that.**
Line 389 and line 427 describe skins as bought with **credits**, an in-game currency earned from operations, and line 431 says skins can also be "earned through achievements." Nothing mentions real money. The DLC hook is real, but the Armoury is not monetization. This affects the Analyst's suggestion to cut skin purchases. Skins are one of only **two** credit sinks the document names, along with extra equipment copies. Cutting them makes my #3 worse: once the squad is equipped, credits have nothing to buy. Any cut there needs a replacement sink.

### CONNECTIONS

**X1. Adversarial QA #5 (Suppressing Fire can block movement) + my #5 (wipe is the only failure state) = missions that can't be won but can't be lost.**
QA asks whether an enemy Suppressing Fire cone over the only route to extraction can stop an operator every turn. Combine that with my #5: reinforcements have no stated cap and wipe is the only defined failure. The squad can then be pinned outside the zone with no way to extract, no defined abort, and no loss trigger unless the player feeds operators into fire. That is a soft-lock inside a single mission. It is also another case of Finding 1, where the player's only way out is to wipe on purpose. The symmetric control-cone rules QA wants and the reinforcement cap and abort rule I want need to be specified together.

**X2. Adversarial QA #2 (quitting mid-mission) shows that my Finding 1's side-mission analysis may not matter.**
I argued that side missions push the player to keep a doomed squad fighting rather than extract partially. QA points out the document has no save or quit rule. If quitting mid-mission reverts to HQ, then on side missions too the best play is to quit when things go badly, and "Each mission is played once" (line 320) can't be enforced. So the inverted incentive covers the **whole** loss model, not just story missions. The fix has to include a save rule (an autosave at deployment that is overwritten on commit, or an ironman-style lock). Otherwise every loss tuning number, including the 45% capture rate, can simply be avoided.

**X3. Feasibility #1 / Business Analyst #1 (22 missions over 16 cycles) + my #4 (exclusive choices split the balance) = the balance budget is undercounted, not only the build budget.**
Both colleagues count the **build** cost of 8 branch missions. Under my lens, the bigger cost comes after the branches. Each choice changes the kits available for every later mission, so four binary choices produce up to 16 equipment states going into Act IV. The Balance Agent's per-mission budget (line 643) assumes one player-power state per mission. The Feasibility Lead suggests that branch pairs share a map with different rewards. That fixes the build cost and leaves the downstream balance cost untouched, because the reward difference is the thing that branches. A cheap systemic fix is to reconverge: make the later kit available to everyone one act later, so the branches differ only for one act.

**X4. Narrative Critic #4 (the choices have no moral consequence) + my lens = the "Open the Cages" branch also has no mechanical output.**
The Critic says rescuing civilians has no story payoff. From the systems side it is worse. Every other branch names a reward category ("precision weapons", "heavy fire support", "mobility equipment", "protective equipment", a kit). "Rescue civilians and skilled workers" (line 376) names people with no stated effect: no recruits, no roster slots, no Armoury unlocks, no XP foundation. The opposite branch gets "local weapons production." As written, the moral choice is also the empty choice, so a player optimizing systems will always leave people in the cages. One fix serves both lenses: rescued workers could expand roster space or raise the recruit training foundation (line 262). That ties the choice into the roster-floor problem in my #2 and gives the Act II character something to react to.

**X5. Adversarial QA #4 / Feasibility #4 (NPC allies in the finale) + my Finding 1 = the finale can be retried until the outcome is acceptable.**
Their Last Order is a main story mission, so a wipe returns the player to "before the failed attempt" (line 326). The player's choice "dooms one of those other characters" (Act IV section), and that outcome is recorded for DLC. Since the doc defines no failure besides a wipe and no rule for scripted deaths during combat, a player who dislikes how the scripted deaths play out can wipe and retry. The finale's one consequential branch can be retried at will. Also, if NPC allies count as "deployed operators" in the wipe definition (line 322), the wipe condition gets harder to reach with 8 units, and the AP economy is tuned for 4 (line 220). The finale's difficulty can't be set until both questions are answered.

**X6. Narrative Critic #2 / Player Psychologist #4 (the player's identity) + my #2 = a protected avatar is a roster floor of one.**
If the Breakout prisoner is a protected avatar, as the Psychologist offers as an option, that operator can't be lost, which partly fixes the roster floor. But it creates an economy problem: the one operator who can't die is the safest place to invest XP, and everyone else becomes expendable. That works against line 437 ("Experienced operators retain the value of their additional investment"). If the avatar can die, the Act characters lose who they are reacting to. In either case the identity decision changes the loss economy and has to be made before the numbers in my #3 can be tuned.

### REVISIONS

- **Finding 2: upgrade from MAJOR to BLOCKING.** Adversarial QA (#1) and the Player Psychologist (#1) reached the same death-spiral result independently, and C1 shows that the only partial exit (side missions) is on a colleague's cut list. Line 220 gives "4 operators for a standard mission" and never says whether fewer can deploy. Together with no roster floor, this is a reachable soft-lock. One correction: I wrote "a story mission that *requires* a standard squad". The document says "standard," not "required." The missing rule is the problem.
- **Finding 1: keep BLOCKING and widen the scope.** Based on X2, I'm adding the missing save/quit rule. Without it the inversion covers side missions as well as story missions. Adversarial QA (#2) found the same story-mission inversion independently. I'm withdrawing my claim that side missions push the player "to keep a doomed squad in the fight", because without a save rule I can't say what side missions push the player toward.
- **Finding 4: narrow the scope and keep MAJOR.** The point about cut kits leaving the choice empty is now covered by four reviewers, so I'm leaving it to them. My distinct points are the cost of tuning across branches (X3) and the unclear scope of kit unlocks. I'm **downgrading** the point that the Medic is weak compared with the Captain to a MINOR note. It is a balance guess, and without numbers (my own #3) I can't support it.
- **Finding 5: keep MAJOR, with a note on how it combines with other findings.** On its own it is a spec gap. Combined with QA #5 (X1), it creates a soft-lock inside a single mission.
- **Finding 3: unchanged.** No colleague disputed it. The Feasibility Lead's #5 (the token estimates are not checked against actual usage) points to the same problem in production: the plan has no measurements to tune against.
