# Handover, 2026-09-20

**What.** Wrote the per-project link prompt, the self-governance clause and the
derogation register, four registry stubs at status unmanaged, and the per-project
launch plan. Rewrote the Tower's own instructions to be the same block it hands
out. Patched the registry entry and the evolution map. Stories S-005 to S-008.

**Why.** Yassir asked for the prompt that binds every governed project to the
Tower, for the Tower to be bound by the same rules it enforces, and for the next
actions per project to be produced as part of release one.

**What changed.**
- new  docs/PROJECT_LINK_PROMPT.md
- new  policy/self-governance.md
- new  decisions/derogations.yml            (X-001 proposed, not granted)
- new  docs/LAUNCH_PLAN.md
- new  registry/{virtual-closet, family-school-dashboard, ai-architecture-tower, home-assistant}.yml
- edit docs/PROJECT_INSTRUCTIONS.md         (now the shared block, filled)
- edit registry/control-tower.yml           (self_governance block, two links)
- edit evolution/control-tower.md           (S-005 to S-008, D-005, D-006)

Nothing outside _tower was read, written, moved or deleted. No project was adopted.
No UI was built. The M0 hold is intact.

**What it proves.** That the governance model can be written down and applied to
its own author before a line of code exists. The registry stubs also prove the
scan works: two projects are under the root, the other candidates are not, which
is a residency finding rather than an assumption.

**What is left.** M0, unchanged and unstarted: S-002 the repo and remote, S-003 the
heartbeat, S-004 three unattended nights. All still blocked.

**Blocked on Yassir.** D-001 options A to E. D-002 GitHub account. D-003 mirror
destination. X-001 grant or deny. D-005 whether "iExecAdmin" exists. D-006 folder
grants for the stray scan. Root path confirmation, still unanswered from the
previous handover.

**Read first next time.** docs/LAUNCH_PLAN.md, then decisions/derogations.yml.
