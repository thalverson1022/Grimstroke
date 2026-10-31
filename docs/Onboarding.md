# Project Grimstroke Onboarding

Read this first when starting a job. It identifies the current context and where to look next; it is not a second project plan or progress report.

## Read in this order

1. **The user's current request.** Identify the requested outcome and any milestone/task ID. New user direction can change the plan; record material changes in the appropriate existing document.
2. **[Phase 7 Milestone Tracker](Phase_7_Milestone_Tracker.md).** Read the phase summary, relevant milestone, current tasks, blockers, and latest activity. This is the authority for what is started, finished, awaiting review, or next. Do not infer progress from this onboarding guide.
3. **[Game Scope](Game_Scope.md).** Read this short overview to understand the implemented game and its working boundaries.
4. **[Phase 7 Project Plan](Phase_7_Project_Plan.md).** On first joining the project, read the goal, player journey, town/expedition rules, and scope controls. Then read the sections for the assigned task and its dependencies. Read the full plan for phase-wide design or integration work; do not repeatedly preload unrelated sections for a focused change.
5. **Relevant code, data, and tests.** Use the entry points below. Search for affected symbols before opening large files, then follow their direct dependencies.

The plan describes intended behavior; it is not proof that a feature exists. Current code establishes implemented behavior, and the tracker records delivery and acceptance. If these disagree, identify the specific discrepancy rather than silently treating a proposal as implemented or reopening completed work.

## Project identity

- Workspace: `F:\Data\Claude Projects\Project-Grimstroke`
- Repository: [thalverson1022/Grimstroke](https://github.com/thalverson1022/Grimstroke); primary branch: `main`.
- Godot **4.7**; open [project.godot](../project/project.godot). Main scene: `project/scenes/game_root.tscn`.
- Windows player data: `%APPDATA%/Grimstroke/`. FacelessVoid and Enigma are separate projects with separate data.
- Starting snapshot: Grimstroke `34cfed5`, based on accepted FacelessVoid commit `b5ab445`.

Phase 7's direction is town-based preparation, new gold-spending services, lives and potions, and the Mountain Road to the White Dragon, followed by continued contracts. System design comes before final economic balancing. Exact rules, candidate features, and unresolved choices belong to the plan.

## Task-specific entry points

These are existing baseline entry points, not a required reading list or a mandate to place every new system in them. Search for newer implementations as the phase progresses.

| Task area | Start here |
| --- | --- |
| Town navigation, Tavern, and expedition flow | [game_root.gd](../project/scenes/game_root.gd), [BuildState](../project/scripts/autoload/build_state.gd), [combat_screen.gd](../project/scenes/combat/combat_screen.gd) |
| Talent points, subclasses, and Weapon Master | [build_progression.gd](../project/scripts/systems/build_progression.gd), [build_resolver.gd](../project/scripts/systems/build_resolver.gd), [build_content_registry.gd](../project/scripts/systems/build_content_registry.gd) |
| Shop, gear, gold, and Blacksmith | BuildState's reward/shop transactions, [gear_generator.gd](../project/scripts/systems/gear_generator.gd), [stat_catalog.gd](../project/scripts/systems/stat_catalog.gd), `project/scripts/resources/`, `project/data/gear/` |
| Potion and blessing combat effects | [combat_resolver.gd](../project/scripts/systems/combat_resolver.gd), affected stat/effect resources, combat playback/UI consumers |
| Training | [training_room.gd](../project/scenes/training_room/training_room.gd), [training_room_state.gd](../project/scripts/systems/training_room_state.gd) |
| Contract maps and Mountain Road integration | [contract_route_generator.gd](../project/scripts/systems/contract_route_generator/contract_route_generator.gd), BuildState, affected map views; the mountain needs its own authored route rules |
| Lives, upgrades, and persistence | BuildState, [save_system.gd](../project/scripts/systems/save_system.gd), [practice_save_system.gd](../project/scripts/systems/practice_save_system.gd), [seven_slot_save_boundary.gd](../project/scripts/systems/seven_slot_save_boundary.gd) |
| Presentation and audio | Affected files in `project/scenes/`, `project/scripts/ui/`, and [audio_manager.gd](../project/scripts/autoload/audio_manager.gd); preserve supplied asset identities |
| Verification and tooling | Relevant `project/tests/` coverage and [run_retrigger_checks.py](../tools/p6/run_retrigger_checks.py), inspected before use; tool-specific READMEs under `tools/` |

The content registry identifies active builds. Some packaged resources and `tools/p6/fixtures/` serve legacy compatibility or historical tests; their names and descriptions are not current design instructions.

## Working on a job

- Check applicable repository instructions and `git status` before editing. Preserve unrelated pending changes.
- Match the task to its milestone and completion checkpoint. Do not start the next milestone merely because this guide names it.
- Resolve consequential open design choices with the user; do not silently turn candidate blessings, example numbers, or proposed policies into requirements.
- Include relevant UI, persistence, and focused verification with the change. Use actual rendered inspection for visual work. Documentation-only changes need link and consistency checks, not a game regression campaign.
- Before import or launch, use a fresh disposable project copy and redirect `APPDATA` and `LOCALAPPDATA`. Verify the actual user-data root and keep Adventure, Practice, Practice-core, legacy, and epoch-marker test paths distinct. Never read, hash, load, or reset real player profiles as fixtures.
- Inspect old runners before execution. Some require missing historical reports or contain superseded assumptions. Do not run broad legacy scripts with default player profiles. Existing engine diagnostics are not automatically new regressions or evidence of a clean bill of health.
- At completion, update the tracker with the outcome, relevant evidence, blockers, and next action. Update the plan only when design changes, and the game scope when implemented scope changes. Do not mark review-gated work complete before acceptance.

## Keep context small

Maintain four documents with distinct purposes: this onboarding guide for navigation, Game Scope for the implemented overview, the Phase 7 plan for design, and the milestone tracker for progress. Update them in place. Do not add task handoffs, per-milestone trackers, or duplicate status summaries unless explicitly requested.

Historical Phase 6 documents were intentionally removed. Retrieve a specific historical file from Git only to answer a concrete question that current source and documentation cannot resolve. Do not load the old documentation collection or copy it back into `docs`. Keep execution logs and generated evidence in ignored reports.

## Starting prompt

> Read `docs/Onboarding.md` and follow its reading order. Use the tracker for current progress, the game scope for the implemented baseline, and the relevant plan sections for intended behavior. My task is: **[milestone/task ID and requested outcome]**. Inspect only the source and tests needed for that task; do not preload Phase 6 history.
