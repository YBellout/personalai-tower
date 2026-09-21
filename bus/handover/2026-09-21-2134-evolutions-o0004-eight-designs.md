# Handover, 2026-09-21 21:34, Evolutions chat

**What.** Order O-0004, complete: proposed designs for all eight of its stories,
S-018, S-019, S-020, S-017, S-021, S-022, S-023, S-013, each committed on its own
in `AI Control Tower/.chats/evolutions`, branch `evolutions`. Not the control room:
wrote no shared file, no `_tower` commit, no merge, no push, touched neither
`prod/` nor `dev/`.

**Opened cold, found clean.** Read D-018, this order, the evolution map, every
claims file, every decision, self-governance.md, knowledge/ in full, the newest
handover (`...170849-heartbeat.md`) plus the four before it for context, and the
design doc sections 1 to 18, fresh (the earlier read hit a reply cap; the
remainder, sections 17's phase table onward and all of 18, was fetched with a
follow-up `view` at the gap it left, so the whole document is now read, not just
what fit in one call). The prior session's own in-flight items (P1 to P3, D1 to D3
from the 14:33 evolutions close-out) were already cleared by the control room's
14:45 pass; nothing was left for this session to pick up before starting O-0004.

**Before any git**, requested delete permission for both connected folders and
proved it with a create-then-remove probe inside the clone, per the prompt. Then
`git fetch origin` and a fast-forward merge of `origin/main` into `evolutions`
(`c2348f8..9a854bf`, 10 commits: S-016's acceptance, S-024/S-025, the runner
installer), since the branch was behind main, per O-0004's own constraint.

## Done

Eight design files, `AI Control Tower/docs/stories/`, each `State: proposed`,
each naming its acceptance criteria and evidence in advance, the knowledge it
relies on, its dependencies and what it blocks, and which of its runs would go
through `run-operations.sh` per D-017. Commits `ec3eee3` through `b7c584f`, one
per design, in `order_of_work`'s own order.

Two design findings worth the control room's attention before the rest:

- **S-021** found that `v0.2.0-plan.md`'s own C3 evidence for this story, "the
  plist's path," does not hold: S-015's plist names the runner's `.app` bundle,
  not a script, so the fix is a front-door indirection (`dev/bin/run-operations.sh`
  becomes a five-line stub, never promoted; today's logic renames to
  `run-operations.impl.sh`), not a plist edit. Full reasoning in the design file.
- **S-020** found that the mirror's own configured fallback, `~/PersonalAI-mirror`,
  sits outside the runner app's granted folder (`~/Documents`) and would fail
  unattended the same way every pre-S-015 heartbeat run did. Recommends moving it
  to `~/Documents/PersonalAI-mirror`.

## Report

`_tower/bus/reports/control-tower/evolutions/O-0004.report.yml`, outcome
`complete`. Eighteen items at decision depth, one line each with a recommendation,
under `needs`; none decided live in this session, this was an async design pass,
not an interactive one. The control room's own filing of these into numbered
decisions is D-018's write, not this chat's.

## Files touched

| File | State |
|---|---|
| AI Control Tower/docs/stories/S-018-status-py-design.md | new, committed `ec3eee3` |
| AI Control Tower/docs/stories/S-019-audit-py-design.md | new, committed `0996eba` |
| AI Control Tower/docs/stories/S-020-mirror-sh-design.md | new, committed `382607f` |
| AI Control Tower/docs/stories/S-017-brief-sh-design.md | new, committed `e02764e` |
| AI Control Tower/docs/stories/S-021-promote-heartbeat-design.md | new, committed `e16b3e4` |
| AI Control Tower/docs/stories/S-022-adopt-platform-architecture-design.md | new, committed `da9d193` |
| AI Control Tower/docs/stories/S-023-private-remote-design.md | new, committed `60df09f` |
| AI Control Tower/docs/stories/S-013-raw-note-intake-ui.md | rewritten from its "not started" stub to a full proposed design, committed `b7c584f` |
| _tower/claims/control-tower.evolutions.yml | claimed for all eight stories at open, released in this handover |
| _tower/bus/reports/control-tower/evolutions/O-0004.report.yml | new |

## Pending

None blocking. The eighteen decision-depth items in the report are for the
control room and Yassir on their own schedule, not a stop condition for this
chat.

## Next

The control room reviews the eight designs and the report's `needs` list, files
the numbered decisions D-018 reserves to it, and either issues a build order once
S-004 passes or leaves these as the M1 backlog exactly as `v0.2.0-plan.md`
already has them. This chat's claims are released below; a closed chat holds
nothing.
