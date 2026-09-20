# Handover, 2026-09-20, session close

**What.** The build session that set up the hub's governance documents is closed.
Control passes to the AI Control Tower control room chat, which was launched with
docs/LAUNCH_PROMPT_v0.1.0.md.

**Why.** Yassir launched the control room chat and is closing this one. From here
that chat is the single writer to this hub, which is what keeps two chats from
clobbering one file.

**What this session produced.** Stories S-005 to S-009 of release v0.1.0, all
documents, no code:
- docs/PROJECT_LINK_PROMPT.md, docs/OPEN_SESSION_PROMPT.md,
  docs/LAUNCH_PROMPT_v0.1.0.md, docs/LAUNCH_PLAN.md
- policy/self-governance.md, decisions/derogations.yml (X-001 proposed),
  decisions/D-007.md
- registry/{virtual-closet, family-school-dashboard, ai-architecture-tower,
  home-assistant}.yml, all at status unmanaged
- rewrote docs/PROJECT_INSTRUCTIONS.md, patched registry/control-tower.yml and
  evolution/control-tower.md, appended a close section to docs/HANDOVER.md

**State of the hub at close.**
- No git repository anywhere, so nothing is uncommitted and nothing is unpushed.
- No order issued, no report written, no claim held, bus is clean.
- control_room.chat in registry/control-tower.yml is still empty. The new chat sets
  it as its first write. If it is still empty on the next read, that chat never got
  its folder grant and never started.
- Tower status is still `importing`. It becomes `active` when M0 passes.
- Nothing outside _tower was read, written, moved or deleted, at any point. No
  project was adopted, no file moved, no UI built. The M0 hold is intact.

**What does not cross over.** This conversation, its memory, and its folder grant.
The new chat needs its own grant to ~/Documents/PersonalAI. Everything this session
knew that mattered is in the files above, which is the point of writing them.

**Blocked on Yassir, unchanged.** D-001 A to E, D-002 GitHub account, D-003 mirror
destination, X-001 grant or deny, D-005 iExecAdmin, D-006 stray-scan grants, root
path confirmation. The launch prompt stops at its step 1 until these are answered.

**Read first next time.** This file, then docs/LAUNCH_PLAN.md, then
decisions/derogations.yml.
