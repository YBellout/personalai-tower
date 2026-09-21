# Claims

Who holds which files right now. D-018. One file per chat, so two chats never write the
same file: `control-tower.bugs.yml`, `control-tower.evolutions.yml`.

Before touching any path, a chat reads every file here and never writes a path another
chat holds. It adds its claim first, and removes it when the control room has merged the
story. A claim older than 24 hours with no report behind it is stale: the audit flags it,
and only the control room clears it.

    chat: bugs
    session: https://claude.ai/code/session_...
    opened: 2026-09-21
    claims:
      - story: S-014
        paths: ["AI Control Tower/dev/bin/heartbeat.sh"]
        since: 2026-09-21T09:30
