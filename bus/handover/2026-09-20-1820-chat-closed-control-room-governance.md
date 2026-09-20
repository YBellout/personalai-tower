# Handover, 2026-09-20 18:20

**What.** The first control room chat is closed at Yassir's request, and the hub is
handed to a new chat. Archive:
"AI Control Tower/archives/2026-09-20-chat-control-room-governance.md".

**What changed in this step.**
- edit config.yml                 git block rewritten. The collision left a comment
                                  saying the push was blocked pending the handle and
                                  naming a Keychain item the design had replaced. It
                                  now records the handle, the repo and osxkeychain,
                                  with why a push from the Claude VM cannot work.
- edit registry/control-tower.yml control_room released, both fields empty, with the
                                  rule written beside them.
- edit docs/OPEN_SESSION_PROMPT.md step 3 was naming S-002 to S-004 by hand and had
                                  gone stale, it still said "nightly scheduled task"
                                  after S-003a chose launchd. It is now a pointer to
                                  the newest handover, which is what the rest of that
                                  file already does, plus the control-room claim.
- new   the archive above.

**State at close, verified just now, not taken from any handover.**
- HEAD e8788b0 before this entry, tree clean. origin is
  https://YBellout@github.com/YBellout/personalai-tower.git.
- **No push has ever succeeded.** There is no origin/main. The hub still has no
  offsite copy, which is the half of M0 that is not proved.
- **The launchd agent has never woken by itself.** events.log holds exactly one Mac
  run, 13:05:15, and it is now 18:15. Five hours, zero automatic wakes. S-003's whole
  claim is that it runs unattended, and right now the evidence contradicts it rather
  than merely being absent. bus/heartbeat/ is empty, so there is no last-success
  marker either. This is the first thing the next chat should look at.
- A push cannot be tested from the Claude VM at all: the remote is configured for the
  osxkeychain helper, which does not exist there. `git ls-remote` fails on it. On
  macOS, where launchd runs the heartbeat, it is the right helper. So the push can
  only ever be proved from the Mac side.
- github.com/YBellout/personalai-tower answers 404 anonymously, which means absent or
  private and cannot be told apart from here.

**What is left, in order.**
1. Yassir: run launchers/check-heartbeat.command, because the agent is not waking.
2. Yassir: confirm the repo exists and is private, then the token, then
   launchers/connect-github.command, until origin/main exists.
3. Then S-004, three days, which cannot start before the first successful push.
4. Open and untouched: D-003 mirror, D-006 stray-scan grants, D-013 M1's exit test.

**One thing for the next chat to put to Yassir.** A Flask UI now exists at
"AI Control Tower/dev/ui" with a .venv of several hundred files. The M0 hold says no
UI until S-004 passes, and the UI is here before it. That is either a derogation that
was never recorded or a hold that has quietly lapsed, and it should be one or the
other on purpose. Also, that .venv must be git-ignored before "AI Control Tower" gets
its own repo, or the repo swallows it.

**Read first next time.** knowledge/status.md, then this file.
