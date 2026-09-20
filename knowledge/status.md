# Status, how the Tower reports where Yassir is

Decision D-015, story S-011. Scope: the control room chat, and later the Tower UI.

## What it is for

The control room chat stays open on the side as Yassir's project dashboard. The status
is regenerated often. It must give him, in seconds: where he is, what HE has to do next,
and what Claude does next. Brief and actionable, always. Simple and visual.

## When it is regenerated

1. Yassir types the single word `status`. This is a short control answer under D-007,
   so it never goes through intake.
2. Automatically, at the end of every completed work step in the control room.

## How it is regenerated, never from memory

Read fresh, in this order, and nothing else:

1. `_tower/bus/handover/`, newest by mtime, then the newest `*-heartbeat.md`
2. `_tower/evolution/control-tower.md`, stories and open decisions
3. `_tower/registry/*.yml`, status per project
4. `_tower/config.yml`, empty values that block something
5. `git -C _tower log -1`, `git -C _tower status --porcelain`, `git -C _tower remote -v`
6. `_tower/bus/events.log`, last lines, and `_tower/bus/heartbeat/last-success`

If the hub cannot be reached, say so in one line and show the last `status.json` with
its date. Never invent a state.

## The two outputs, always both

1. **`_tower/status/status.json`**, the data. It is the contract the future HTML UI
   reads (M1, `status.py`). Overwritten at every refresh and committed. Shape below.
2. **The side doc**, the current rendering of that data, rewritten in place, same link:
   https://claude.ai/code/artifact/20928a96-0eea-4492-a661-13d95e25b464
   Plus three lines in chat: light and headline, Yassir's next action, Claude's next action.

When the UI exists it replaces the side doc as the rendering. The data file and these
rules do not change.

## Fixed layout of the rendering, top to bottom

1. **Headline**: one light and one sentence. 🟢 on track, 🟡 waiting or at risk, 🔴 broken or blocked.
2. **Your actions**: a table, at most 4 rows: number, action with minutes, who can do it,
   button. Before listing any action, check whether Claude can do it for him, and tag it:
   🤖 Claude alone, 🤝 shared (say which part stays his), 👤 only him (say why, one clause).
   Anything Claude can do alone without his OK is not an action of his, Claude just does it.
   Never automate a step that creates, shows or pastes a secret, that stays 👤.
   Button column: a prefilled link when a URL exists, the control words `do N` when Claude
   can run it, and the launcher file name when it is a double-click. `do N` is a short
   control answer under D-007, no intake. If there is none, write "Nothing needed from you".
   The HTML UI (M1) turns this column into real buttons: `link`, `do`, `launcher`.
3. **Claude next**: at most 3 lines, what runs without him.
4. **Milestone**: release, progress n of m stories, exit test counter (days passed of 3).
5. **Stories**: one table, one row per open story, state as ✅ done, 🔵 in progress,
   ⏳ waiting on Yassir, ⛔ blocked, ⚪ not started. Done stories collapse to one line.
6. **Projects**: one table, project, registry status, one next step.
7. **Watch**: at most 3 risks, one line each. No more.
8. Footer: generated at, sources read.

## Rules of writing
- Every hub path shown to Yassir is clickable and opens the containing folder. In the
  side doc: a `file:///` link to the folder, spaces as %20. In chat: a `computer://`
  link. In the M1 UI: a button that reveals the file in Finder. If a surface blocks
  the link, keep the path readable next to it.

- Fits one screen of the side panel. If it grows, cut, do not scroll.
- Yassir's actions always come first, above everything except the headline.
- No history, no explanation of how things work, no restating decisions. Links to the
  hub file instead.
- States come from named evidence in the hub, never from belief. A story is ✅ only if
  its criteria closed.
- Commas instead of long dashes, in every status, as in all text for Yassir.

## status.json shape

    generated_at, generated_by, light (green|amber|red), headline,
    your_actions[]  {n, do, minutes, automation (claude|shared|user), why, button {kind (link|do|launcher), target}}
    claude_next[]   string
    milestone       {release, name, stories_done, stories_total, exit_test, exit_days_passed, exit_days_needed}
    stories[]       {id, title, state (done|in_progress|waiting_user|blocked|not_started), note}
    projects[]      {id, name, status, next}
    watch[]         string
    heartbeat       {installed, last_run, last_result, last_success_day}
    sources[]       string
