# Self-governance

Scope: global. Binding on the AI Control Tower itself.

## The rule

The Tower is a governed project like any other. It has a registry entry
(`registry/control-tower.yml`), a charter, a policy (`policy/control-tower.yml`),
an evolution map (`evolution/control-tower.md`) and a control room chat, and it is
bound by every rule it enforces on the projects it governs.

The test, applied to every new rule before it is written down:

> The Tower may not require of a governed project anything it has not already done
> to itself, or is not doing to itself in the same release.

A rule that cannot pass that test ships with a derogation, recorded, or does not
ship.

## What this means in practice

| The rule the Tower enforces | How it binds the Tower |
|---|---|
| Governed means every file under the root, local disk | The Tower's own code lives in `AI Control Tower/dev` and `prod`, its data in `_tower`, nothing outside |
| One git repo per project, private remote | `_tower` and `AI Control Tower` each get one. M0 does the first |
| Never write prod except through promote | The Tower's own heartbeat and scripts are promoted, not edited in place. See X-001 |
| No code without an accepted design file | The heartbeat gets a design file before it gets a line of code |
| No release without evidence per acceptance criterion | M0's evidence is the three unattended nights, not an opinion |
| Never delete, move to `_to_delete/` | Applies to `_tower` first, where most early mistakes will be |
| No secrets in files, Keychain only | The GitHub credential for the push is a Keychain item, never a file |
| Budget enforced | `budget_usd_month: 15` in the Tower's own registry entry, same enforcement path |
| A handover after anything that changes anything | Including this file |
| Decision depth, at most three questions | The Tower answers Yassir this way, always |
| Nightly audit | Runs against `control-tower` first, and reports the Tower's own conformance before anything else |

## The one real asymmetry

Every governed project escalates a cross-project question to the Tower. The Tower
has nothing above it, so the Tower escalates to Yassir. That is the only place
where the Tower's obligations differ, and it is a difference in who decides, not in
whether a decision is recorded. The record is the same: a decision file, an id, a
scope.

The Tower does not get to decide its own exceptions. See below.

## Derogations

A derogation is a recorded, time-boxed exception to a rule above. It is the only
legitimate way for anything, the Tower included, to be out of conformance.

- Only Yassir grants one. Claude proposes, Claude never grants.
- Claude never extends, renews or reinterprets one, and never treats an expired
  derogation as still standing.
- Every derogation needs an expiry date or a closing trigger. One with neither is
  invalid and the audit treats it as a breach, not an exception.
- Every derogation names a compensating control, or says plainly that there is none.
- They live in one file, `decisions/derogations.yml`, so the full list of things
  currently not conformant is one read, never a search.
- The nightly audit reports every derogation: granted and live, expired, or
  proposed and not yet granted. An expired one is red.
- A derogation is scoped to one rule and one project. It never generalises.

Anything out of conformance without an entry in that file is a breach, and the
audit reports it as one.
