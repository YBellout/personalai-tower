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
