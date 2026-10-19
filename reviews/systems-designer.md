# Systems Designer — Round 1

Scope: core loop, progression, pacing across the campaign, difficulty curve, economy math. Line references are to `gdd.txt`.

---

## 1. Failing the mission costs less than losing one operator, so the main stakes can be bypassed. **BLOCKING**

**Source:** L308: "Any operator still outside the zone, including a Downed operator, is lost when the *successful* extraction concludes." L312: "If the whole squad is Downed, the mission fails. The operation remains available for another attempt." L326: "Each offered mission retains its setup across retries."

**Problem:** Permanent loss only happens on a *successful* extraction. A full-squad wipe is a failure, and failure has no stated cost: no operator loss, no campaign clock, no lost reward, no changed setup. Suppose one operator goes Downed and can't be reached. The best play is to let the other three go Downed too. That fails the mission, keeps all four operators and lets the player replay the same map with full knowledge of it. This undercuts the pitch ("bring your operators home", L7), the "Recruitment and loss" section (L254-258) and the memorial. The document also never says whether XP, credits or gear used on a failed attempt are kept or lost. That needs to be specified before the exploit can be scored.

**Needed:** A failure cost that is at least as bad as losing one operator (for example, Downed operators are captured or lost on a wipe, or a failed operation closes or escalates), plus a defined result for XP and credits on failure.

---

## 2. The economy has no numbers, no stated sinks and no limit on farming. **MAJOR**

**Source:** L402-412 (Credits, Progression pace). L119: "a completed side mission is removed from the current set of offers". L326-328 (generated side missions). The document never says whether time passes between missions or whether the side-mission pool is limited.

**Problem:** Credits and XP have no values. The section gives no rate per mission, no cost per training step, no length for a kit line and no Armoury prices. "A focused operator's development through a kit line by the later campaign" (L412) can't be checked. It doesn't say how many steps a line has or how much XP the story path gives. The structure has a bigger gap. Side missions come from a generator, and the document never says whether the offer list refills or whether anything advances while the player farms. If it refills and nothing advances, side missions become unlimited XP and credits. Then "Story progression is intended to outfit a standard squad" (L405) puts no ceiling on player power, and the authored difficulty curve (L292) can be flattened by grinding. The only credit sinks are extra equipment copies and skins. Those run out once the squad is equipped, so credits lose value in the back half of the campaign.

**Needed:** An economy table (income per mission type, cost per training step, steps per kit line, item prices). A rule for refilling side missions or limiting the pool. A credit sink that stays useful late in the campaign.

---

## 3. Nothing carries over between missions, so the roster bench has no systemic job. **MAJOR**

**Source:** L208: "Health recovers between missions." L240: "Gear uses refresh for the next mission." L256: "Recruits receive a training foundation based on story progress." L46 and L68 promise "a bench of specialists" and reasons to keep reserves.

**Problem:** Each mission starts from the same clean state. There's no injury, fatigue, recovery time or partial healing. Being Downed and then revived costs nothing after the mission. The only state that carries forward is permanent loss, and Finding 1 shows how to avoid that. The reasons the document gives for using the bench are mission fit and personal preference. Neither is pressure from the systems. XP is earned by deployed operators ("Mission experience contributes to training", L119), and recruits are brought up to the story baseline. So the strongest strategy is one heavily trained A-team plus a fresh recruit when a specialist kit is needed. Limits on equipment copies (L404) mainly matter across those same four operators. The roster, recruitment and equipment-copy systems sit alongside the core loop without being connected to it.

**Needed:** At least one cost that carries over and forces rotation (for example, recovery time for Downed or heavily damaged operators), or an explicit decision that rotation is cosmetic and the bench exists only for loss recovery.

---

## 4. Some branch choices permanently lock whole kits, but the difficulty curve and teaching content assume all kits exist. **MAJOR**

**Source:** L360: "Bring Them Home or Chain of Command — Restore a medical team or recover a field commander, *opening the corresponding support kit*." L358: "Long Reach or Heavy Hands — precision weapons or heavy fire support." L107 (the sample mission uses both Sniper and Medic). L206: "Medic training can improve the squad's options, including revival at a distance."

**Problem:** These choices are exclusive (L353: "closes the other opportunity"). The Medic/Captain branch definitely locks one kit. Long Reach/Heavy Hands appears to lock Sniper or Minigun. The document never says whether a closed kit can come back through side missions or random rewards. L408 limits random rewards to "discovered items", so probably not. Recovering Downed operators is central to whether loss happens. A player who chose Chain of Command has no Medic. That means no ranged Rescue and only medkits for healing, so every later extraction plays a different survival game. The difficulty section (L292) and the authored milestone missions (L346-347) don't say which kit set they're tuned for. They also don't say whether each mission must be beatable on all branch combinations. With 2^4 = 16 possible paths, the Balance Agent (L538) has no defined target.

**Needed:** A statement of which kits each branch locks and whether that's permanent. A minimum squad toolset that every path is guaranteed. A balance target for late missions under each branch, at least for the Medic/Captain split.

---

## 5. Mission pressure only starts after the objective, and reinforcement rules aren't defined. **MINOR** (becomes MAJOR if XP is awarded per kill)

**Source:** L84: "Completing the job often opens extraction and brings sustained reinforcement pressure." L290-292, L306. There are no turn limits, alert states or reinforcement timing anywhere in the document.

**Problem:** Before the objective, nothing pushes the player to keep moving. Defenders "value [their] assigned position" (L279), and Overwatch triggers on enemies spending AP inside a cone (L185). That makes slow, overwatch-heavy play the low-risk default during the approach, which works against the pacing goal in L332-334. After the objective, "sustained" reinforcements have no stated rate, cap, escalation or end condition. That leaves the extraction difficulty, which is the main test of whether the player "preserved a workable way out", unspecified. If XP or credits come from kills rather than completion (L119 is ambiguous), unlimited reinforcements become a farming source on top of Finding 2.

**Needed:** Decide whether the approach phase has pressure (alert level, patrol escalation or a soft turn limit). A reinforcement model (trigger, wave size, interval, cap). A clear statement that rewards come from objectives, not kills.

---

## Round 2 — Cross-examination

Colleague files read: narrative-critic, player-psychologist, feasibility-lead, adversarial-qa, business-analyst.

### Conflicts

**C1. Player Psychologist F2 (confirmation before abandoning Downed operators) makes my F1 exploit worse unless failure gets a cost first.** I agree the auto-abandon at L308 is a misclick trap. But adding a prompt such as "Extracting now will leave X behind. Confirm?" sends the player to a decision screen at the exact moment the wipe-reset (F1) is the better option. It works as a tooltip for the exploit. The fix order matters. Give failure a cost first (my F1), then add the prompt. If the prompt ships first, it teaches players to throw missions. The psychologist also lists missing save/reload rules under F1. I agree, and I'll go further: even with a wipe cost, free manual saves are a second bypass of the same stakes. Failure cost and save policy have to be designed together, or each one undoes the other.

**C2. Player Psychologist F5 (benched operators should earn XP so they don't "fall behind") conflicts with my F3.** The document already limits how far the bench falls behind. L256 brings recruits up to "a training foundation based on story progress", and L414 says a late specialist can "make productive choices for them immediately". The real problem runs the other way: benching costs too little, not too much. Shared XP would remove the last mechanical difference between deployed and reserve operators. Rotation would then be cosmetic, which is the outcome F3 warns about. I'd only accept bench XP alongside a carry-over cost such as recovery time, so the bench gets used because it has to be, not because it keeps pace for free.

**C3. Adversarial QA F4 (Field Orders AP loop): I agree with the gap, not the severity.** The document has one kit per operator (L222), and copies are limited (L398, L404). So two Captains in one squad take two Captain kit copies, two operators trained in that line, and two of the four squad slots. That's a large investment. More importantly, this is one case of my F2 problem: the document gives no numbers for anything. Whether Field Orders loops depends on a per-turn limit and an AP-granted versus AP-cost ratio that don't exist yet. Any first balance pass would add a once-per-turn limit. I'd rate the loop MINOR as a specific finding and fold it into "the document has no numbers" (F2). **Suppressing Fire board-lock** (also QA F4) is a different matter. It's MAJOR, and see Connection K3.

**C4. Feasibility Lead F2 and Business Analyst F3 both lean toward replacing the runtime generator with a fixed or pre-baked pool.** The analyst correctly says side missions are "load-bearing for the economy" (L406, L412), so they can't simply be cut. I'd go further and say a *finite* curated pool is better for the systems, not just cheaper to build. It closes the unlimited-farming hole in my F2 and gives the economy a ceiling that can be calculated. The danger is QA F3's "floor": with a finite pool and permanent loss, a player who loses operators late has limited ways to rebuild. So the scope cut is fine, but only together with a guaranteed-recruit floor (L256 mostly provides this) and a pool size worked out from the L412 progression target. Nobody should approve the cut without that calculation.

### Connections

**K1. Friendly fire turns F1 from a passive exploit into a one-click reset (my F1 + QA F2).** L157 says area attacks affect "damageable units within their blast, including friendly operators". L388 gives area attacks such as Orbital Strike and Airburst. The player doesn't need to wait for the enemy to Down the rest of the squad. They can frag their own cluster and force L312's failure-with-retry. QA F2 asks whether a Downed operator can take more damage. That matters here too. If Downed operators can't be killed, self-bombing is a risk-free reset button. If they can, friendly fire becomes the only route to permanent death outside L308, which no other system expects. In both cases the Downed damage rule and the failure-cost rule are one design decision.

**K2. Loss has no weight in the systems or the story (my F3 + Narrative Critic F4 + L256).** The narrative critic shows that no authored content reacts to a death. From my side, the systems don't make loss hurt much either. A replacement arrives at the story-baseline training level (L256), gear and health reset (L208, L240), and the lost operator's equipment is never said to be lost with them. What a death actually removes is the XP spent above baseline, plus the player's own attachment. So the "bring them home" pillar sits on a mechanical cost that shrinks as the campaign goes on: the higher the baseline, the cheaper a death. Combined with F1's free wipe, losing an operator is either avoidable or cheap. It's never expensive in the way the pitch promises. Fix the systems side (catch-up below baseline, loss of carried gear, or a recruitment delay) alongside the narrative side. Narrative acknowledgement alone can't support stakes that the systems don't impose.

**K3. Extraction is the only pacing pressure, and the document both contradicts it and gives a counter to it (my F5 + QA F1 + QA F4).** My F5 says approach-phase pressure is missing, so everything depends on extraction. QA F1 shows that the rules for how extraction ends contradict each other (L117 says revival is required; L308 says Downed operators are abandoned automatically). QA F4 shows that Suppressing Fire has no duration or cap and can hold the fixed reinforcement approaches (L290). Together these mean the one phase that carries the mission's tension has unclear ending rules and an uncapped tool that can shut it off. Feasibility Lead F4 adds the third part. With no gameplay-AI design, the likeliest weak-AI result is the defender-holds-position default (L278), which makes the approach phase even more passive. **I'm upgrading F5 to MAJOR** (see below).

**K4. A branch-locked kit can be lost twice (my F4 + QA F3 + L398).** L360 opens either the Medic or the Captain kit, and L398 says an unlock "*can*" make Armoury copies available, which implies some don't. If the only Medic kit belongs to an operator who is lost, and no Armoury copy exists, the player has lost the Medic for good. The branch didn't take it away. One extraction did. Then every later mission is played without the tool that makes Downed recovery possible. That feeds back into more losses. It's a death spiral the document never mentions. A player-psychology fix that only previews the branch choice (Psychologist F4) won't catch it. The rule has to be: kits opened by a branch are always buyable once opened.

**K5. Business Analyst F3 / Feasibility Lead F1 (the 16-path test matrix) give my F4 a production cost.** I raised 2^4 combinations as a balance target that isn't defined. The analysts show it's also a testing cost the eight-week plan can't absorb. That supports my proposed fix of a guaranteed minimum toolset for every path. It reduces the number of combinations that need tuning to 2 (Medic vs Captain). The other three pairs become changes in the amount of gear rather than which kits exist, and those can be tested by tuning numbers rather than replaying the campaign.

### Revisions

- **F1: stays BLOCKING, with a wider scope.** Three colleagues found the same thing on their own (Psychologist F1, Narrative F4, QA F1), so this is the board's most robust finding. I'm adding the friendly-fire enabler (K1), the save-policy dependency (C1), and QA's point that "secure the location" milestones (L310) have no extraction step, so the loss rule doesn't cover them at all.
- **F2: stays MAJOR.** I'm absorbing QA F4's AP loop as an example of it (C3). I'm adding the condition that any move to a finite side-mission pool must come with a calculation of the pool size (C4).
- **F3: stays MAJOR, reframed.** The finding is now "loss and rotation have almost no mechanical cost" (K2), not only "the bench has no job". L256's catch-up rule is the main cause of both.
- **F4: stays MAJOR.** I'm adding the lose-it-twice death spiral (K4) and a firm fix: kits opened by a branch are always buyable once opened.
- **F5: upgraded MINOR to MAJOR.** Combined with QA's Suppressing Fire board-lock and the L117/L308 contradiction, the mission's only pressure phase is undefined and can be shut off (K3).
- **F5, partial withdrawal:** L404 says "Credits come from successful operations and their applicable rewards", so credits per kill is ruled out. Only the XP-source question (L119) is still open, so the farming condition now applies to XP only.
