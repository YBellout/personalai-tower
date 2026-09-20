# Handover, 2026-09-20

**What.** Yassir accepted the S-003a design (launchd agent, exit test = three consecutive
days with the Mac on). S-003b is built and tested as far as the VM allows.

**What changed.**
- new  "AI Control Tower/dev/bin/heartbeat.sh"
- new  "AI Control Tower/launchers/install-heartbeat.command"
- edit "AI Control Tower/docs/S-003-heartbeat-design.md"   state accepted
- new  bus/events.log, bus/heartbeat/, heartbeat handovers from the test runs

**Verified in the VM.** Manual run commits and writes a handover (C1 minus push). Two runs
leave a clean tree and two distinct entries (C2). Hub missing reports HUB MISSING, rc 2,
and a push failure reports on its own line (C3). On the VM a bad remote reads as
"credential rejected" because the sandbox proxy answers 403, so C3's network case is
provisional until it is re-run on macOS.

**Not yet done, needs Yassir.** 1 double-click launchers/install-heartbeat.command (C4),
allow bash to access Documents if macOS asks. 2 GitHub handle, then the remote, the
Keychain sign-in and the first push (S-002 C5, C6). S-004's three days start after both.

**Read first next time.** This file.
