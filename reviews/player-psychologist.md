# Player Psychologist — Round 1

## 1. Permanent loss is harsher than a full wipe, which pushes players to throw missions. BLOCKING

**Problem.** Losing one operator is permanent. Losing the whole squad has no lasting cost: the mission fails and can be retried with the same setup. So a player whose favourite operator is Downed far from extraction has a reason to get the rest of the squad Downed on purpose rather than extract without them. That inverts the "bring your operators home" fantasy. The design's emotional peak, an agonising withdrawal, turns into a choice between a sacrifice and a reset button, and players will press reset. The GDD also never says what happens to saves, or whether there is a manual save. Without that rule, players will reload whenever a loss happens, and the loss mechanic stops meaning anything.

**Source.**
- Line 308: "Any operator still outside the zone, including a Downed operator, is lost when the successful extraction concludes."
- Line 312: "If the whole squad is Downed, the mission fails. The operation remains available for another attempt."
- Line 326: "Each offered mission retains its setup across retries."
- Omitted: what the player keeps after a failure (XP, gear uses, injuries), save and reload rules, and any player-selected difficulty or ironman option.

## 2. Downed operators are abandoned automatically, without confirmation. MAJOR

**Problem.** Leaving a standing operator behind needs an explicit decision. Downed operators get no such step. The mission ends once all *standing* operators are accounted for. If the last standing operator steps into the zone, possibly through a misclick or a waypoint error, every Downed teammate is lost permanently with no prompt. The document has no undo for movement, and Space is used both to confirm actions and (held) to end the turn. When a player loses a heavily customised operator to an input mistake rather than a tactical one, they feel cheated rather than grieving, and that is a common point to quit.

**Source.**
- Line 308: "the player can explicitly commit to leaving another standing operator behind. The mission concludes when all standing operators are accounted for".
- Line 498 and line 505: Space confirms actions and hold-Space ends the turn.
- Omitted: a confirmation step before abandoning Downed operators, and any undo or misclick protection.

## 3. The second mission introduces too much at once, and several core rules are never taught. MAJOR

**Problem.** Breakout teaches movement and cover with one unarmed prisoner, which is a good start. The next mission, A Place to Stand, then introduces at once: a four-operator squad, AP budgeting across operators, attacks and damage ranges, Overwatch, and the whole headquarters layer (Barracks, Armoury, War Table, XP, credits, training, appearance). That is the point where the first-hour player is most likely to feel overwhelmed. Several rules that decide life or death have no stated teaching moment at all:
- the cover, then armor, then health damage pipeline;
- reaction fire triggered by spending AP inside a cone;
- enemy grenade timing;
- Suppressing Fire stopping movement;
- splitting a move costing extra AP;
- the extraction loss rule.

The GDD names no tooltips, glossary or codex, mission-replay tutorial, or difficulty option to catch players who miss a lesson. The tactical promise "understand the mistake behind a failed one" (line 62) depends on these rules being learned, but the document only says players learn "through encounters".

**Source.**
- Lines 511–515 (Learning through the campaign).
- Line 366: "Headquarters becomes available after the resistance takes its initial base."
- Lines 145, 155, 185–187, 284, 308: rules with no matching teaching beat.

## 4. Kit lockouts are blind and permanent, and they can remove a core safety tool. MAJOR

**Problem.** Mutually exclusive operations permanently close off an equipment line, and the player usually hasn't tried either option yet. "Bring Them Home or Chain of Command" decides between the Medic and Captain kits. The Medic is the only stated source of ranged Revive and Stim, and the GDD's own example squad includes one. A player who picks Captain may find out much later that the withdrawal and Downed systems are harder without a Medic, and blame the choice rather than their own play. That kind of late regret drives restarts and abandonment. The document doesn't say whether the choice screen previews or lets you trial the kit, or whether the lost kit can ever be obtained later, for example through side missions or the Armoury.

**Source.**
- Lines 353–360: "Completing one advances the campaign and closes the other opportunity."
- Line 206: ranged revival is Medic training.
- Line 107: the example squad depends on a Medic.
- Line 362 ("Side operations supply additional equipment...") is too vague to show the other path is recoverable.

## 5. The attachment pillar starts late, and the first operator's identity is undefined. MINOR

**Problem.** The "squad with an identity" pillar depends on naming and customising operators, but the Barracks and appearance editing only open once headquarters exists. Breakout's prisoner is never said to be customisable, named by the player, or a lasting roster member. Players form attachment early. If the first operator they protect is a fixed character, or isn't carried forward, the player's first investment of care is lost. The document also doesn't say whether benched operators earn XP. That matters to the stated "bench of specialists" playstyle, because players quickly sense when unused characters are falling behind.

**Source.**
- Line 214: "The opening escape introduces a single prisoner".
- Line 250: "Randomized recruits arrive with a usable identity and can be customized immediately".
- Line 366.
- Line 119: "Mission experience contributes to training", with no statement of who receives it.

## Round 2 — Cross-examination

Four of six reviewers (Systems #1, Narrative #4, QA #1, and my #1) independently found the wipe-beats-loss inversion. That diagnosis is settled. The disagreements below are about remedies and priorities, and that is where my lens pushes back.

### CONFLICTS

**C1. Systems Designer #1's remedy would turn an exploit into a quit point.** Systems proposes "a failure cost that is at least as bad as losing one operator (for example, Downed operators are captured or lost on a wipe...)". I agree the cost has to exist. But making every Downed operator permanently lost on a wipe means one bad turn can delete four named, customised characters at once. That happens to a player who, by my #3, was never taught the cover/armor pipeline, reaction-fire triggers or grenade timing. Combine that with QA #3 (no recruitment floor, possible roster softlock) and the result is a death spiral. In this genre, a death spiral is when players uninstall, not when they "grieve". The emotional target in the pitch is the hard withdrawal decision, not catastrophe. My position: a wipe should cost **more than a successful extraction and less than four permanent deaths**. Two options:
- Downed operators are *captured*, opening a time-limited rescue side mission. This echoes the prisoner opening, which also answers Narrative #4's "what does being left behind mean in fiction?"
- The operation closes and its rewards are lost.

Either removes the exploit without a total-loss cliff. This is a real disagreement about severity curves, not about the bug.

**C2. Systems Designer #3 wants carry-over penalties (recovery time) to force bench rotation. I'd use carrots, not sticks.** Two problems with injury timers:
- **They mean nothing here.** QA #3 and Systems #2 both note there is no campaign clock. If nothing advances between missions, a recovering operator just waits for the player to run one side mission. That adds friction without real choice.
- **They stack punishment on the most anxious players.** Permadeath is already the game's main stress source. Adding recovery downtime on top makes "my favourite got hurt" a double penalty and pushes players toward the save-scumming I flagged in #1.

Rotation is better driven by reward: partial XP for benched operators (the omission in my #5), side missions tuned for B-team kits, and memorial/veteran recognition that values breadth. I accept Systems' point that the bench currently has no systemic job. I disagree that a penalty is the right lever.

**C3. Feasibility #5 ("a single body type with tinted or swappable outfits") cuts below the attachment floor; Business #2's version is the one to adopt.** Both are right that the full creator fights the art bottleneck. But my #5 rests on players forming attachment early, and the cheapest attachment drivers are:
- player-given names and callsigns;
- a recognisable face or silhouette per operator;
- visible history (missions, kills, near-deaths);
- the memorial.

A single body type with tint-only variation risks every operator reading as the same mannequin in the HQ lineup, and squads you can't tell apart get no protective feeling. Business #2's "callsigns, a small set of presets, mission history, and the memorial" keeps that floor. I endorse that cut. My one condition: the Breakout prisoner gets the same nameable identity from minute one.

**C4. Narrative Critic #5 wants the branch choices to carry more moral weight. Combined with my #4, that makes things worse unless the mechanics change too.** Narrative wants "Open the Cages or Take the Assembly Line" to land as an ethical choice. As written, the same choice also gates gear without preview. Players then make a moral choice on loadout grounds, then feel guilty, or choose morally and get punished mechanically weeks later. Both outcomes create resentment, not meaning. Adding narrative weight is only safe if the mechanical side is softened: preview the kit, and make the unchosen kit recoverable later at a cost. I'd argue the moral framing should be added *after* that fix, not before, or it amplifies my #4.

### CONNECTIONS

**X1. The player-facing example teaches the wrong extraction rule (QA #1 + my #2).** QA spotted that line 117, the Example of Play, says the player "must" revive Downed operators, and that the mission ends only when the squad reaches the zone "or the player has explicitly committed to leaving an operator behind." That is the passage most likely to become tutorial copy, store text and trailer narration. So the player's mental model will be "the game will ask me before anyone is abandoned", and the real rule (line 308) silently abandons Downed operators. QA's case of a Medic walking through the zone on the way to a revive is the exact misclick scenario from my #2. This is no longer just missing confirmation UX; it is a broken promise the game makes to the player. See the upgrade in R1.

**X2. Untaught rules plus friendly fire on Downed bodies create the worst feel-bad in the design (QA #2 + my #3).** QA asks whether area attacks (frag, Airburst, Orbital Strike) can finish off a Downed operator, since line 157 says they hit friendlies. If they can, and the player isn't clearly told, a player can permanently kill their own favourite with their own ultimate ability. Self-inflicted permadeath from a hidden rule is the strongest "this game cheated me" moment possible. Damage previews on Downed allies and a hard warning prompt are needed. I'd fold this into my #3 as its most severe instance.

**X3. Freeform movement makes reaction-fire previews a trust requirement, not a nice-to-have (Feasibility #4 + my #3).** Feasibility notes that movement previews "have to forecast reaction fire along a continuous path" on a gridless map, and flags this as the system most likely to slip. From the player's side, that preview is the *only* way a player learns line 185's "spending AP inside a cone" trigger without a tutorial beat. If the preview is cut or inaccurate to save engineering time, the "understand the mistake behind a failed one" promise (line 62) fails. Players will experience reaction fire as random, which is exactly the hit-chance frustration the game's hook claims to remove (Business #4). Any scope cut must protect this preview.

**X4. A scope cut makes onboarding the whole product (Feasibility #1 / Business #1 + my #3).** Both production reviewers recommend a week-8 target like "Act 1 plus one side-mission type." If that happens, Breakout and A Place to Stand are not the first hour of a long game; they *are* most of what playtesters and graders will see. The overload in mission 2 then drives the entire impression of the slice.

**X5. Enemy control can produce unavoidable damage the player can't read (QA #4 + Systems #5 + my #3).** QA notes that enemies can use Suppressing Fire to pin a player inside a grenade marker, making the response window meaningless. Systems notes that the approach phase rewards slow overwatch creep. Together:
- The approach teaches the player that patience is safe.
- Extraction then traps them with a control-plus-grenade combo they were never shown.

That is a difficulty spike that reads as unfair rather than hard.

**X6. The audience will import XCOM habits (Business #4 + my #1).** Business shows the design matches the XCOM 2 template. That audience arrives already expecting save-scumming and Ironman toggles. Leaving the save model undefined (my #1 omission) is therefore not neutral: the default player behaviour for this audience is to reload losses, which removes the memorial's meaning unless the GDD makes a deliberate call.

### REVISIONS

- **R1 — #2 upgraded from MAJOR to BLOCKING.** QA #1's line-117 contradiction shows the document *itself* promises an explicit abandonment decision. So silent loss of Downed operators is a contradiction in the core loss mechanic that the emotional pillar depends on, not a UX polish item. It must be resolved before the extraction design is final.
- **R2 — #1 stays BLOCKING; remedy refined.** See C1: the fix should not overcorrect into wipe = total roster loss.
- **R3 — #3 stays MAJOR, but its priority rises.** X4 means onboarding is likely most of what the eight-week slice contains. I'm also adding X2 (friendly fire on Downed allies) as its most severe instance.
- **R4 — #4 stays MAJOR, with broader scope.** Systems #4 confirms Long Reach/Heavy Hands also locks a kit, and that no balance target exists across the 16 branch paths. My concern is the player-side half of that problem: late, blind regret. Business #3 suggests cutting branching for scope. If that happens, #4 disappears, and I'd support that cut on player grounds as well.
- **R5 — #5 split.** I'm handing the "benched operators and XP" point to Systems #3, which states the systemic problem better; my input is the carrot-not-stick remedy in C2. The prisoner-identity point stays MINOR on my side, but it depends on Narrative #2. If the prisoner is the player's avatar ("the player becomes one of its skilled operators", line 422), that operator either has to be exempt from permadeath, which would quietly undercut the loss pillar, or be fully losable, which breaks the avatar framing. That decision needs to be made early, so I'd flag it as a dependency rather than raise its severity.
