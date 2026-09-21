# Handover, 2026-09-21 14:33

**Closing.** Evolutions chat, session ending this close-out. Not the control room,
wrote no shared file, no _tower commit, no merge. Read fresh at open: D-018, O-0002,
evolution/control-tower.md, every claims file, every decision, self-governance.md,
knowledge/ in full, the newest handover before this session, and the design doc
sections 1 to 18 (Claude Docs, live, rev 42).

## Done

- S-016 design written and committed, "AI Control Tower/docs/stories/S-016-promote-rollback-design.md",
  commit d3c69d4 on branch evolutions in AI Control Tower/.chats/evolutions.
- Its three open items put to Yassir directly in this chat and picked, 2026-09-21
  (evolutions-D1 to D3 below).

## In flight

The fold-in-picks edit to S-016's design file sits in the evolutions clone's working
tree, uncommitted. Two commits attempted and both left a stuck lock: the first
commit (d3c69d4) itself succeeded but could not unlink its own tmp objects; the
second refused outright on ".git/HEAD.lock", and the git status run to check it left
".git/index.lock" too. device_request_delete_permission reported delete enabled for
~/Documents/PersonalAI, but rm and mv both still failed "Operation not permitted" on
both lock files. Stopped rather than create more locks.

Revert path if this is abandoned rather than resumed: `git checkout --
docs/stories/S-016-promote-rollback-design.md` in that clone restores d3c69d4's
version (the "Needs a decision" form), and evolutions-D1 to D3 below carry the picks
that would need reapplying.

## Files touched

| File | State |
|---|---|
| AI Control Tower/docs/stories/S-016-promote-rollback-design.md | committed d3c69d4; working-tree edit on top, uncommitted |
| _tower/claims/control-tower.evolutions.yml | claimed for S-016, released after the report |
| _tower/bus/reports/control-tower/evolutions/O-0002.report.yml | new, outcome partial |
| _tower/bus/handover/2026-09-21-0815-evolutions-s016-design.md | new |
| _tower/bus/handover/2026-09-21-0820-evolutions-s016-picks-and-git-lock.md | new |
| AI Control Tower/.chats/evolutions/docs/stories/_delete_test.txt | stray, untracked, a permission probe, not part of any design |

## Pending

- evolutions-P1: commit the fold-in-picks edit once ".git/HEAD.lock" and
  ".git/index.lock" are cleared from AI Control Tower/.chats/evolutions/.git/.
- evolutions-P2: remove the stray _delete_test.txt from the same clone.
- evolutions-P3: resume O-0002's order_of_work at S-018, status.py, next per the order,
  independent of P1 and P2.

## Decisions

- evolutions-D1: S-016's promote proceeds to the smoke check rather than refusing
  outright when a project's registry declares no test suite. Picked by Yassir directly
  in this chat, 2026-09-21. Not yet a numbered D-0NN, that filing is the control
  room's, per D-018's "who writes what".
- evolutions-D2: pruning prod/ archive snapshots past five is not a self-governance
  delete, no derogation needed. Same status as D1.
- evolutions-D3: promote refuses with a named reason when no smoke check is declared,
  rather than skipping verification silently. Same status as D1. Consequence: writing
  control-tower's own dev/bin/smoke.sh now sits in front of S-021.

## Next

1. Clear the two stuck locks in AI Control Tower/.chats/evolutions/.git/, worth
   checking why the delete grant reported success but the filesystem still refused it.
2. Land evolutions-P1's commit.
3. Fold evolutions-D1 to D3 into a numbered decision, control room's write.
4. Resume at S-018 per O-0002, in this chat or a fresh one.

**Read first next time.** this file.
