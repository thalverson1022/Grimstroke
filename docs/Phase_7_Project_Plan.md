# Phase 7: Project Grimstroke

**Status: Draft for review. Implementation has not started.**

## Goal

Turn the existing contract-based DPS game into a town-centered Adventure with meaningful ways to invest in a build, a finite mountain conquest goal, and continued contract play after victory.

The player earns resources through contracts, spends them on equipment and town services, and prepares to climb Peak Deeps and defeat the White Dragon. The mountain is available from the start but initially far too difficult. Preparation, build choices, and judgment determine when to attempt it.

**Design the new systems first; balance the economy around them afterward.** Gold rewards, prices, resale, and spending opportunities must be evaluated together once the services are defined.

This plan records the agreed direction and proposes implementation stages. Candidate blessing effects and numerical examples are not finalized balance specifications. The [Game Scope](Game_Scope.md) describes the implemented starting baseline; this plan describes the proposed phase.

## Player journey

1. Choose a class and primary subclass, then arrive in town with all destinations visible and accessible. The player starts without gold.
2. Enter the Tavern and complete a lightly revised version of the existing tutorial encounters. Replace the shopping introduction with the Lucky Coin, gold, talent points, and random gear rewards. Completing the Tavern does not refresh shop stock.
3. Meet **Ghit**, the contract giver. The Tavern becomes the recurring quest hub.
4. Inspect and accept a contract. Acceptance reserves it; the player can prepare in town before departing.
5. Use the Road to enter the selected contract or choose the Mountain Road instead.
6. Complete contracts, acquire resources, and return to town to choose how to spend them. The automatic post-contract shop is removed.
7. Earn the secondary-subclass unlock from the first completed contract. It appears in the rewards, but must be claimed at the Weapon Master.
8. Attempt the fixed Mountain Road, progressing through authored encounters and branching choices to the White Dragon.
9. Defeat the White Dragon to conquer Peak Deeps and see the victory screen. Continue the same run through contracts afterward. C30 is intended to be much harder than the White Dragon.

## Town and expedition rules

The town is the main interface. Its destinations are the **Tavern, Shop, Blacksmith, Alchemist, Cathedral, and Weapon Master**, with the **Road** providing expedition access. The exact visual layout and interaction design will be developed within this phase.

### Lives, defeat, and retreat

- Lives are global across the run. The proposed starting amount and maximum are **three**; maximum lives can increase.
- Losing a combat attempt costs one life. At zero lives, the entire run ends.
- With lives remaining, the player stays at the encounter and may adjust the macro, prepare potions, and retry the same enemy.
- Fleeing an encounter costs one additional life and returns the player to that expedition's map. It does not return directly to town.
- From the map, the player can choose another available path or abandon the expedition for free and return to town.
- Defeat followed by fleeing therefore costs two lives. Any action that reduces lives to zero ends the run.
- Training does not cost lives, award rewards, consume potions, or advance encounter-limited blessings.

Players may inspect contract maps, abandon contracts, and obtain new ones. Completing only early encounters before abandoning is an allowed resource-gathering strategy. Later encounters and completion rewards should make deeper progression more attractive; this is an economy-balancing requirement, not a reason to prohibit early abandonment.

### Mountain Road

- The map is fixed and inspectable before entry, with authored enemies and some choice of path.
- The first boss is the **Boarcerotops**, envisioned as a large DPS check. The final boss is the **White Dragon** at the top of Peak Deeps.
- Mountain encounters grant **no rewards**. They do not refresh town shop stock.
- Defeat, retry, flee, and abandonment use the same life rules as contracts.
- Leaving for town resets the ascent. A later visit starts over rather than retaining cleared bosses.
- Victory marks the main playthrough goal but does not end the character's run. Contracts remain playable afterward.

## Town services

### Tavern

Reuse the existing opening encounters with the agreed reward and shopping changes. Introduce Ghit and the contract loop, then retain the Tavern as the quest hub. The contract selection interface must support inspection, reservation, and returning to town for preparation.

### Shop

The town shop sells gear and potions and buys both back from the player. It replaces the automatic post-contract shop interface.

Gear and potion stock refresh only after a successful **contract boss kill**. Ordinary victories, abandonment, Tavern completion, and mountain bosses do not qualify. Purchased offers sell out.

Gear retains the current paid reroll mechanics. Rerolling is an intended core method of seeking strong equipment, not incidental behavior to suppress. Potions have a separate fixed number of randomly drawn offers; gear rerolls cannot change or replenish them.

Alchemist upgrades can expand gear and potion offer counts and improve purchase discounts. A separate permanent gear-reroll discount is a candidate. Initial stock, exact counts, costs, and interactions with capacity upgrades remain design tasks.

### Blacksmith

The blacksmith offers focused, permanent item modifications through two actions:

| Action | Agreed behavior |
| --- | --- |
| Reroll | The first attempt selects the only stat slot on that item that may ever be rerolled. Each attempt rolls a stat and fresh value from that equipment slot's eligible pool, preserving Basic versus Master category. Attempts are unlimited, with exponentially increasing gold cost. Legendary gear cannot be rerolled. |
| Forge upgrade | The player chooses any eligible normal stat slot as the preferred target. It has the highest chance of receiving a random positive increase, with a small chance that another eligible slot receives it instead. The upgrade permanently locks the entire item against further blacksmith rerolls and upgrades. |

Legendary items may receive the one-time forge upgrade, but only to normal stats. Their Legendary effect is never an eligible target, including an accidental target.

The original stat roll and forge bonus have separate ranges. A Cathedral max-roll blessing maximizes both components where a forge bonus exists; it does not grant a forge bonus to an unforged stat.

**Illustrative example, not balance values:** an original +3–5 stat rolls +4. Forging grants +1 from a +1–3 bonus range, making the total +5. A later max-roll blessing produces +5 original and +3 forge bonus, totaling +8. Without forging, that blessing would produce only +5.

### Cathedral

The player offers gear and a gold tithe to receive one random blessing. The offering and tithe are committed to the ritual. A dud returns nothing. A transformation blessing returns the offered item with the specified change; other results consume it in exchange for the reward or buff.

Blacksmith-modified items can be offered. A max-roll result retains their stat identities and maximizes the original and existing forge components. Purification can remove a curse while preserving the item's beneficial properties.

The terminology separates gear families:

| Family | Rarities |
| --- | --- |
| Angelic | Crude, Basic, Master, Epic, Unique |
| Demonic | Cursed, Chaos |
| Neutral | Legendary |

Cursed and Chaos are not steps between Epic and Unique on a single Angelic rarity ladder. For offerings, **quality means rarity**. A bonus for prior blacksmith investment is a candidate, with its exact influence undecided.

The proposed probability model has two stages:

1. **Choose a blessing block.** Offering rarity determines the block distribution. Higher reward blocks remain possible at very low odds; they are not absolutely locked out. Explicit probabilities must describe cross-family results rather than relying on an assumed linear rarity ordering.
2. **Choose a result inside that block.** The tithe reduces the odds of less advantageous outcomes and improves the distribution within the selected block, even if it is a rare higher block. It never changes block-selection odds.

Exact tables remain hidden from the player. We must design understandable offering feedback without exposing the full table. Duds are allowed. Harmful results are undecided and are not assumed in the initial implementation.

#### Candidate blessing blocks

These preserve the first-pass ideas for design and testing. Quantities, eligibility, and wording remain provisional.

| Block | Candidate results |
| --- | --- |
| Basic | Nothing; return the offering upgraded to Master; +1 base damage for 3 attempts. |
| Master | Nothing; random Basic item; return the offering upgraded to Epic; +3 base damage for 5 attempts. |
| Epic | Nothing; random lower-level Angelic item; random Cursed item; random potion; maximize the offered item's stats; +5 base damage for 10 attempts. |
| Unique | Nothing; random lower-level Angelic item; random Demonic item; random potion; maximize item stats; reroll the special stat; a run-long buff to base damage, crit chance, attack speed, magic find, or shop discount. |
| Cursed | Nothing; random Angelic item; random potion; return the offering without its curse; ignore block, dodge, or absorb for 5 attempts; +100% crit damage for 2 attempts. |
| Chaos | Nothing; random Cursed item; random Angelic item; random potion; return the offering with all values changed to positive; ignore block, dodge, or absorb for 5 attempts; +100% crit damage for 2 attempts. |
| Legendary | Nothing; random lower-level item; 2 random potions; run-long base damage, crit chance, attack speed, magic find, or shop discount; all attacks inflict poison; +10 poison stack maximum; retriggers retrigger again; acquire the sacrificed item's Legendary effect; +1 life; ignore block, dodge, absorb, or cleansing for 10 attempts; +200% crit damage for 5 attempts; poison ticks 100% faster for 5 attempts; +10 seconds for 5 attempts; +100% gold rewards for 5 attempts. |

An encounter-limited blessing consumes one duration charge per actual combat attempt, whether the player wins or loses. Training consumes none. Permanent blessings last for the remainder of the current run.

Before implementation, resolve: Crude offering behavior; the meaning of “lower level”; transformation eligibility when the rolled block differs from the offering; beneficial treatment of Chaos modifiers; eligible stats and special effects; duplicate blessing stacking and caps; finite retrigger behavior; Legendary-effect compatibility; life-reward behavior at maximum lives; and precise percentage definitions. Do not invent these rules during coding.

### Alchemist

The alchemist sells permanent improvements for the current run and restores lives. It does **not** sell potions; the shop does.

Confirmed services are increased maximum lives, life restoration, increased gear inventory capacity, increased potion capacity, increased gear offers in the shop, increased potion offers in the shop, and improved shop discount. More contract choices and a gear-reroll discount are candidates.

Define upgrade steps, caps, restoration rules, and whether increasing maximum lives also restores current lives. Exact gold amounts follow during economy tuning. These purchases do not carry into a new run.

### Weapon Master

- Spending unspent talent points is free and possible anywhere.
- During the Tavern tutorial, respecs are free and available through the talent interface.
- After the tutorial, respecs occur only at the Weapon Master. They refund all allocated points and do not change the primary or secondary subclass.
- Respecs begin cheap and become increasingly expensive with repeated use. The exact pricing curve is undecided.
- The first completed contract visibly awards the secondary-subclass unlock. The Weapon Master is where it is claimed: choose from two fixed random options, both distinct from the primary. Visiting again cannot reroll the choices.
- Training uses the player's actual gear and current talent allocation against a dummy with adjustable mechanics. Reuse the Practice Room presentation where useful, without its gear editor or hypothetical talent allocation.

## Potions

Potions are powerful, single-attempt consumables intended to overcome difficult mechanics, cover build weaknesses, and enable dramatic combinations. They are particularly important for mountain preparation.

- One potion occupies one dedicated potion slot; inventory copies do not stack into one slot.
- Any number of carried potions may be selected for a fight.
- Consume selected potions when the fight starts, not while merely preparing.
- Effects expire after that attempt, including on defeat. A retry requires fresh potions.
- Numerical effects stack. Duplicate binary effects, such as ignoring resistance, confer no additional benefit.
- Training consumes no potions.

Initial effect candidates include ignoring resistance, reducing enemy block by 10, adding 10 seconds, and granting +50% crit chance with +100% crit damage. These are examples, not finalized values. Define how each effect interacts with existing caps and combat ordering before implementation.

## Milestones and completion criteria

The [Phase 7 milestone tracker](Phase_7_Milestone_Tracker.md) owns the eight milestones, completion checkpoints, task status, blockers, and review gates. This plan owns system rules and scope. Consult the tracker for current progress rather than maintaining a second status table here.

The mountain's intended difficulty and route are designed early so services have a clear purpose. Final values are tuned after the systems exist. C30 must support the intended post-victory challenge, but acceptance does not require exhaustive balance of unlimited contract levels or every possible build.

## Cross-system validation

Test the boundaries where these systems meet, not only each screen independently:

- Save/load preserves current and maximum lives, pending secondary choices, stock and sold offers, potion inventory, queued consumption, service costs, forge history, blessings, expedition state, and mountain victory.
- Rewards, purchases, sacrifices, life losses, and boss-triggered refreshes cannot occur twice from repeated input, reopening a screen, or ordinary save/load.
- Fleeing does not count as clearing an enemy or bypass a mandatory route requirement. Define alternate-path availability explicitly.
- Potions and blessings apply to actual resolution, not merely playback. Replaying or skipping the animation does not consume them again.
- Equipment transformations handle inventory capacity, item ownership, unique effects, and blacksmith locks consistently.
- The player sees costs, permanent commitments, life consequences, and available choices before confirming consequential actions.
- Preserve supplied asset identities and existing gameplay outside the agreed changes. Run tests in fresh disposable copies with redirected user-data paths; never use real player saves as fixtures.

## Scope controls and remaining decisions

No further preliminary interview is required to produce this draft. The following are bounded design work, not implied implementation choices:

- Town layout, art requirements, navigation, initial shop stock, exact tutorial rewards, and whether contracts can remain reserved during a mountain trip.
- Precise respec escalation, alchemist upgrade limits, restoration and life-cap behavior, gear reroll eligibility, forge odds/ranges, and post-blessing blacksmith-lock behavior.
- Initial potion catalog, prices, combat-cap interactions, overflow handling, and presentation of redundant binary potions.
- Cathedral block matrix, in-block weights, tithe schedule, transformation rules, initial blessing catalog, stacking rules, and optional investment bonuses or harmful outcomes.
- Mountain boss roster, branching route, tuning targets, repeat-victory behavior, and exact presentation of post-victory continuation.
- Save compatibility and how existing Adventures enter the new flow. No reset is authorized by this plan.

This phase does not implicitly add new playable classes, a talent-tree redesign, town building or NPC simulation, crafting materials, potion crafting, between-run progression, or a separate post-victory mode. New mechanics required by an approved potion or blessing are scoped within that system; broader combat rewrites require an explicit decision.

Maintain **one Phase 7 design plan** here and **one milestone tracker** for progress and acceptance. Keep the game scope short, exact values in their owning code/data, and test outputs in ignored reports. Do not create per-milestone documents, additional handoffs, or duplicated status summaries unless requested.
