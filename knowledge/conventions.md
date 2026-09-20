# Conventions

## Objects and ids
Only seven object types exist, and only these prefixes:

    R-017     requirement   what he wants, in his words
    D-021     decision      a choice, scope project or global
    S-141     story         buildable work with a design file and criteria
    O-0042    order         work dispatched on the bus
    v1.15.0   release       a promoted version
    F-0231    feedback      a comment filed from inside an app
    (stamp)   handover      one action, recorded, append-only

Retired and not to be reintroduced: ADR, DIR, batch B-, idea lists, session notes.

## Files and paths
- Root is the value of `root` in _tower/config.yml. Nothing is hardcoded elsewhere.
- Launchers are numbered and named for what they do: `1. Start Closet.command`.
- Dates are ISO: 2026-09-20. Timestamps are local time.

## Money
- Prices are final. Taxes and shipping are already included, nothing is added on top.
- Currency is stated per value, never assumed.
