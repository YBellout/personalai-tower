# AI Control Tower, evolution

## Objectives
- O1 Every project governed, residency clean, nothing outside the root
- O2 Two human steps per requirement: one pick and ten minutes
- O3 Decided once here, dispatched everywhere, never re-decided per project

## Release v0.1.0, M0, "R1". 13 stories, 8 done
Redefined 2026-09-20 on Yassir's validation, D-018: S-014 and S-015 pulled in, because
M0 cannot pass without them. Exit test unchanged: three unattended days, each with a
commit and a push. Tags: [bugs] and [evolutions] name the work chat that holds it.

Open, in the order they unblock each other:
- [ ] S-015 bug  [bugs] Unattended runs cannot enter ~/Documents. Diagnosed 2026-09-20 from
      bus/reports/heartbeat-diagnostic-2026-09-20-234628.txt: launchd ran the heartbeat
      22 times on schedule, every automatic run died before line 1, exit 126, macOS
      privacy protection. Fix per D-017: one granted runner app as the single entry
      point for every unattended job, plus a liveness file and a dead-man check in the
      status. Design proposed 2026-09-20 23:55, awaiting Yassir:
      "AI Control Tower/docs/S-015-runner-design.md". Blocks S-004. (O2)
- [ ] S-014 bug  [bugs] heartbeat.sh does not handle a stale .git/index.lock: an abandoned
      lock (seen twice on 2026-09-20, once by the 18:20 session, once by the 21:30 one)
      blocks its commit every 30 minutes until someone deletes the file by hand.
      Remove a lock older than a few minutes with no git process holding it, and say
      so in the report. Belongs before S-004 starts. (O2)  added 2026-09-20.
      Design file proposed 2026-09-20 21:55, awaiting Yassir:
      "AI Control Tower/docs/S-014-stale-lock-design.md".
- [ ] S-002 [control room] git init _tower, first commit, private GitHub remote  (O1) (est S)
      2026-09-20: init, .gitignore and first commit 497b217 done, C1 to C4, C7, C8 met.
      Handle YBellout recorded, origin set to personalai-tower. C5 and C6 still open:
      no push has ever succeeded, no origin/main. Waiting on Yassir's repo, token and
      connect-github.command. A push cannot be tested from the Claude VM, osxkeychain.
- [ ] S-003 [control room] Heartbeat scheduled task: wake, read, append an event, commit, push,
      write a handover  (O2) (est M)
      X-001 granted. S-003a accepted 2026-09-20, launchd agent every 30 minutes.
      S-003b built and installed. launchd fires on schedule, 22 runs by 23:46, but
      every automatic run is blocked by macOS privacy protection before the script
      starts. Fixed by S-015 per D-017. S-014 and S-015 before S-004.
- [ ] S-004 [control room] Run it three nights unattended, nobody touching the Mac  (O2) (est S)

Done:
- [x] S-001 Set the root and confirm it with Yassir  (O1)  2026-09-20
      Confirmed by Yassir, recorded in config.yml as root_confirmed_by/on
- [x] S-005 Per-project link prompt, docs/PROJECT_LINK_PROMPT.md  (O3)  2026-09-20
- [x] S-006 Self-governance clause and derogation register  (O3)  2026-09-20
- [x] S-007 Registry stubs for every candidate project, status unmanaged  (O1)  2026-09-20
- [x] S-008 Per-project launch plan, docs/LAUNCH_PLAN.md  (O3)  2026-09-20
- [x] S-009 D-007 prompt intake protocol, written, folded into knowledge/operator.md
      and into the pasted block for every project  (O2, O3)  2026-09-20
- [x] S-010 D-014, the link prompt carries its own precondition and a not-adopted
      stop clause, applied to docs/PROJECT_LINK_PROMPT.md and to the Tower's own
      docs/PROJECT_INSTRUCTIONS.md in the same release  (O3)  2026-09-20
- [x] S-011 D-015, status spec knowledge/status.md, data contract status/status.json,
      side doc regenerated under the fixed layout  (O2)  2026-09-20
      The HTML rendering of the same data is M1, with status.py

## Next release v0.2.0, M1. 8 stories, all feature, all [evolutions]
Starts building only when S-004 passes. Designs are written now, under order O-0002.
Exit test, D-013: the Tower itself. Break heartbeat.sh in dev and watch promote refuse,
promote a good change, roll it back, and the heartbeat still runs. S-021 is that event,
and it also closes X-001.
- [ ] S-016 feature  [evolutions]  promote.sh and rollback.sh, with the sha256 release
      manifest in prod/ that D-009 requires. Everything else in M1 leans on it.
- [ ] S-017 feature  [evolutions]  brief.sh <project>, the generated opener under 60
      lines. Retires docs/OPEN_SESSION_PROMPT.md and the per-chat prompts.
- [ ] S-018 feature  [evolutions]  status.py generates status/status.json from the hub,
      so the status stops being hand-written. Absorbs S-015's dead-man check on
      bus/heartbeat/alive.
- [ ] S-019 feature  [evolutions]  audit.py, nightly through the runner: residency,
      policy drift, derogation expiry, stale claims, and the dispatch checks that close
      D-007, D-014, D-016 and D-018.
- [ ] S-020 feature  [evolutions]  mirror.sh, incremental sha256 mirror to the D-003
      target. Needs Yassir's answer on the external drive.
- [ ] S-021 feature  [evolutions]  promote heartbeat.sh and run-operations.sh from dev/
      to prod/ with promote.sh. M1's exit test, closes X-001.
- [ ] S-022 feature  [evolutions]  adopt platform-architecture, adoption steps 1 to 8,
      the docs-only rehearsal of the pipeline. First project adopted after the Tower.
- [ ] S-023 feature  [evolutions]  private remote for the "AI Control Tower" repo,
      personalai-control-tower, so the Tower's own code has an offsite copy.

## Later, M3, the UI
- [ ] S-012 UI server basis, AI Control Tower/dev/ui (Flask app + templates, reads
      status/status.json under the fixed layout from knowledge/status.md)  2026-09-20
      Not an M0 story: v0.1.0-plan.md says "no UI is built" in this release, so this
      is dev-only scaffolding, out of the story count above, doesn't touch the exit
      test. Flagged to Yassir before starting, built now on his answer. Design file:
      AI Control Tower/docs/S-012-ui-server-design.md, accepted same day via the
      control room's interactive intake. Smoke-tested against the live status.json
      (index and /api/status both render). Launcher: launchers/start-ui.command.
      Out of conformance with the M0 hold on Yassir's answer, recorded as X-002 on
      2026-09-20, closing when S-004 passes. Committed in the "AI Control Tower" repo,
      919315b, which did not exist before 2026-09-20 21:55.
- [ ] S-013 feature  [evolutions] Raw-note intake UI in the Tower UI (dev/ui): one text field where
      Yassir drops unstructured notes, and the page runs the D-007 flow in the browser,
      correct, restructure, clarify (at most three questions), validate, then hands the
      validated prompt on. Replaces doing intake in chat. (O2)  added 2026-09-20 on
      Yassir's instruction. Story file: "AI Control Tower/docs/stories/S-013-raw-note-intake-ui.md".
      Design file owed before any code, per policy/self-governance.md.

## Operations (D-016)
Runs the Tower owns. Unchanged code, evidence in bus/. No chat holds them: after S-015
every one is dispatched by the runner, run-operations.sh, per D-017.
- heartbeat, every 30 minutes under launchd (S-003b, X-001). launchd fires on schedule,
  macOS blocks every automatic run until S-015 ships.
- audit, mirror, status generation: v0.2.0, S-018 to S-020.

## Work chats (D-018)
- Control room, this project's standing chat: shared files, merges, dispatch, status.
- Bugs, "AI Control Tower, Bugs": [bugs] stories, L1, clone .chats/bugs. Order O-0001.
- Evolutions, "AI Control Tower, Evolutions": [evolutions] stories, L2, design only
  until S-004, clone .chats/evolutions. Order O-0002.
Prompts: _tower/docs/CHAT_PROMPT_BUGS.md and CHAT_PROMPT_EVOLUTIONS.md.

If M0 fails, orders become numbered launchers Yassir starts before bed and nothing else
in the design changes.

## Open decisions
- D-004 Ratchet permissions to deny-by-default. Trigger: the Mac mini goes live
  behind Cloudflare Access. Not a date.

Derogations live in decisions/derogations.yml, not here. Two are live, both granted by
Yassir on 2026-09-20. X-001, the heartbeat runs from dev/, closes when M1's promote.sh
promotes it, which D-013 makes the same event as M1's exit test. X-002, the dev UI built
past the M0 hold, closes when S-004 passes.

## Accepted decisions
- D-018 Two work chats in parallel, Bugs and Evolutions, splitting D-016's Evolutions
  stream by tag. Control room sole writer of shared files, claims per chat, one clone
  per chat. R1 redefined to 13 stories. Answered 2026-09-20. decisions/D-018.md.
- D-017 Unattended jobs enter the hub through one granted runner app, the single entry
  point for every Operations run. Full Disk Access for bash and moving the hub were
  both rejected. Answered 2026-09-20. decisions/D-017.md, story S-015.
- D-013 M1's exit test runs against the Tower itself. Promoting heartbeat.sh through
  promote.sh is also what closes X-001, so the two are one event. Platform Architecture
  runs alongside as the docs-only rehearsal. Answered 2026-09-20. decisions/D-013.md.
- D-006 Stray-scan grants over ~/Desktop, ~/Documents, ~/Downloads, requested when the
  scan first runs at M1. ~/Developer dropped, it does not exist. Answered 2026-09-20.
- D-003 Local mirror: an external drive if one exists, otherwise ~/PersonalAI-mirror.
  Answered 2026-09-20, one fact outstanding, whether the drive exists. Nothing is
  mirrored until mirror.sh at M1.
- D-016 Two work streams, Operations (batch and execution runs) and Evolutions (bug
  fixes plus feature evolutions from stories), for the Tower and every governed
  project. Scope global, answered 2026-09-20. decisions/D-016.md. Applied to this map
  in the same commit, the two headings above. Closes on the M1 audit.
- D-015 The control room is the status dashboard. Status on the word `status` and after
  every step, read fresh, one fixed layout, data in status/status.json for the future
  UI. Answered 2026-09-20. decisions/D-015.md, story S-011.
- D-002 GitHub account. Handle YBellout given 2026-09-20 and recorded in config.yml.
  Stays open until the first push succeeds (repo personalai-tower, private).
- D-014 The link prompt is pasted at adoption step 8, and says so. Scope global,
  answered 2026-09-20 after it was pasted into four unadopted projects and all four
  could only ask questions. decisions/D-014.md, story S-010. Closes on the same audit
  check as D-007, at M1.
- D-001 Options A to E from the design handover. Answered 2026-09-20, all five taken
  as recommended, and closed by being split into one decision file each:
  D-008 project setup (A), D-009 folder and git layout (B), D-010 shared library
  scope (C), D-011 design system scope (D), D-012 onboarding sequence (E).
- D-005 "iExecAdmin". Answered 2026-09-20: out of scope, it is not a project this
  Tower governs. D-012 supersedes design sections 13 and 17 on the onboarding order.
  Consequence recorded as D-013.
- D-007 Prompt intake protocol, and marking generated prompts. Scope global,
  answered 2026-09-20. decisions/D-007.md. Live for control-tower, queued for every
  other project at adoption step 8. Closes when the audit confirms the marker line
  and the intake clause are present in every governed project's instructions.

## Released
Nothing yet.

## Abandoned
Nothing yet.
