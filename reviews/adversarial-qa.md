# Adversarial QA — Round 1

## 1. Extraction, Downed, and failure rules contradict each other, and failing a mission beats succeeding — BLOCKING

**Problem.** Three passages give conflicting rules for when a mission ends and what happens to Downed operators.

- Example of play (line 117): "If an operator is Downed, the player **must** create the time and access needed to revive them before continuing the extraction. The mission concludes when the squad has reached the extraction zone or the player has explicitly committed to leaving an operator behind."
- Extraction (line 308): the explicit leave-behind commitment applies only to a **standing** operator. "The mission concludes when all standing operators are accounted for... Any operator still outside the zone, including a Downed operator, is lost when the successful extraction concludes."
- Failure (line 312): "If the whole squad is Downed, the mission fails. The operation remains available for another attempt."

Line 117 says revival is required. Line 308 says the mission ends automatically and the Downed operator is lost. Under line 308, a Downed operator never needs an explicit decision. As soon as the last standing operator steps into the zone, the mission ends and the Downed teammate is permanently lost with no confirmation. A Medic who paths through the zone on the way to a revive could trigger this by accident.

**Exploit.** The document never says operators are lost, or that rewards are kept, on a full-squad wipe. If a wipe costs nothing permanent, the best play whenever one operator is Downed far from extraction is to let the rest of the squad go down too. The player loses no one, the mission stays available, and line 326 keeps generated mission layouts the same across retries. A wipe then works as a free scouting run. The player can also take the optional cache, wipe, and retry, with no rule saying whether that reward is kept.

**Also unhandled:**
- Can an extracted operator leave the zone again?
- Does a squad with 1 extracted operator and 3 Downed count as "the whole squad Downed"?
- What happens to Downed operators in "secure the location" missions (line 310), which have no extraction step? Line 208 makes bringing someone home depend on "a successful withdrawal."

## 2. The Downed state has no rules for further damage, enemy targeting, or forced movement — MAJOR

**Source.** Lines 204-208 define Downed only as "needs revival to stand and act again." Line 157 says area attacks hit "damageable units... including friendly operators." Line 278 says enemies seek "opportunities to damage or Down operators." Line 284 says enemy grenades explode next enemy turn with a "response window... to reposition."

**Unanswered questions:**
- Can a Downed operator take more damage or be killed outright, for example by a frag, Airburst, Orbital Strike, or enemy grenade?
- Will enemy AI focus on Downed operators to finish them, or ignore them?
- A Downed operator inside a grenade marker cannot use the response window. Can they be moved or carried?
- Does Revive trigger enemy Overwatch? Line 185 says "spending AP within" a cone triggers it, which turns every revive inside a cone into a forced trade.
- How much health does a revived operator have? Can they act on the same turn? Can they be Downed and revived without limit within one mission?

Without these rules, permanent loss (line 258) depends on behavior nobody has specified. Because Orbital Strike hits friendlies, it may also be able to kill a Downed teammate permanently.

## 3. Permanent losses can leave the roster unable to field a squad, and there is no recovery rule — MAJOR

**Source.** Lost operators leave the roster (line 258). "Campaign milestones expand the roster" (line 256). Recruitment "fills the available roster space," but nothing says when or how. Gear is "allocated to operators" (line 404). An unlock "**can**" provide extra Armoury copies (line 398), which means some items may not.

**Unhandled:**
- Is there a minimum squad size? Can the player deploy fewer than 4?
- Can the player recruit between milestones, or only at them? After heavy losses in Act 1 (Dead Air, Sever the Ring), can the player still field 4?
- What happens to equipment allocated to a lost operator? If a story reward with a single copy is lost with its carrier (the Shock Sword from Dead Air, or a choice reward like Long Reach / Heavy Hands), can it be bought again?
- The Warmech is "supplied" for specific operations (line 234). What happens if its pilot is lost during Keys to the Giants, and Break the Bastion depends on it?

**Opposite risk.** Side missions appear to be unlimited and generated (line 326). Nothing in the document applies time pressure or a campaign clock. That makes grinding side missions the obvious recovery path, which undercuts both the loss consequence and the progression pace in lines 410-414. As written, the design either softlocks the player or makes losses trivial. It needs a stated floor, such as guaranteed recruits or replaceable story equipment, and a stated ceiling, such as a limit on side-mission availability.

## 4. AP-granting and movement-control abilities have no stated limits, so they can loop or lock the board — MAJOR

**Source.**
- Field Orders "grants another operator AP" (line 388), and AP-granting abilities "extend a maneuver" (line 129).
- Training "across kits" is supported (line 392), and equipment copies can be bought (line 398), so several Captains in one squad is legal.
- Suppressing Fire works by "stopping enemies moving through its cone" (line 187).
- Reinforcements arrive through a small number of fixed "exterior approaches" (line 290).

**Exploits:**
- **AP loop.** Two or more Captains can pass Field Orders back and forth. If the AP granted is at least the AP cost, or the ability is not limited to once per turn or per target, the squad gets unlimited actions in Our Turn. Line 157 mentions "use limits" for attacks but defines none for Field Orders.
- **Board lock.** No duration, number of uses, or per-enemy cap is given for Suppressing Fire. A Minigun posted on each reinforcement approach can hard-stop every arriving enemy every turn, which removes the extraction-phase pressure the design depends on.
- **Enemy use against the player.** "Both the squad and the enemy can use control" (line 183). If an enemy stops a player's movement inside a grenade marker, the line 284 response window becomes unavoidable damage. That contradicts the readability pillar (line 62).

## 5. Objective and non-combatant units have no damage or failure rules — MAJOR

**Source.** Objectives include "accessing a console, destroying controls... taking supplies, rescuing people, escorting them" (line 298). Destructible cover loses durability to "fire" and "explosion" (line 169). Area attacks hit "damageable units" (line 157). Enemy behavior (lines 278-280) mentions only operators as targets. The only failure condition (line 312) is a full-squad wipe.

**Unhandled:**
- Can the player's own frag, Airburst, or Orbital Strike destroy a console that has to be accessed, or the supplies or cache that have to be taken? If so, is the mission failed, or stuck with no way to finish?
- What happens if an escorted or rescued person is Downed or killed? Can enemies target them? If they die, does the mission fail, continue with a penalty, or does the person count as "lost" like an operator?
- For holding missions, what does losing the position mean if enemies take the controls?
- If the stockpile itself is destroyed by stray explosives before charges are planted, is the sabotage complete?

Without these rules, the only stated way to fail is a full wipe. A player can ignore escort and rescue NPCs entirely, or cause dead-end mission states that the Testing Agent has no expected result to check against (line 585).

## Round 2 — Cross-examination

### Conflicts

**Systems Designer #1 (failure costs less than losing one operator): the proposed fix creates a new fail state.** We agree on the exploit, and so do Player Psychologist #1 and Narrative Critic #4. Four reviewers reached it independently, which makes it the strongest finding on the board. My disagreement is with the remedy. Systems proposes that "Downed operators are captured or lost on a wipe." If that rule is added without anything else, one wipe loses all four operators. The document gives no minimum squad size, no recruitment timing outside "campaign milestones" (line 256), and no rule for single-copy story equipment (my #3). An Act 1 wipe on Dead Air or Sever the Ring could leave a roster of zero with the next milestone locked behind a mission the player can't staff. The case is worse in Breakout, where the squad is "a single prisoner" (line 214): under Systems' rule, any failure there would end the campaign. A wipe penalty can't ship without the roster floor I asked for in #3. The two findings have to be fixed together. If the penalty is fixed alone, a soft exploit becomes a hard softlock.

**Player Psychologist #2 (automatic abandonment through misclicks): the cause is in the rules, not the input.** Psych pins much of the risk on Space being shared between confirm and hold-to-end-turn (lines 498, 505). Line 507 already addresses that: "Input context distinguishes... an action confirmation from End Turn." The input argument is the weaker half of the finding. The defect I care about is in line 308 itself. A correctly entered, deliberate move by the last standing operator into the zone ends the mission and abandons every Downed teammate. That includes a move that only passes through the zone on the way to a revive, and a move cut short when Overwatch interrupts it mid-path (line 185, "can continue its movement"). An undo button doesn't solve that. The fix is the confirmation rule that line 117 already implies. Line 308 needs to require the same explicit commitment for Downed operators that it requires for standing ones.

**Systems Designer #5 (mission pressure, rated MINOR): I'd rate it MAJOR now, without the "if XP per kill" condition.** Systems treats unbounded reinforcements mainly as a pacing issue. My #4 shows the other direction. Reinforcements arrive through a few fixed approaches (line 290), and Suppressing Fire stops movement through its cone with no stated limit (line 187). An uncapped reinforcement stream therefore isn't pressure. It's a queue the player can freeze in place. The extraction phase, which Systems calls "the main test," can be either endless or trivial depending on two numbers the document never gives. Neither outcome needs kill-based XP.

**Feasibility #2 vs. Business Analyst #3 (cut the generator, or keep it because it carries the economy).** Feasibility says to cut to pre-baked layouts. BA says side missions are "load-bearing for the economy" (line 406), so the generator can't simply be cut. From the QA side, either answer is acceptable, but the roster recovery path depends on which is chosen. My #3 found that side missions are the only realistic way to rebuild after losses. A small fixed pool makes the softlock risk real once it runs out. An unlimited generator turns loss into grinding. Whatever is decided about the generator also has to settle the roster floor and ceiling. The two decisions can't be made separately.

### Connections

**A. Generator plus retained setup gives defects a fixed seed (Feasibility #2, BA #3, my #5).** Feasibility shows that no agent ever sees the specific mission a player gets. Line 326 says "each offered mission retains its setup across retries." Line 119 says only a *completed* side mission leaves the offer list. Put together, a generated site with a break gets locked in place: extraction unreachable across a block seam, an objective console embedded in destructible cover that a grenade can delete, a reinforcement approach that spawns inside the play area. The broken site persists across every retry and can't be completed or cleared. Nothing says the player can decline or reroll an offer. Retention is meant to be a learning feature. Without a validation step it guarantees the player keeps hitting the same bug. At minimum, the document needs an abandon or reroll rule for offers.

**B. Failure returns the player to "mission choices", so both branches can be scouted for free (Systems #4, Psych #4, Narrative #5, my #1).** Line 312 says failure "returns the player to the preparation and **mission choices** needed for a new attempt." For an exclusive pair (line 353), the document doesn't say whether a failed attempt at one side keeps the other open. If it does, a player can deliberately wipe on Bring Them Home to see its layout, then switch to Chain of Command, or the reverse. All three colleagues treat the kit lockout as blind and permanent. Combined with my wipe exploit, it is neither. The blind choice Psych worries about can be undone by losing on purpose. Whether that's acceptable is a design call, but right now the document hasn't decided it.

**C. The Medic/Captain branch decides which of my exploits is live (Systems #4, Psych #4, my #2 and #4).** Chain of Command opens the Captain kit, and Field Orders (line 388) is the AP-loop risk in my #4. Bring Them Home opens the Medic, and ranged Rescue reduces the Downed-state gaps in my #2. The two balance targets Systems asks for are therefore different exploit surfaces, not just different difficulty levels. The Captain path has a possible infinite-action bug plus a harder Downed problem: no ranged revive, so more Downed operators are left in the open. That raises the incentive to wipe on purpose under my #1. The Balance Agent needs per-branch test cases for these specific interactions, not only a general difficulty target.

**D. Systems #3 (nothing carries over) plus my #2: revives can be repeated without limit at zero cost.** Downed status has no per-mission cap that I could find, health "recovers between missions" (line 208), and nothing carries forward. So within a mission the only cost of being Downed is the AP spent on the revive. An operator who can be Downed and revived without limit is in practice immortal while a Medic stands. The permanent-loss pillar then depends only on the extraction-zone edge case in line 308. Systems' carryover proposal (recovery time after being Downed) would also close this.

**E. Narrative #2 (who is the player?) is also an undefined fail state.** Line 422 says "the player becomes one of its skilled operators." If that operator is a roster member, line 258 lets them be permanently lost. The document never says whether losing the player's own operator ends the campaign, removes the viewpoint character, or is just another memorial entry. Narrative treats this as a framing problem. For QA it is a missing game-over condition.

**F. Narrative #5 (Open the Cages) depends on escort rules that don't exist (my #5).** The most morally weighted choice is a civilian rescue. My #5 shows that rescued and escorted people have no damage, death, or failure rules. If civilians can't die, the rescue carries no tension. If they can die but their deaths don't fail the mission, the player can let them die at no cost. Either way, the moral weight Narrative wants is undercut by the mechanics before writing can address it.

### Revisions

- **#1 stays BLOCKING.** I've narrowed the misclick sub-point (see the Psych conflict above). The rule defect stands on its own. I'm adding Connection B, where the wipe exploit also lets the player get around exclusive branch locks.
- **#3: MAJOR becomes BLOCKING if any wipe penalty is adopted.** On its own it's MAJOR. It becomes the blocker the moment Systems' #1 fix, or any similar fix, goes in. The Breakout single-prisoner case makes this concrete.
- **#4: kept MAJOR, but I'm narrowing it.** The AP loop only applies on the Chain of Command path, or if the Captain kit can be trained across through some other route. I assumed multiple Captains were always available. Line 360 makes the Captain branch-gated, so I overstated the reach. I'm downgrading the "enemy control pins you in a grenade marker" sub-point to MINOR. It's a plausible bad interaction, but the response window is a readability tuning issue, not a broken rule. The Suppressing Fire board lock is still MAJOR, now reinforced by Systems #5.
- **#5 stays MAJOR, with the scope widened to generated missions.** Connection A shows that objective destruction on a generated site, with setup retained across retries, can produce a repeatable dead-end offer rather than a single bad run.
