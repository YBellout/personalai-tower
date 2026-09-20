# Handover, 2026-09-20

**What.** Recorded this chat as the Tower's control room. Set `control_room.chat`
and `control_room.opened` in `registry/control-tower.yml`.

**Why.** LAUNCH_PROMPT_v0.1.0.md orders it before any other change, so the standing
chat is identified on disk rather than implied by whoever is typing.

**What changed.**
- edit registry/control-tower.yml   (control_room.chat, control_room.opened)

Nothing else. No project adopted, no file moved, no UI built. The M0 hold is intact.

**Verified on the way in.** Root `/Users/yassirbellout/Documents/PersonalAI` exists,
is readable and writable, and holds `_tower`, `_shared`, `AI Control Tower` and
`PersonalShopper`. The full READ list of OPEN_SESSION_PROMPT.md was read fresh,
including both artifacts. The platform doc is at rev 12, which is the
`last_seen_rev` already in `registry/ai-architecture-tower.yml`, so that status line
is current and needed no edit.

**Two findings, neither acted on.**
- `~/Developer` does not exist on this Mac. `config.yml`
  `residency.scan_for_strays` names four locations and only three of them are real,
  so D-006 is a grant over `~/Desktop`, `~/Documents`, `~/Downloads`, and the fourth
  line should be dropped from config when D-006 is answered.
- The four earlier handover filenames carry clock values (1500, 1620, 1705, 1740)
  that do not match their own mtimes, which fall between 07:24 and 07:48 UTC. This
  entry uses the operator's real local time, America/Toronto. Until the naming clock
  is settled, order these entries by mtime, not by name.

**What is left.** The launch prompt arrived with every answer at TBD, so nothing was
transcribed and nothing was granted. One decision-depth message went back: the D-001
block, X-001, and the two values only Yassir holds, D-002 and D-003. The v0.1.0
release plan and M0 are both behind that answer.

**Read first next time.** docs/LAUNCH_PROMPT_v0.1.0.md, then this file.
