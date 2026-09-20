# Launch plan, per project

Written 2026-09-20 as part of release v0.1.0. Generated from a read-only scan of
the hub plus the registry. Refresh it by re-running the scan, not from memory.

## The gate

Nothing in this file executes until both of these are true:

1. M0 has passed its exit test: the heartbeat ran three nights unattended, with
   nobody touching the Mac.
2. Option E is picked, which fixes the order below.

Until then this is a plan, not a queue. No project is adopted, no file is moved,
no UI is built. That hold is from the design doc and it is not mine to lift.

## The pipeline, decided once, identical for every project

Sixteen steps in the design doc, section 16. The shape every project passes through:

1. **Charter line.** One sentence from Yassir: what this project is for, and one
   thing it is explicitly not for. Everything downstream gates on it.
2. **Sweep.** Find every file belonging to the project, wherever it currently is.
   Yassir confirms the list. Nothing moves yet.
3. **Freeze.** A verbatim read-only copy with `MANIFEST.tsv` and sha256, verified.
   Never touched again. Originals stay where they are until Yassir says otherwise,
   weeks later. Nothing is deleted during onboarding, ever.
4. **Place under the root.** `dev/` and `prod/`, code separated from resources.
5. **Git.** `git init`, `.gitignore` excluding resources and secrets, first commit,
   private GitHub remote, baseline tag.
6. **Govern.** Registry entry to `active`, policy file, charter, evolution backfill.
7. **Prove.** Baseline tests, `brief.sh`, `promote.sh`, `rollback.sh`, the mirror
   launcher. Then break something in `dev` and watch promote refuse.
8. **Link.** Open the control room chat, paste the block from
   `PROJECT_LINK_PROMPT.md` filled for that project id.

Steps 5 and 7 need D-002. Step 3 needs D-003, because the frozen copy is the first
thing the mirror has to protect.

## Order, and the next actions per project

The order below is the handover's recommendation for option E. Sections 13 and 17
of the design doc give a different order and name a project, "iExecAdmin", that
does not exist under the hub and appears nowhere else. That conflict is unresolved,
see open questions.

### 1. control-tower, in progress

Already governed, status `importing`. Next actions, which are M0:

- S-002 `git init _tower`, first commit, private remote under the D-002 account.
- S-003 Design file for the heartbeat, then `bin/heartbeat.sh`, then the nightly
  scheduled task, created from inside this project so its runs land here.
- S-004 Three unattended nights. On pass, status goes `importing` to `active`.
- X-001 needs granting or denying before S-003 writes a line of code.

### 2. ai-architecture-tower, docs-only, the cheap rehearsal

The right M1 candidate. It has no code, no data and nothing at risk, so it
exercises steps 1 to 8 end to end in an afternoon and finds the holes in the
pipeline before a project with real files goes through it.

- Create `AI Architecture Tower/docs/` under the root, one repo.
- Set the status line by re-reading the platform doc, every time, never cached.
- Note: the design doc's M1 exit test is written for a project with code. Against
  a docs-only project it cannot be run as written, so M1 either keeps a code
  project as its subject or the exit test is rewritten. That is a real choice and
  it belongs with option E.

### 3. family-school-dashboard, the first real adoption

The first project whose actual files move. Highest data sensitivity of the set.

- Locate it. It is not under the hub root, and the Tower has no folder grant to
  any of the four stray-scan locations in `config.yml`.
- Sweep and freeze before anything else, because this is the first time the
  pipeline touches files that matter.
- Policy file written before the move, not after.

### 4. virtual-closet, last on purpose

4.0 GB, 40,060 files, no version control anywhere, live work in flight. The most
valuable project and the worst one to restructure with an unproven process, which
is exactly why it is last.

- Answer the boundary question first: is the project `PersonalShopper`, or
  `PersonalShopper/Virtual Closet` with the rest as resources? It decides the repo.
- Split code from the 4 GB of photos before `git init`, not after.
- Lift the `.env` secrets to Keychain, see finding VC-F1.
- Add the enforced crawl pace limit, VC-F4, carried over from the permission
  decision. It is about not being blocked, so the allow-audit posture does not
  cover it.

### 5. home-assistant, or not at all

T-2 is unanswered. Config rather than an app. Adopting it as code would be
governance for its own sake, which is the named risk of the Tower eating the
projects it governs.

## Added to release v0.1.0 today

- `docs/PROJECT_LINK_PROMPT.md`, the block that binds a project to the Tower.
- `policy/self-governance.md`, the Tower bound by what it enforces.
- `decisions/derogations.yml`, the register, with X-001 proposed.
- Four registry stubs at status `unmanaged`, verified facts only.
- This file.

## Open questions, blocking the order

- **Option E**, unpicked, and the section 13 versus section 18 conflict above.
- **"iExecAdmin"**, named as the M1 pilot in sections 13 and 17, absent from the
  hub, the handover and the memory of every project. Does it exist, and is it in
  scope? If not, M1's exit test needs rewriting against a project that does.
- **D-002**, GitHub account. Blocks step 5 for every project including the Tower.
- **D-003**, mirror destination. Blocks step 3, the frozen copy, for every project.
- **X-001**, grant or deny. Blocks M0's first line of code.
- **Stray scan grants.** The Tower cannot see `~/Desktop`, `~/Documents`,
  `~/Downloads` or `~/Developer`, so it cannot find what is outside the root, and
  residency is unverifiable for every project except the two already under it.
