# Handover, 2026-09-21 08:20

**What.** Yassir picked all three of S-016's open items directly in this chat, as
short control answers: proceed to smoke check when health.tests is empty, prune past
five archives without a derogation, refuse promote when health.smoke is empty.

**What changed.**
- edit "AI Control Tower/docs/stories/S-016-promote-rollback-design.md" in the working
  tree, "Needs a decision" folded into "Decided", steps 1 and 6 updated to match.
  **Not committed**, see below.
- edit bus/reports/control-tower/evolutions/O-0002.report.yml, the three picks moved
  from needs[] to decided[], next[] now names the two real blockers.

**What went wrong.** The first commit (d3c69d4, the original S-016 design) succeeded
but could not unlink its own tmp objects, leaving `.git/HEAD.lock` behind in the
evolutions clone. The second commit, folding in Yassir's picks, then refused outright:
"cannot lock ref 'HEAD'". device_request_delete_permission was called for
~/Documents/PersonalAI and reported success, but both `rm` and `mv` still failed with
"Operation not permitted" on `.git/HEAD.lock`, and a later `git status` left a second
stuck lock, `.git/index.lock`. Stopped retrying per the git-locks rule rather than
create more of them.

**Verified before writing.** Nothing lost: d3c69d4 is a real commit with the original
design. The picks are safe in the working tree and in this handover and the report,
just not yet in a commit.

**What it opens.** Whoever next holds delete access that actually works in this
folder, or the control room on its own session, removes `.git/HEAD.lock` and
`.git/index.lock` from `AI Control Tower/.chats/evolutions/.git/`, then commits the
already-edited design file. There is also one stray untracked file to remove first,
`AI Control Tower/.chats/evolutions/docs/stories/_delete_test.txt`, a permission probe,
harmless, not part of the design.

**What is left.** S-016 stays open, design proposed but not fully committed. Per
O-0002's order_of_work this does not block S-018, next.

**Read first next time.** this file, then
bus/reports/control-tower/evolutions/O-0002.report.yml.
