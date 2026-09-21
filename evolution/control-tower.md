# AI Control Tower, evolution

## Objectives
- O1 Every project governed, residency clean, nothing outside the root
- O2 Two human steps per requirement: one pick and ten minutes
- O3 Decided once here, dispatched everywhere, never re-decided per project

## Next release: v0.1.0, M0
- [x] S-001 Set the root and confirm it with Yassir  (O1)  2026-09-20
      Confirmed by Yassir, recorded in config.yml as root_confirmed_by/on
- [ ] S-002 git init _tower, first commit, private GitHub remote  (O1) (est S)
      2026-09-20: init, .gitignore and first commit 497b217 done, C1 to C4, C7, C8 met.
      Handle YBellout recorded, origin set to personalai-tower. C5 and C6 still open:
      no push has ever succeeded, no origin/main. Waiting on Yassir's repo, token and
      connect-github.command. A push cannot be tested from the Claude VM, osxkeychain.
- [ ] S-003 Heartbeat scheduled task: wake, read, append an event, commit, push,
      write a handover  (O2) (est M)
      X-001 granted. S-003a accepted 2026-09-20, launchd agent every 30 minutes.
      S-003b built and installed. launchd fires on schedule, 22 runs by 23:46, but
      every automatic run is blocked by macOS privacy protection before the script
      starts. Fixed by S-015 per D-017. S-014 and S-015 before S-004.
- [ ] S-004 Run it three nights unattended, nobody touching the Mac  (O2) (est S)
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

## Pulled forward from M1
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

## Evolutions, backlog (D-016)
Bug fixes and feature evolutions from stories. Each one tagged. Not in the M0 count,
not before S-004 unless Yassir pulls one forward, as he did S-012.
- [ ] S-013 feature  Raw-note intake UI in the Tower UI (dev/ui): one text field where
      Yassir drops unstructured notes, and the page runs the D-007 flow in the browser,
      correct, restructure, clarify (at most three questions), validate, then hands the
      validated prompt on. Replaces doing intake in chat. (O2)  added 2026-09-20 on
      Yassir's instruction. Story file: "AI Control Tower/docs/stories/S-013-raw-note-intake-ui.md".
      Design file owed before any code, per policy/self-governance.md.
- [ ] S-014 bug      heartbeat.sh does not handle a stale .git/index.lock: an abandoned
      lock (seen twice on 2026-09-20, once by the 18:20 session, once by the 21:30 one)
      blocks its commit every 30 minutes until someone deletes the file by hand.
      Remove a lock older than a few minutes with no git process holding it, and say
      so in the report. Belongs before S-004 starts. (O2)  added 2026-09-20.
      Design file proposed 2026-09-20 21:55, awaiting Yassir:
      "AI Control Tower/docs/S-014-stale-lock-design.md".
- [ ] S-015 bug      Unattended runs cannot enter ~/Documents. Diagnosed 2026-09-20 from
      bus/reports/heartbeat-diagnostic-2026-09-20-234628.txt: launchd ran the heartbeat
      22 times on schedule, every automatic run died before line 1, exit 126, macOS
      privacy protection. Fix per D-017: one granted runner app as the single entry
      point for every unattended job, plus a liveness file and a dead-man check in the
      status. Design proposed 2026-09-20 23:55, awaiting Yassir:
      "AI Control Tower/docs/S-015-runner-design.md". Blocks S-004. (O2)

## Operations (D-016)
Runs the Tower owns. Unchanged code, evidence in bus/.
- heartbeat, every 30 minutes under launchd on the Mac (S-003b, X-001). Evidence:
  bus/events.log, bus/heartbeat/last-success, bus/handover/*-heartbeat.md. Not yet
  proven to wake by itself.
- nightly audit, promote, backup: not built, M1 and later.

Exit test for M0: three clean nights. If it fails, orders become numbered launchers
Yassir starts before bed and nothing else in the design changes.

S-005 to S-008 and S-010 are documents. They change nothing on disk outside _tower, adopt no
project and move no file, so they are inside the hold that M0 imposes.

## Open decisions
- D-004 Ratchet permissions to deny-by-default. Trigger: the Mac mini goes live
  behind Cloudflare Access. Not a date.

Derogations live in decisions/derogations.yml, not here. Two are live, both granted by
Yassir on 2026-09-20. X-001, the heartbeat runs from dev/, closes when M1's promote.sh
promotes it, which D-013 makes the same event as M1's exit test. X-002, the dev UI built
past the M0 hold, closes when S-004 passes.

## Accepted decisions
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
