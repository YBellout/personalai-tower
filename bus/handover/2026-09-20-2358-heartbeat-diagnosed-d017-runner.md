# Handover, 2026-09-20 23:58

**What.** Yassir ran check-heartbeat.command. The diagnostic confirms why the heartbeat
has been silent, and he chose the fix. D-017 records the choice, S-015 is rescoped to it,
and its design file is proposed.

**The evidence, bus/reports/heartbeat-diagnostic-2026-09-20-234628.txt.**
- launchd: runs = 22, run interval 1800 s, last exit code 126. The scheduler works and
  the Mac was awake from 13:05 to 23:46.
- err log: every automatic run, `/bin/bash: .../dev/bin/heartbeat.sh: Operation not
  permitted`. macOS privacy protection denies the bash that launchd starts any access
  to ~/Documents, so the script never reaches line 1.
- The one success, 13:05, ran in Terminal started from Finder, which holds that access.

**Correction to the 22:00 entry.** It said the run likely died at line 12 of the script.
It dies before line 1. Consequence: nothing inside heartbeat.sh can report this failure,
so visibility has to come from the hub noticing silence, hence the liveness file and the
dead-man check in S-015's design.

**What changed.**
- new  decisions/D-017.md          one granted runner app for every unattended job. Full
                                   Disk Access for bash and moving the hub both rejected.
- new  "AI Control Tower/docs/S-015-runner-design.md"   proposed.
- edit .gitignore                  bus/heartbeat/alive and last-error, never committed.
- edit evolution/control-tower.md  S-015 rescoped, S-003 note, D-017 accepted.
- edit status/status.json          regenerated.

**Waiting on Yassir.** Accept S-015, and grant or refuse widening X-001 to the
dispatcher, run-operations.sh. Accept S-014. Then the GitHub steps.

**Read first next time.** "AI Control Tower/docs/S-015-runner-design.md", then this file.
