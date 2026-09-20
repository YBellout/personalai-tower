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
      C5 and C6 blocked by D-002: Yassir has no GitHub account set up on this Mac yet,
      he has to create one or look his up
- [ ] S-003 Heartbeat scheduled task: wake, read, append an event, commit, push,
      write a handover  (O2) (est M)
      X-001 granted 2026-09-20. S-003a design file written 2026-09-20, awaiting
      Yassir's acceptance: "AI Control Tower/docs/S-003-heartbeat-design.md"
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

Exit test for M0: three clean nights. If it fails, orders become numbered launchers
Yassir starts before bed and nothing else in the design changes.

S-005 to S-008 and S-010 are documents. They change nothing on disk outside _tower, adopt no
project and move no file, so they are inside the hold that M0 imposes.

## Open decisions
- D-002 GitHub account for the private remotes. Shape answered 2026-09-20: an
  existing personal account of Yassir's, private repos, credential in Keychain as
  personalai.github. The handle itself is still missing, so config.yml git.account
  is empty and S-002's push is blocked, along with step 5 of adoption for every
  project. Closes when the handle is filled in and the first push succeeds.
- D-003 Local mirror destination. Blocks the first backup run, and step 3 of the
  adoption pipeline, the frozen copy, for every project. Not an M0 blocker.
  Recommendation on the table: an external drive if one exists, otherwise
  ~/PersonalAI-mirror on the internal disk, enabled rather than written and disabled.
- D-004 Ratchet permissions to deny-by-default. Trigger: the Mac mini goes live
  behind Cloudflare Access. Not a date.
- D-006 Folder grants for the stray scan. config.yml names ~/Desktop, ~/Documents,
  ~/Downloads and ~/Developer. The Tower has a grant to none of them, so residency
  is unverifiable for every project not already under the root. Not an M0 blocker.
  Finding 2026-09-20: ~/Developer does not exist on this Mac, so the grant is over
  three locations and that fourth line should be dropped from config.yml.
- D-013 M1's exit test. Raised by D-005. The test as written assumes a project with
  code, and D-012 puts a docs-only project second. Either M1 keeps a code project as
  the subject of its exit test, or the test is rewritten. An M1 question, not an M0
  one.

Derogations live in decisions/derogations.yml, not here. X-001 was granted by Yassir
on 2026-09-20 and no longer blocks S-003. Its closing trigger stands: M1 delivers
bin/promote.sh, the heartbeat is promoted, the derogation closes.

## Accepted decisions
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
