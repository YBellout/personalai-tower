# Handover to the AI Control Tower project
Written 2026-09-20, at the end of two design sessions.

## Read these, in this order
1. This file.
2. The Control Tower design doc, sections 1 to 18 (the living source of truth,
   read it fresh, never from a cached summary):
   https://claude.ai/code/artifact/b73a4180-e88e-4b58-9702-9a5e2825829a
3. The AI Apps Platform doc, and in full its second tab "Control Tower Prompt":
   https://claude.ai/code/artifact/336e1b53-42d4-4e95-b03b-2e96c6e03c4b

Nothing from the design conversations crosses over except those two docs, the files
in this hub, and account-level memory. Do not expect a chat history to exist.

## Decided, do not re-derive

| Area | Decided |
|---|---|
| Hub root | ~/Documents/PersonalAI, MacBook Pro, local disk, never iCloud |
| Git | one repo per project, private GitHub remote as the offsite archive |
| Environments | dev/ and prod/ as two visible folders, git underneath |
| Mac mini | not ordered. Everything runs on the MacBook, prod/ is a folder for now |
| Transport to the mini | GitHub. When the mini exists it pulls from the private repos |
| Autonomy | options up front, one pick, then unattended, report at the end |
| Control UI | the FastAPI app with buttons, at M3, not before |
| Object model | the seven types only. R, D, S, O, release, F, handover |
| Backups | local mirror first, offsite target written but disabled |
| Permissions | allow with nightly audit; ratchet to deny-by-default when the mini
  goes live behind Cloudflare Access. Trigger, not a date |
| Pilot | the Tower governs itself first. No files of Yassir's at risk |
| Launch cut | M0 to M6, each gated by its exit test (design doc, section 17) |

## Still open, decide these first
Proposed but never answered. Recommendations below, all reversible.

- **A. claude.ai project setup.** Recommended: Tower project plus one project per
  app, each app keeping its own control room chat. Tower instructions hold rules
  only; its project knowledge holds pointers, never content.
- **B. Folder and git layout.** Recommended: the repo lives in dev/; prod/ is a plain
  copy written only by promote, tagged in git, never edited, and maps one-to-one onto
  a container image when the mini arrives.
- **C. Shared library starting scope.** Recommended: four modules that have consumers
  today, app skeleton, atomic storage, paced HTTP client, LLM wrapper with budget.
  Portal client, Postgres helper, Access check and PWA template are named but empty
  until the mini exists.
- **D. Design system starting scope.** Recommended: extract from the Virtual Closet
  UI. Tokens only in release one, then card grid, filter sidebar, status pill, then
  the Portal shell.
- **E. Onboarding sequence.** Recommended: the Tower itself, then AI Architecture
  Tower as docs-only, then Family School Dashboard, then Virtual Closet last. The
  Closet is the most valuable and the worst thing to restructure with an unproven
  process: 40,000 photos, no git today, and live work in flight.

## What is missing and must be asked for
- D-002 the GitHub account for the private remotes. Blocks the first commit.
- D-003 the local mirror destination, a second local place outside the root.
- The root path itself is set in _tower/config.yml. Confirm it before M1 moves
  any real file, because that is the last moment it is free to change.

## Two caveats carried with the permission decision
- The Virtual Closet's supplier crawling still needs an enforced pace limit in code.
  That is about not being blocked, not about security, so allow-audit does not cover it.
- The deny-by-default ratchet is triggered by the mini going live, and is logged as
  D-004 in the Tower's evolution map so it cannot quietly disappear into setup.

## What already exists in this hub
Created 2026-09-20, before any code:

    _tower/config.yml                 the root and every other single value
    _tower/registry/control-tower.yml the Tower as its own first governed project
    _tower/knowledge/                 operator, conventions, ui, glossary, domain
    _tower/evolution/control-tower.md objectives, M0 stories, open decisions
    _tower/policy/control-tower.yml   allow-audit, observed lists to be filled
    _tower/architecture/README.md     the platform snapshot and the five duties
    _tower/bus/                       orders, reports, feedback, handover
    _tower/bin/README.md              what M0 and M1 must create, in order
    AI Control Tower/{dev,prod,...}   the Tower's own project folders, empty

Nothing here is code. M0 writes the first line of that.

---

# Update, 2026-09-20, close of the build session

Appended at the close of the session that followed this file. Everything above still
stands. This section says what changed since, and what a new chat must not miss.

## A to E, reviewed

The recommendations above were reviewed and agreed. Still unanswered, still D-001.
Four notes belong with the picks and exist in no other file:

- **A.** Agreed, and already acted on: the pasted block was cut down to pointers plus
  the non-negotiables, because a rule written into claude.ai instructions can never
  be changed by the Tower and costs a re-paste into every project to correct. See
  docs/PROJECT_LINK_PROMPT.md.
- **B.** Agreed, with one addition. prod/ sits outside git and so has no integrity
  check of its own. promote must write a sha256 release manifest into prod/.
- **C.** Agreed, no reservation. The second-use rule already protects the scope.
- **D.** Agreed, with a sequencing caveat. Extracting tokens from the Virtual Closet
  UI is read-only and can happen at any time, but no app may take the design system
  as a dependency until the Closet is governed, or the shared look has an ungoverned
  source of truth.
- **E.** Agreed. Design doc sections 13 and 17 give a different order and name a
  project, iExecAdmin, that exists nowhere. Logged as D-005.

## New since this file was written

    docs/PROJECT_LINK_PROMPT.md     the block that binds a project to the Tower
    docs/OPEN_SESSION_PROMPT.md     the per-session opener, stands in for brief.sh
    docs/LAUNCH_PROMPT_v0.1.0.md    the inaugural control room message
    docs/LAUNCH_PLAN.md             next steps and blockers, per project
    policy/self-governance.md       the Tower bound by everything it enforces
    decisions/derogations.yml       the exception register. X-001 proposed, not granted
    decisions/D-007.md              prompt intake, and marking generated prompts
    registry/*.yml                  four stubs at status unmanaged, verified facts only
    bus/handover/                   five entries. The newest is the true current state

docs/PROJECT_INSTRUCTIONS.md was rewritten: the Tower now runs on the same block it
hands to the projects it governs.

## Findings from the first read-only scan of the hub

- Only two things under the root: the empty Tower scaffold, and PersonalShopper at
  4.0 GB across 40,060 files.
- No git repository anywhere under the root. The `.bak-<timestamp>` habit is doing
  that job today.
- `.env` secrets on disk beside the Closet code. Finding VC-F1 in the registry stub.
- Family School Dashboard, Architecture Tower and Home Assistant are not under the
  root at all, and the Tower holds a folder grant to none of the four stray-scan
  locations in config.yml, so residency is unverifiable for them. Logged as D-006.

## Still blocked, all of it

D-001 A to E, D-002 GitHub account, D-003 mirror destination, X-001 grant or deny,
D-005 iExecAdmin, D-006 stray-scan grants, and the root path confirmation. No part of
M0 can start until they are answered.

## One writer

From 2026-09-20 the control room chat is the single writer to this hub. The session
that appended this section is closed and writes nothing further.

---

# Update, 2026-09-20, close of the S-012 session

Appended at the close of the control room session that built the UI basis. Everything
above still stands. This section says what changed since the last close, and what a
new chat must not miss.

## What this session did

- Flagged, before starting, that v0.1.0-plan.md says "no UI is built" in M0. Yassir
  answered via the interactive intake: build it now anyway, as dev scaffolding that
  doesn't touch the M0 exit test. Design note:
  `AI Control Tower/docs/S-012-ui-server-design.md`, accepted the same way.
- Built S-012, the UI server basis: `AI Control Tower/dev/ui/` (Flask app, templates,
  CSS), reads `_tower/status/status.json` under the fixed layout `knowledge/status.md`
  defines. Launcher: `AI Control Tower/launchers/start-ui.command`.
- Found, and fixed, a real bug: the first version opened the browser at a hardcoded
  port regardless of whether the server actually bound it, so a port collision with
  another of Yassir's local apps (the Family School Dashboard, on 8787) sent him to
  that app's page instead. Fixed by having the app probe for a free port and open its
  own browser tab only once it knows which one it actually bound. Verified against a
  simulated collision, not just read over.
- While regenerating status per D-015, found `status/status.json` was stale (from
  before Yassir gave his GitHub handle). Refreshed it and the side doc
  (https://claude.ai/code/artifact/20928a96-0eea-4492-a661-13d95e25b464) against
  freshly read sources, not carried forward from memory.
- `evolution/control-tower.md` gained a "Pulled forward from M1" section for S-012,
  kept out of the v0.1.0 story count on purpose.
- Three handover entries this session, newest first as always in `bus/handover/`:
  S-012 port fix, S-012 UI server basis, D-015/S-011 status feature (that last one
  predates this session but was the most recent before it).

## True current state, verified this session, not carried forward

- `git remote -v` in `_tower` shows `origin -> https://YBellout@github.com/YBellout/personalai-tower.git`,
  set locally. No `origin/main` ref exists anywhere, `git fetch` fails from this VM
  (`credential-osxkeychain` unreachable here, exactly as the M0 ground truth says). No
  evidence anywhere of a successful push. S-002's three remaining actions (create the
  repo, create the token, run `connect-github.command`) are unchanged and still open.
- No heartbeat diagnostic has been run yet (`bus/reports/` is still empty except
  `.keep`). Action 1 in "your actions" is still open too.
- M0 is still 8 of 11 stories done, exit test at 0 of 3 days. Nothing in this session
  changed that; S-012 is explicitly not one of the 11.
- `AI Control Tower` still has no git repo of its own (only `_tower` does, per S-002's
  own note: "M0 does the first"), so `dev/ui`, the new launcher and the design file
  are not under version control anywhere yet.

## New since the last close

    "AI Control Tower/dev/ui/"                      app.py, templates, static, README
    "AI Control Tower/launchers/start-ui.command"    starts the UI
    "AI Control Tower/docs/S-012-ui-server-design.md"
    bus/handover/*-s012-ui-server-basis.md
    bus/handover/*-s012-port-fix.md
    evolution/control-tower.md   "Pulled forward from M1" section

## Still blocked, unchanged by this session

D-002's push (handle is filled, the three GitHub actions are not done), D-003 mirror
destination, D-004 ratchet trigger (not due), D-006 stray-scan grants, D-013 M1's exit
test question. None of these are S-012's to resolve.

## One writer

This session is closed and writes nothing further. The next chat opens with
`_tower/docs/OPEN_SESSION_PROMPT.md`, reads the newest handover by mtime (this
section's own entry point, `bus/handover/`), and becomes the writer.
