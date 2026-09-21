# Handover, 2026-09-20 22:00

**What.** Opened with OPEN_SESSION_PROMPT.md, read the list fresh, put five open items
to Yassir, all taken as recommended, executed. A second git repo now exists. S-014's
design file is proposed. The heartbeat's silence has a likely explanation.

**What changed.**
- edit registry/control-tower.yml   control_room claimed by this chat, formally. X-002
                                    added to open_derogations.
- edit decisions/derogations.yml    X-002 granted by Yassir: the dev UI built past the
                                    M0 hold, closing when S-004 passes. Until now it was
                                    an unrecorded breach.
- new  decisions/D-003.md           mirror: external drive if one exists, otherwise
                                    ~/PersonalAI-mirror. One fact outstanding.
- new  decisions/D-006.md           stray-scan grants over Desktop, Documents,
                                    Downloads, requested at M1. ~/Developer dropped.
- new  decisions/D-013.md           M1's exit test runs against the Tower. Promoting
                                    heartbeat.sh is also X-001's trigger: one event.
- edit config.yml                   mirror path per D-003, flagged as NOT mirroring
                                    until mirror.sh. ~/Developer dropped per D-006.
- edit evolution/control-tower.md   stale S-002, S-003 and duplicate D-002 lines fixed.
                                    D-003, D-006, D-013 moved to accepted. Open decisions
                                    now D-004 only. S-015 added. X-002 recorded.
- edit status/status.json           regenerated per D-015.
- removed _tower/.git/index 2.lock  a leftover of the 01:27 two-chat collision. git
                                    never reads that name. 7 KB of junk.
- new  "AI Control Tower" git repo  919315b, 21 files, largest 20 KB. prod/, .venv,
                                    __pycache__ ignored. Local only. heartbeat.sh, the
                                    UI, the launchers and every design file had no
                                    history before this.
- new  "AI Control Tower/docs/S-014-stale-lock-design.md"  proposed, commit 6897168.

**Verified, not assumed.**
- Before the first commit of the new repo: a secrets scan hit v0.1.0-plan.md, and it was
  the grep pattern written into S-002's own criterion. No real token anywhere.
- Both artifacts unchanged since this morning: design doc rev 42, platform doc rev 12.
- The 21:45 handover said control_room was empty. It held this chat's URL, written at
  01:28:13 and committed by the 21:45 session in d4a3325. A "verified just now" line
  in a handover was wrong. Reading the file, not the handover, is what caught it.

**The finding that changes what M0 is waiting on.** Read heartbeat.sh line by line:
lines 12, 15 and 21 exit with "HUB MISSING" before events.log is touched, and log only
to ~/Library/Logs, which nothing here can read. So "no automatic run in events.log" does
not mean launchd is not firing. The likeliest reading: launchd fires every 30 minutes,
macOS denies the bash it starts access to ~/Documents, the run dies at line 12, and the
hub never hears of it. The 13:05 run worked because it was started from Finder, which
has Documents access. check-heartbeat.command reads that log and confirms or refutes
this. If confirmed, the fix has a security cost worth deciding: Full Disk Access for
/bin/bash grants it to every bash script on the Mac. S-015 carries the narrower route.

**What is left, in order.**
1. Yassir: check-heartbeat.command. It is now the most informative minute available.
2. Yassir: repo, token, connect-github.command, until origin/main exists.
3. Yassir: accept S-014's design. Then Claude builds it.
4. S-015 once the diagnostic confirms the cause.
5. S-004.
6. D-003: whether an external drive exists. And confirm iCloud's Desktop and Documents
   sync is off, because the hub lives in ~/Documents and the first residency rule is
   "never iCloud". Nothing seen suggests it is on, and nothing here can prove it is off.

**Read first next time.** knowledge/status.md, then this file.
