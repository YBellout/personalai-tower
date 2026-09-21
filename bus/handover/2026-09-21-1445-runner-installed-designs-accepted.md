# Handover, 2026-09-21 14:45, control room

**What.** Yassir ran install-runner.command. The runner reached the hub on its first
run. He then accepted S-016 with three amendments, and S-024 and S-025, widening S-024.

**Runner evidence, read from the hub.** bus/heartbeat/alive 2026-09-21T18:38:51Z,
last-error empty, events.log gains a Mac run at 14:38:51, commits f4b9dc0 and 8934a09,
handover 2026-09-21-143851-heartbeat.md. The push failed: "could not read Password",
no GitHub credential yet, expected. S-015 C1 and C5 need two unattended wakes, due
about 15:08 and 15:38.

**Two findings from that run, now inside S-024 on Yassir's pick.** "could not read
Password" is not matched as a credential failure, so it is logged as a generic push
failure. And events.log holds the 14:38:51 run twice: launchd's RunAtLoad and the
installer's own test run fired in the same second, and one handover overwrote the
other. A one-time install effect, the fix is unique handover names.

**What changed.**
- "AI Control Tower" main: S-016 accepted with amendments (a) step 7 writes only the
  registry's version fields, (b) step 1 never reads the evolution map, (c) the tag is
  local, a failed push never blocks a promote; snapshots under archives/releases/.
  S-024 widened with C3 and C4. S-024 and S-025 accepted.
- new decisions/D-020.md   promote.sh owns the registry's version fields, a named
                           exception to D-018. Accepted decisions are never edited.
- edit evolution/control-tower.md, status/status.json.

**What is left.** Yassir: Mac untouched until about 15:40, then Privacy and Security,
open the two chats, GitHub. Control room: verify the two wakes.

**Read first next time.** this file.
