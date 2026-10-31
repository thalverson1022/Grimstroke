# Grimstroke — Next Phase Handoff

Updated: 2026-10-31. **Read this file first for new work.**

Grimstroke was initialized from FacelessVoid commit `b5ab4458a45c65b570de08a69865fded2da64a61` with fresh Git history, plus the source workspace's handoff and three documentation navigation updates. Remote: `https://github.com/thalverson1022/Grimstroke.git`. Gameplay is unchanged. Godot's project name and custom user directory are `Grimstroke` (`%APPDATA%/Grimstroke/` on Windows), keeping prior phases' saves separate. Historical Phase 6 documents retain their original project names and paths; adapt old tools only after inspecting them.

Phase 6 is accepted and complete. Its final baseline is on `main`, merge commit `b5ab445` ([PR #1](https://github.com/thalverson1022/FacelessVoid/pull/1)). The next phase's scope and milestones have not been defined. The user has identified an economic audit as intended future work; this handoff does not start it.

## How to start a task

Read this handoff and the user's current request, then inspect only the relevant source and resources from the table below. Search for the affected symbols before opening whole files. Load a specification or historical record only to answer a concrete question that the current source and task do not resolve.

Treat the accepted implementation as the starting ground truth. Phase 6's redesigned mechanics are implemented features, not proposals awaiting approval or work to repeat. New user direction can change that baseline. If implementation and an accepted contract conflict, identify that specific discrepancy rather than reopening the phase.

**Do not preload the Phase 6 onboarding, milestone trackers, decision logs, design reviews or regression reports.** Historical “pending,” “next” and experimental instructions describe old checkpoints. They do not authorize new work. Use the reference index in [docs/README.md](README.md) only when a task needs it.

## Accepted baseline

| Area | Ground truth to preserve unless the task changes it |
| --- | --- |
| Project | Godot 4.7; open `project/project.godot`, main scene `project/scenes/game_root.tscn`. Repository: Grimstroke; sibling FacelessVoid and Enigma are separate. |
| Builds | Four Rogue trees: Assassin, Bladedancer, Shadow and Thief. Ranked talents, skill unlocks, intrinsics and cross-tree interactions are implemented. |
| Progression | Shared 45-point cap; three points per completed contract. A distinct secondary is earned after the first contract's normal reward/shop flow, from two persisted choices. Both trees provide intrinsics/unlocks; primary alone provides per-point scaling. |
| Modes | Adventure persists progression. Test is session-only and hidden in normal title UI. Practice has its own persistence. Test/Practice role selection is unrestricted. |
| Gear | Seven slots, including Gloves and Pants; twenty authored Legendaries and accepted supplied artwork. Fresh Adventures equip only Crude Dagger. Equal eligible-slot acquisition and equal Basic-stat weights within each slot are implemented; other rarity/pool rules remain current. |
| Combat | Current ordering, triggers, statuses, repeats, damage rules and deterministic resolution are accepted. Exact formulas and item/talent values live in current code/resources; inspect the relevant ones rather than reconstructing them from past decisions. |
| Presentation | Current art, compact own-item hovers, talent trees, combat cues, logs and staged shop/reward reveals are accepted. Equipped-reference/projected comparisons are hidden. Shop skip defaults OFF each launch and persists only within that session. Skip/death playback includes the verified first-frame correction. |
| Saves | Adventure v5, Practice v4, shared epoch1 boundary. The seven-slot reset policy is already implemented; it is not an instruction to reset real saves during onboarding or validation. |
| Difficulty | Optimization and synergy matter; weak builds can fail and severe counters can be intentional. Preserve current tuning, rewards and acquisition behavior as the comparison baseline. |

## Open only the relevant area

Paths below are entry points, not a required reading list. Follow their direct dependencies as needed.

| Task | Start here |
| --- | --- |
| Build state, roles, points | [build_state.gd](../project/scripts/autoload/build_state.gd), [build_progression.gd](../project/scripts/systems/build_progression.gd), [build_resolver.gd](../project/scripts/systems/build_resolver.gd) |
| Talents and skills | `project/data/subclass_trees/`, `project/data/skills/`; [build_content_registry.gd](../project/scripts/systems/build_content_registry.gd) identifies active content. |
| Combat mechanics | [combat_resolver.gd](../project/scripts/systems/combat_resolver.gd) and the affected effect/resource class. For a rule explanation, read the relevant section of [Combat Mechanics Reference](Combat_Mechanics_Reference.md). |
| Gear, loot or economy | [gear_generator.gd](../project/scripts/systems/gear_generator.gd), [stat_catalog.gd](../project/scripts/systems/stat_catalog.gd), `project/data/gear/`; follow transaction ownership from BuildState. |
| Adventure flow, shops, rewards | [game_root.gd](../project/scenes/game_root.gd), [combat_screen.gd](../project/scenes/combat/combat_screen.gd), then the affected overlay/transaction. |
| Practice | [training_room.gd](../project/scenes/training_room/training_room.gd) and its affected view/editor. |
| Saves or reset | [save_system.gd](../project/scripts/systems/save_system.gd), [practice_save_system.gd](../project/scripts/systems/practice_save_system.gd), [seven_slot_save_boundary.gd](../project/scripts/systems/seven_slot_save_boundary.gd) |
| Visuals, playback or audio | Affected `project/scenes/combat/` view, `project/scripts/ui/` component or [audio_manager.gd](../project/scripts/autoload/audio_manager.gd). Preserve supplied asset identities. |
| Verification | Select relevant `project/tests/` coverage; inspect [run_retrigger_checks.py](../tools/p6/run_retrigger_checks.py) before adapting it. Some old whole-journey fixtures have superseded assumptions; a historical filename is not proof of current coverage. |

## Verification and known limits

Use fresh disposable project copies and redirect `APPDATA`/`LOCALAPPDATA` before import or launch. Keep Adventure, Practice, Practice-core, legacy and epoch-marker test paths distinct and isolated. Verify the actual user-data root. Never read, hash, load or reset real player profiles or sibling Enigma data as fixtures. Do not launch old broad runners with their default profiles/rosters. The retrigger runner's reused-scratch path refreshes only selected directories; a fresh copy avoids stale assets/config.

Run checks affected by the change; inspect actual rendered UI for visual work. Documentation-only edits need link/consistency checks, not a game regression campaign. Generated reports, scratch projects and user data are ignored by Git; detailed historical evidence is local and may be absent in a fresh clone.

Phase 6 qualification retained certificate-store, first-import, renderer-conversion, recursive-script metadata and rapid headless audio shutdown diagnostics with explicit limits. They are not declared fixed. No export readiness, power-loss durability, universal all-build balance or arbitrary-stall/pause/hot-reload lifecycle guarantee follows. If one becomes relevant, consult only the matching **T5 diagnostic row** in the [closed M11 record](P6M11_Regression_And_Closeout_Tracker.md#diagnostic-dispositions).

## Next-phase scope and documentation

Economic/resale review, broader trigger usability/headroom investigation and expanded balance work remain deferred. Observed resale profit is accepted baseline behavior pending the user's economic review, not automatically an exploit to patch. These are candidate concerns, not an inherited mandatory checklist. Define the next phase with the user before assigning milestones or changing policy.

Keep **one active phase plan/tracker** for goals, decisions, tasks and acceptance. Update this handoff in place when ground truth changes. Put exact formulas in their owning code/reference, not copies across status documents. Create a separate design document only for a substantial specification that needs one; keep test attempts and execution logs in reports. Completed plans become history, not additional onboarding requirements. Preserve tool-consumed files and stable paths when archiving.

For a new conversation:

> Read `docs/Next_Phase_Handoff.md` first. Treat the accepted implementation as the baseline. Do not load Phase 6 history unless my task needs a specific reference. My next task is: …
