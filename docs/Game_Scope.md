# Grimstroke Game Scope

Grimstroke is a fantasy DPS and build-crafting RPG prototype. The player prepares a Rogue's talents, equipment, and skill sequence, then watches the build play out against an enemy within a time limit. The central challenge is finding combinations that deal enough damage and overcome the target's defenses.

Grimstroke continues the completed FacelessVoid phase. The current game is the accepted starting point; the next phase's goals have not yet been chosen.

## The game loop

Start an Adventure, choose a primary Rogue specialization, and begin in the Tavern. Select encounters, inspect enemies, and prepare a build before fighting. Combat resolves deterministically from the build, target, and random seed, then plays back with animations, damage feedback, status effects, and a combat log. Playback supports speed changes and skipping.

Win encounters to earn rewards, acquire equipment, and progress through generated contracts and bosses. Spend gold in shops and adjust the build as new gear, talents, and skills become available. A failed fight provides a damage recap and an opportunity to revise the build and retry. Optimization and enemy matchups matter; weak builds can fail, and some enemies deliberately counter particular strategies.

## Builds and progression

The playable class is Rogue, with four implemented talent trees: **Assassin, Bladedancer, Shadow, and Thief**. Ranked talents, inherent bonuses, skill unlocks, and interactions between trees support different builds.

Adventure starts with one primary tree. After the first completed contract's reward and shop flow, the player chooses a distinct secondary from two saved options. Both trees contribute inherent bonuses and skill unlocks; only the primary grants its per-point scaling bonus. Talent points share a **45-point cap**, with **three points earned per completed contract**.

The player arranges unlocked skills into a sequence. Damage, cooldowns, critical hits, repeated attacks, triggered effects, buffs, debuffs, and enemy defenses interact during combat. Exact values and formulas belong to the current game code and resources rather than this overview.

## Equipment and economy

Equipment uses seven slots: **Dagger, Hood, Doublet, Gloves, Pants, Ring, and Necklace**. A fresh Adventure starts with only a Crude Dagger. Generated equipment, rarity-specific stat pools, Cursed and Chaos drawbacks, Unique effects, and **twenty authored Legendary items** provide further build choices.

Loot, rewards, shops, selling, gold-related abilities, and progression pacing are implemented. Current prices, rewards, and resale behavior form the baseline for a future economic review; resale profit is not automatically a defect to remove.

## Play modes and presentation

- **Adventure:** persistent encounters, contracts, rewards, equipment, and character progression.
- **Practice Room:** independently saved build experiments with configurable targets and unrestricted tree selection.
- **Test mode:** session-only development runs, hidden from the normal title screen.

The game includes illustrated environments and enemies, character animation, item and skill icons, talent-tree and equipment interfaces, tooltips, combat feedback, audio, logs, and staged reward/shop reveals. Supporting browser labs cover content authoring and inspection; their instructions live beside the tools.

## Project setup and working boundaries

Open [project/project.godot](../project/project.godot) in **Godot 4.7**. The main scene is `project/scenes/game_root.tscn`. Windows saves and settings use `%APPDATA%/Grimstroke/`, separate from FacelessVoid and Enigma.

Runtime logic lives in `project/scripts/`, screens in `project/scenes/`, content and artwork in `project/data/` and `project/assets/`, and checks in `project/tests/`. `build_content_registry.gd` identifies the active build content; some packaged resources remain for legacy compatibility. Tool fixtures live under `tools/p6/fixtures/` and are not current design specifications.

The imported baseline passed focused startup, mode, combat, playback, and save/replay checks. Existing first-import, renderer, certificate-store, and shutdown diagnostics remain; export readiness, long-session stability, and universal build balance have not been established. Validate changes in disposable copies with redirected `APPDATA` and `LOCALAPPDATA`, keeping all test save paths separate. Never use real player profiles as test fixtures.

## Next phase and documentation

An economic audit is intended future work. Broader balance work and trigger usability/performance investigation are also deferred candidates. Agree on the next phase before assigning milestones or changing these policies.

Keep this as the single maintained project scope document. Update it when the game's scope changes; do not create separate handoffs, status summaries, or milestone documents unless explicitly requested. Keep execution logs in ignored reports. Use code and resources for detailed mechanics, and Git history for past decisions.

The starting snapshot is Grimstroke commit `34cfed5`, imported from FacelessVoid `b5ab445`. Previous phase documentation is recoverable there without keeping it in the working tree.
