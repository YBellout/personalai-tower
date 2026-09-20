# bin

Empty on purpose. M0 and M1 create these, in this order:

    brief.sh <project>     the generated opening context, under 60 lines
    heartbeat.sh           the M0 proof: wake, read, append, commit, push, handover
    status.py              regenerates _tower/status.json from git, disk and the files
    promote.sh <project>   tests, tag, snapshot prod, copy code, smoke, record
    rollback.sh <project>  restore the previous release
    mirror.sh              incremental checksum mirror to the local backup target
    audit.py               residency, policy drift, conformance, stray files
    adopt.sh <project>     the sixteen-step onboarding pipeline

Nothing here is written by hand twice: these are the Tower's own code, developed in
"AI Control Tower/dev" and promoted to "AI Control Tower/prod".
