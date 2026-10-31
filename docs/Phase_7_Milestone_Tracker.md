# Phase 7 Milestone Tracker

Updated: 2026-10-31.

**Phase status: Planning. Completed milestones: 0 of 8. Active milestone: None. Next milestone: M1.**

The initial project draft and milestone breakdown are prepared. Detailed system design and implementation have not started. Creating this tracker does not complete M1.

The [Phase 7 project plan](Phase_7_Project_Plan.md) owns feature rules, scope, and unresolved design questions. This tracker owns milestone status, current tasks, blockers, evidence, and acceptance. The [Game Scope](Game_Scope.md) remains the short implemented-game overview.

## Milestones

| ID | Milestone | Status | Completion checkpoint |
| --- | --- | --- | --- |
| M1 | System design and progression rules | Not started | Resolve major behavioral gaps, bound the initial service/potion/blessing content, define mountain route and boss roles, and agree on state/data changes and save compatibility. User reviews the design before implementation. Prices can remain provisional. |
| M2 | Town, Tavern, and expedition flow | Not started | A fresh run reaches town, completes the revised tutorial, reserves and enters contracts, and returns to town. Global lives, retry, flee to the map, free abandonment, and zero-life run termination work. The automatic shop transition is removed. |
| M3 | Weapon Master and character progression | Not started | First-contract secondary choices are fixed, saved, and claimed once at the Weapon Master. Full respecs retain subclass identities, escalate in cost, and remain free during the tutorial. Unspent points can be spent anywhere. Current-build training has adjustable targets and no run-resource side effects. |
| M4 | Shop, potions, and Alchemist | Not started | Gear/potion purchases and resale, separate stock, contract-boss refreshes, paid gear rerolls, potion capacity/use, life services, and agreed run upgrades work through save/load. Abandonment and mountain bosses do not refresh stock; gear rerolls do not affect potion offers. |
| M5 | Blacksmith and Cathedral | Not started | Selected-slot rerolls, weighted one-time forging, item locks, separate stat/forge ranges, sacrifices, transformations, blessing durations, and the approved initial tables work. Legendary effects cannot be forged. Tithe changes within-block odds only. Transactions resolve once and persist correctly. |
| M6 | Mountain Road and victory | Not started | The fixed inspectable ascent includes Boarcerotops, the agreed route/bosses, and White Dragon. Encounters award nothing; abandoning resets the ascent. Defeat and retreat obey life rules. Victory is recorded and shown, then the same run can continue contracts. User reviews the complete functional loop. |
| M7 | Economic audit and integrated balance | Not started | Evaluate and tune income, deeper-contract rewards, prices, resale, rerolls, respecs, life recovery, upgrades, forging, and tithes together. Representative runs demonstrate meaningful spending and a viable route to mountain readiness. Farming and economic build advantages follow deliberate policies. User reviews tuning. |
| M8 | Integrated playtest, polish, and acceptance | Not started | Complete the journey through mountain victory and continued contracts. Verify cross-system persistence and interactions, finish scoped presentation/guidance, and resolve blocking defects. User accepts the phase with explicit remaining limitations. |

Default sequence: **M1 → M2 → M3 → M4 → M5 → M6 → M7 → M8**. Adjust only when a dependency or agreed scope change justifies it; record the reason here. Mountain difficulty is outlined in M1 and tuned in M7. Each implementation milestone includes its own interface, persistence, and focused verification; these are not postponed wholesale to M8.

## Next work: M1

All tasks below are not started. Resolve rules in the existing project plan rather than creating separate specifications by default.

- [ ] **M1-T1 — Flow and lives:** settle encounter/map transitions, route availability after fleeing, contract reservation during mountain trips, initial stock, tutorial rewards, and run-end behavior.
- [ ] **M1-T2 — Service rules:** settle respec escalation, Alchemist upgrade limits and life restoration, Blacksmith eligibility and roll ranges, and post-blessing item locks. Define pricing rules without final gold amounts.
- [ ] **M1-T3 — Initial content:** bound the potion and blessing lists; define stacking, caps, duration/consumption, transformation eligibility, block selection, and tithe behavior. Mark candidate features as included or deferred.
- [ ] **M1-T4 — Mountain design:** agree on the fixed route, enemy roles, target readiness, victory continuation, and repeat-ascent behavior. Identify required art and interface work.
- [ ] **M1-T5 — Data and persistence:** map ownership of lives, stock, pending rewards, upgrades, item roll components, consumables, blessings, and expedition state. Agree on existing-save handling before implementation; this tracker authorizes no save reset.
- [ ] **M1-T6 — Design review:** reconcile the plan, check dependencies and scope limits, and obtain user acceptance of the implementation-ready design.

Expand later milestones into a short task list when they become next. Do not create a speculative backlog of every possible implementation detail now.

## Review gates

| Gate | Purpose | State |
| --- | --- | --- |
| After M1 | Approve bounded behavior, content, and data/save design | Pending |
| After M6 | Review the complete functional town → preparation → mountain → continued-contract loop | Pending |
| After M7 | Review economy and progression tuning | Pending |
| After M8 | Accept Phase 7 and its documented limitations | Pending |

## Blockers and unresolved decisions

**Blocking issues: None identified during planning.** The project plan's remaining decisions are scheduled M1 design work, not completed decisions or current technical blockers.

When a blocker appears, record its milestone/task, impact, and concrete next action here. Remove resolved blockers from the active list and retain only a concise resolution in the activity record.

## Activity and acceptance record

| Date | Milestone | Update | Evidence or acceptance |
| --- | --- | --- | --- |
| 2026-10-31 | Planning | Prepared the Phase 7 draft from the agreed discussion and established eight milestones. Created this tracker at the user's request. | [Project plan](Phase_7_Project_Plan.md). Detailed design and implementation remain not started. |

## Tracking rules

- Use **Not started**, **In progress**, **Blocked**, **Ready for review**, or **Complete**. Completed work must meet its checkpoint, have relevant verification, and satisfy any listed review gate.
- Update the summary, milestone row, and current task list together. Keep only one milestone as the default active focus; record any deliberate overlap.
- Link commits and concise test evidence when available. Keep raw execution logs and generated reports in ignored report folders; do not paste them here.
- Record material decisions and acceptance briefly. Update the actual design in the project plan rather than duplicating it in the tracker.
- Use isolated disposable test copies and redirected user-data paths. Never test against real player saves.
- Keep one tracker for the entire phase. No per-milestone trackers, closeout packets, or extra handoffs unless explicitly requested.
