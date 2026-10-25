# next — recommend a task

Goal: break the inertia. The user knows they need to move forward but doesn't
know where to start, and ends up doing nothing. Give them **one concrete first
push**, not a dump of the whole backlog.

## Rules

- **Only read the logbook** (`roadmap.md`, `technical-debt.md`, `wishlist.md`)
  and, if needed to judge effort, take a cheap look at the code. **Don't query
  git.**
- If extra context is given (`next debt`, `next quick`), lean the
  recommendation toward it.
- If every file is empty, say so and offer to run `audit` or to capture ideas
  in the wishlist.

## How to choose

The bias is **getting started**, not "the most important thing" (which is
usually the biggest and most overwhelming). Weigh:

- **Low effort** to get into flow (quick win) — high weight.
- High **risk** in `TD` (7-10) — push it up even if it isn't a quick win, but
  say so.
- Work already marked `In progress` — resuming it wins, it avoids leaving
  things half done.
- The roadmap order (top = higher priority).
- Obvious dependencies (don't recommend something blocked by an unfinished
  task).

## Output

Answer in the language the user is speaking. Give **1 main recommendation + 2
alternatives**, each with a one-line reason:

```
Start with: [RM-003] Live smart tracking
  Why: it kicks off the core of v1.5 and the data model is already in place.

Alternatives:
  Quick  — [TD-006] Show network errors in the hooks (~30 min, removes real friction).
  Deeper — [TD-005] Basic auth before exposing it through the tunnel (risk 6/10).
```

Close by offering to **mark the chosen one `In progress (YYYY-MM-DD)`** in its
file (the WIP marker from the task lifecycle). Don't mark it without
confirmation.
