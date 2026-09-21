# Bus

How the Tower and the projects talk, given that no chat can call another.

    orders/<project>/      work the Tower wants done, one file per order
    reports/<project>/     what came back, one file per order
    feedback/<project>/    comments filed from inside an app
    handover/<project>.md  append-only, six lines per action, read by the control room
    ../claims/<project>.yml who is holding which files right now

Orders are immutable: changing your mind issues a new one that supersedes it.
One order in flight per project. A report is always written, including on failure.

Amended by D-018, 2026-09-20: a project with work chats keys the bus by chat as well,
`orders/<project>/<chat>/`, `reports/<project>/<chat>/`, `claims/<project>.<chat>.yml`,
and the rule becomes one order in flight per chat.
