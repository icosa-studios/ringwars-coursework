# Adversarial QA — Round 1

## 1. Roster depletion can softlock the campaign — BLOCKING

**Problem.** Every story mission needs a squad of 4. The document lists three ways to lose operators permanently, and nothing guarantees the player can still field 4:
- Downed operators outside the zone are "lost when the successful extraction concludes."
- A side-mission wipe closes the operation. Each operator is then captured (45%) or permanently lost (55%).
- Captured operators "are unavailable for deployment," and rescue missions only "may" be offered.

Replacements are limited too. "Campaign milestones expand the roster" and "Recruitment fills available roster space," so recruits arrive only at story milestones. A player who loses several operators between milestones may not have 4 bodies for the next story operation. The story-mission retry rule only "returns to before the failed attempt," which is after those losses, so retrying cannot fix it. The fallback is "complete available side missions," but that only works if the player has enough operators to deploy on them. The doc also never says what happens to equipment an operator was carrying when lost or captured. If it is lost, the "Story progression is intended to outfit a standard squad" guarantee also breaks.

**Source.** Recruitment and loss; Extraction and securing a position; Mission outcomes; Credits and equipment ownership.

**Needed.** A roster floor: emergency recruits, a minimum-squad rule, or story missions allowed with fewer operators. Also a rule for what happens to a lost or captured operator's equipment.

## 2. On story missions, wiping beats extracting with losses — BLOCKING

**Problem.** Take a main story mission where three operators are Downed and one is standing:
- **Extract:** the three Downed operators are permanently lost, and the mission counts as a success.
- **Let the last operator go down:** that is a full-squad wipe, which means Game Over. But "Trying again returns to before the failed attempt," so the player keeps everyone and gets another try.

So the safest play is to throw the last operator into enemy fire. The rules punish the partial success more than the total failure. Calling this "**Game Over.** The campaign cannot continue" contradicts the reload behavior described in the same table cell.

A related gap: there is no rule for saving or quitting mid-mission. If quitting mid-mission reverts to the pre-mission save, then "Each mission is played once" and the irreversible side-mission capture and loss rolls can be dodged by quitting.

**Source.** Mission outcomes table; Extraction and securing a position; Persistence and return.

**Needed.** Make extraction losses on story missions consistent with the retry rule (for example, allow a restart before resolution or make a wipe cost something). Define save points and what quitting mid-mission does.

## 3. The "kits to cut" list breaks campaign choices and rewards — MAJOR

**Problem.** Technical Strategy lists Warmech, Medic and Captain as cuttable and says "affected missions remain playable with the available equipment." But three parts of the campaign depend on those kits:
- **Bring Them Home or Chain of Command** exists to open "the corresponding support kit," meaning Medic or Captain. If both are cut, this mutually exclusive story choice rewards nothing, whichever branch the player picks.
- **Keys to the Giants** ("take heavy equipment") and the "Warmech assault" depend on the Warmech kit.
- The Example operation and the Healing section rely on the Medic's Stim and Rescue. Training examples cite Field Orders (Captain) and Orbital Strike, which is probably also Captain but the doc doesn't say.

"Playable" is not the same as "coherent." The doc defines no fallback reward or replacement for these choices.

**Source.** Technical Strategy course delivery table; Mission choices table; Campaign arc; Healing and Downed operators; Experience and kit training.

**Needed.** For each cut kit, state the replacement reward or branch. For Keys to the Giants, decide whether it is restructured or removed.

## 4. Their Last Order's scripted deaths conflict with the Downed, extraction and wipe rules — MAJOR

**Problem.** The final mission deploys 4 operators plus the four principal characters, and Act IV parts add 2–3 NPC operators per character. The doc never says how the core rules apply to NPC allies:
- Can they be Downed, and can the player revive them?
- Do they count toward a "full-squad wipe" ("every deployed operator is Downed")?
- Are they lost if left outside extraction?
- Who controls them?

Scripted deaths make this worse. The leader must die, and the player-doomed character must die. What happens if a different principal is Downed and left behind, or if the player tries to protect or revive the doomed one? "At least one of the other three" allows more deaths, but the doc never says how, so systemic losses can clash with the story. "Secure a position" missions (including likely finale structures) have no rule for Downed operators when the mission ends. The extraction loss rule only covers "the successful extraction."

**Source.** Act IV and the final assault; Mission outcomes; Extraction and securing a position.

**Needed.** NPC ally rules (control, Downed and revive, wipe counting, extraction). Rules for how scripted deaths override or coexist with systemic deaths. Rules for what happens to Downed operators at the end of a secure-position mission.

## 5. Control-cone rules are undefined when enemies use them on operators — MAJOR

**Problem.** "Both the squad and the enemy can use control," but the rules are written from the squad's side, and several cases are unresolved:
- **Suppressing Fire** "stop[s] enemies moving through its cone." If an enemy Minigun-type unit suppresses the only route to extraction, can a stopped operator continue? Is their remaining AP forfeited? Can this repeat every turn and block withdrawal indefinitely?
- **Overwatch** triggers when a target is "spending AP within it" and gives a "guaranteed hit." Does that include Revive, objective interactions, gear use, or committing to extract? If so, a single watcher guarantees damage to every rescuer.
- Can several Overwatch cones stack on one move? How many reactions does committed AP buy? Does Overwatch fire on a target already Downed mid-path? None of this is stated.
- Melee "preview an approach with the AP needed for the strike reserved." If an Overwatch reaction Downs the attacker mid-approach, does the reserved AP refund?

**Source.** Overwatch and Suppressing Fire; Melee and approach routes; Extraction and securing a position; Difficulty ("Rifle Overwatch is used sparingly").

**Needed.** Define symmetric control-cone rules: what triggers them, how many reactions are allowed, how stacking works, what happens to AP when movement is stopped, and whether extraction can be blocked.

## Round 2 — Cross-examination

### CONFLICTS

**C1. Systems Designer #1 (side-mission half): "the player is pushed to keep a doomed squad in the fight." This only holds in a narrow case, and the finding overstates it.**
The story-mission half matches my Finding 2, and I agree with it. The side-mission half doesn't hold up when you run the numbers. A side-mission wipe hits *every deployed operator*, standing ones included ("Each deployed operator has a 45% chance of capture; otherwise they are permanently lost"). An extraction only loses the operators left outside the zone. With 4 deployed:
- 1 Downed: extracting loses 1 for certain. Wiping loses about 2.2 on average for good, puts 4 at risk, and gives up the mission rewards. Extracting is clearly better.
- 2 Downed: extracting loses 2. Wiping loses about 2.2 dead plus about 1.8 captured, and those captives can only be recovered through rescues the doc says "may" exist. Extracting is still better.
- 3 Downed: extracting loses 3. Wiping loses about 2.2 dead plus about 1.8 captured. Only here does wiping win, and only if the player trusts that rescues will happen.

So the side-mission inversion is a gamble at the edge, not a dominant strategy. Its severity depends on an unspecified rule, the reliability of rescues. If rescues are guaranteed, captured operators are just delayed, and the crossover drops to 2 Downed. The fix Systems proposes ("abandoned Downed operators use the same capture roll as a wipe") is reasonable, but it is MINOR for side missions. The BLOCKING part is the story-mission rule, which is deterministic and free to the player.

**C2. Systems Designer #2 and Player Psychologist #1 rate roster attrition MAJOR. I keep it BLOCKING.**
Systems frames this as "either a grind or a death spiral" depending on whether side missions replenish. That isn't a choice between two acceptable results. The document can't be implemented as written, because one of the two possible answers produces a campaign that can't continue (fewer than 4 operators, no side missions on offer, recruits only at the next milestone, and that milestone sits behind a story mission that needs 4). The Game Over text names "complete available side missions" as the recovery path, which assumes side missions are always available and that the player can deploy on them. Neither is promised. A spec gap where one valid reading causes a hard lock is BLOCKING until it is closed. I do accept Systems' point that if side missions refill without limit, the lock goes away and becomes an economy problem. The cheapest fix is the same either way: a guaranteed roster floor.

**C3. Business Analyst #4 misreads the Armoury as a commercial monetization feature.**
BA argues the coursework scope conflicts with "a paid-skin Armoury." The GDD says "The Armoury turns them [credits] into additional equipment and available cosmetic purchases," and "Skins can also be earned through achievements or bought where available." Skins are bought with in-game credits, not real money. The DLC hook is real, but the "commercial roadmap" tension rests partly on this misreading. BA also says "a 45% capture roll replaces outright death on side missions." It doesn't. 55% of wiped operators still die. That matters for C1 above, because the wipe outcome is harsher than BA implies.

**C4. Feasibility #1 and BA #1 count about 22 missions by adding 8 choice missions on top of 14. Part of that is double-counted.**
The Act II row of the campaign arc already lists "rescue and weapons choices" as a slot among its representative operations. Those are Open the Cages / Take the Assembly Line and probably Long Reach / Heavy Hands. Separately, the column is labelled "Representative operations," so the list isn't exhaustive, and the real count could be higher. The doc doesn't give a firm mission count in either direction. That is a QA finding in itself: no one can confirm the campaign is complete because the authoritative mission list doesn't exist. Their conclusion (16 cycles is not enough) holds even with the lower count, but the exact figure shouldn't be quoted as established.

### CONNECTIONS

**X1. My Finding 2 + Area-attack friendly fire: the story-mission wipe exploit can be triggered on demand.** "Area attacks affect damageable units within their blast, including friendly operators." Nothing requires the player to wait for the enemy. A player who sees extraction coming at a high cost can frag their own clustered squad (or walk the last operator into an Overwatch cone, which gives a "guaranteed hit") to force a wipe and reset. This rules out the defence that "it's hard to wipe deliberately." It also means the Player Psychologist's #2 fix (a mandatory warning listing who will be lost at extraction) *increases* the exploit: the warning screen tells the player exactly when resetting is worth it. The warning should ship, but only together with a fix to the story wipe rule.

**X2. My Finding 5 + Player Psychologist #2: which comes first, the extraction or the wipe?** The mission "concludes when all standing operators are accounted for." If the last standing operator is Downed by an Overwatch reaction while moving into the zone ("entering the cone or spending AP within it can trigger"), the result could be a successful extraction (Downed teammates lost) or a full wipe (story: free reset; side: capture rolls). The doc doesn't define the order of resolution. Under X1, players will learn to steer for whichever result helps them. An enemy Suppressing Fire cone over the zone (my #5) could also stop the last operator just outside it, and the doc doesn't say whether that state can end.

**X3. BA #3 (side missions could be cut) + my Finding 1: cutting side missions removes the only stated recovery path.** If the side-mission layer is cut, which BA argues for and Feasibility #1's budget makes likely, the Game Over recovery text ("complete available side missions before attempting the story operation") has nothing behind it. Recruits then come only from milestones, story extraction losses can't be undone, and Systems #2's "grind" outcome is gone while the "death spiral" outcome stays. Cutting side missions has to include a roster floor on story missions. Otherwise the cut makes Finding 1 certain to happen.

**X4. Narrative #2 / Player Psychologist #4 (player identity) + Mission outcomes: either answer creates a new edge case.** If the Breakout prisoner is a protected avatar (Psychologist's option), the doc needs a rule for that operator being Downed and left outside extraction, or caught in a side-mission wipe. Is that a forced Game Over on a side mission? Does the avatar automatically avoid the 55% death roll? An operator who can't die is also an exploit. They become the obvious one to send on every Overwatch-baiting and rescue task, because nothing they do is ever permanent. If the avatar is not protected, every Act character line aimed "at the player" needs a fallback for when that operator is in the memorial. The identity decision has to be made together with the loss rules, not separately.

**X5. Feasibility #4 + my Finding 4: the 8-unit finale also breaks the wipe definition.** Feasibility asks who controls the four principals. QA asks: if the principals are deployed units and are scripted to die, does "every deployed operator is Downed" count them? If it does, a scripted death plus three Downed operators could trigger a story Game Over in the final mission, and so the X1 reset exploit. If it doesn't, the player can keep fighting with only NPCs standing, which the HUD and turn loop (Tab cycling, squad lineup) were never specified for.

### REVISIONS

- **Finding 2: keep BLOCKING, and widen it.** Add X1 (a wipe can be forced with friendly-fire area attacks) and X2 (no resolution order for the last operator being Downed at the zone). Following C1, I am *not* extending the BLOCKING rating to the side-mission inversion that Systems raised. On side missions it is a MINOR edge case, conditional on rescue reliability.
- **Finding 1: keep BLOCKING** (see C2), and add the requirement from X3 that any side-mission cut must come with a roster floor.
- **Finding 3 (cut list): severity stays MAJOR, but I'm deprioritizing it as a QA item.** Four of six reviewers raised it independently, so it's covered. Feasibility #1 makes the cuts likely rather than hypothetical, which raises its importance. But the fix (name a replacement reward per branch) is cheap and isn't an exploit, so it's not where QA adds value.
- **Finding 4: narrowing it.** The "secure a position has no Downed-operator rule" part overlaps with Systems #5, which covers it more fully alongside escort and hold failure states. I'm leaving that part to Systems #5 and keeping my finding to NPC allies, scripted deaths, and the wipe-counting problem in X5.
- **Finding 5: keep MAJOR, upgrading the "Overwatch on Revive" question to the most important part of it.** Taken with X1 and X2, whether Revive and the extraction step trigger guaranteed-hit Overwatch decides whether rescuing a teammate is ever worth doing. That makes it the factor that decides whether extracting or wiping is the better choice, not a side question about edge cases.
