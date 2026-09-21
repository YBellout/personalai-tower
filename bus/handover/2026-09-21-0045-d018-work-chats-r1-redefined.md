# Handover, 2026-09-21 00:45

**What.** Yassir asked for the next actions split into bug fixing and evolutions, R1 and
the next release redefined, and two autonomous chats that run in parallel. Intake under
D-007, three questions, all answered as recommended, which validated the requirement.
D-018 records it.

**What changed.**
- new  decisions/D-018.md           two work chats, Bugs and Evolutions, splitting D-016's
                                    Evolutions stream by tag. Control room sole writer of
                                    shared files. Claims per chat. One clone per chat.
- new  claims/README.md             the claim format and rules, one file per chat.
- edit bus/README.md                orders, reports and claims keyed by chat; one order in
                                    flight per chat.
- new  bus/orders/control-tower/bugs/O-0001.yml         S-014 then S-015, gated.
- new  bus/orders/control-tower/evolutions/O-0002.yml   design only, S-016..S-023, S-013.
- new  docs/CHAT_PROMPT_BUGS.md, docs/CHAT_PROMPT_EVOLUTIONS.md   paste-ready, marked.
- edit docs/OPEN_SESSION_PROMPT.md  the control room reads D-018.
- edit registry/control-tower.yml   work_chats block.
- edit evolution/control-tower.md   R1 is v0.1.0 with 13 stories, S-014 and S-015 pulled
                                    in. v0.2.0 = M1 with S-016 to S-023. S-012 and S-013
                                    moved to M3. Work chats section. D-018 accepted.
- edit status/status.json           regenerated.
- "AI Control Tower": .gitignore gains .chats/; v0.1.0-plan.md gains S-014 and S-015;
  new v0.2.0-plan.md, proposed; two clones, .chats/bugs and .chats/evolutions.

**One mechanism changed from what was validated, and why.** The validated text said "a
git worktree per chat". Tested first: git 2.34 in the Claude VM writes worktree links as
absolute paths containing the creating session's id, so a worktree made here is broken
in every other chat and on the Mac. Each chat got a full clone with relative origin
`../..` instead, verified to fetch. Same property Yassir chose, own files, own index,
shared history, control-room merge. Recorded in D-018. Say the word to revisit.

**The limit stated plainly to Yassir.** A chat works only when it has a turn and chats
cannot message each other. "Autonomous" means no human needed mid-task, not running while
idle. Scheduled self-waking is M5.

**What is left, in order.**
1. Yassir: accept S-015, grant or refuse X-001's widening, accept S-014.
2. Yassir: open the two chats and paste their prompts.
3. Yassir: the GitHub steps.
4. Yassir: approve v0.2.0-plan.md, not urgent, the Evolutions chat designs either way.

**Read first next time.** decisions/D-018.md, then this file.
