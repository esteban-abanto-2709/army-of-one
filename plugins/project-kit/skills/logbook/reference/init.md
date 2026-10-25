# init — set up or migrate the system

Goal: leave `docs/logbook/` in place and absorb into it **any** tracking
artifact that already exists in the project, whatever it's called. It isn't a
closed list of special cases: the flow is
**discover → classify → confirm → migrate**. Idempotent: if everything is
already in `docs/logbook/` and up to date, don't break anything.

First: is it a git repo? If not, say so (offer `git init`) — the backup for
everything that gets deleted depends on git.

## 1. Discover candidates

Sweep the repo (skipping `node_modules`, `dist`, `.next`, build) for documents
that **are** work tracking, by name **and** by content. The names below are
hints, NOT an exhaustive list — generalize to variants, plurals, casing and
languages:

- To do / ideas: `roadmap`, `todo`, `todos`, `tasks`, `backlog`, `wishlist`,
  `ideas`, `pending`, `notes`…
- Debt / problems: `technical-debt`, `tech-debt`, `debt`, `issues`, `fixme`…
- Done: `changelog`, `history`, `releases`, `done`…
- Previous version of this system: a `docs/tracking/` folder (already almost in
  format → easy case, just rename and normalize).

**Content** counts too: a `.md` that is really a list of tasks/ideas/done items
is a candidate even if its name doesn't fit. Flag for asking any file where
you're unsure between "tracking" and "conceptual".

## 2. Classify

Map each candidate — or **each section within a file**, because one file can
split into several buckets — to one of the four:

| Content | Destination |
|---|---|
| Something wrong **now** in the code | `technical-debt.md` (`TD`) |
| **Committed** work | `roadmap.md` (`RM`) |
| Idea **with no commitment** | `wishlist.md` (`WL`) |
| Already **finished** | `changelog.md` |

**Conceptual** material (product vision, v1/v2/v3 milestones in prose) is NOT
tracking → it stays in `docs/` (e.g. `docs/product-vision.md`). If it has
committed work embedded, extract those pieces as `RM` and leave a cross
pointer.

## 3. Language

Resolve the document language as `spec.md` says.

- **Nothing configured and no existing logbook:** ask the user which language
  the logbook should be written in. The answer goes into the agent rules
  (step 6).
- **Configured language differs from the existing files:** offer to translate
  them: everything, or only the open files (roadmap, debt, wishlist) leaving the
  changelog history as it is. Titles, field labels and entries are translated;
  **codes never change**. Only with the user's OK; if they decline, the files
  keep their language.

## 4. Propose a plan and confirm

Classification is fuzzy, so **don't move anything yet**. Show the user the
plan: which file/section goes to which bucket, what stays conceptual, which
codes would be assigned, the document language (and any translation), and
which file the agent rules will go into (step 6). Let them correct it and
migrate only after their OK. (Exception: the mechanical rename of
`docs/tracking/` can be done directly, telling them.)

## 5. Migrate

- `git mv` when a whole file maps 1:1 to a destination (keeps history); if it
  splits into several buckets, create the destinations and `git rm` the old
  one.
- Apply the header templates from `spec.md`, in the document language.
- Assign consecutive `TD/RM/WL` codes from 001, never reused (open file +
  changelog). If an entry already had a valid code (`docs/tracking/` case),
  **keep it, don't renumber**.
- Reconcile format: debt with `Status: Open`; changelog as
  `## [CODE] Title (YYYY-MM-DD HH:MM)`. For historical entries without a time,
  keep only the date `(YYYY-MM-DD)`. **Never query git for dates/times.**
- Respect "files on demand": don't create empty buckets. If nothing was
  discovered, create only the `docs/logbook/` folder and explain that the files
  are born when there is something real to put in them.
- Fix broken pointers (`README.md`, vision docs) to old paths/names.

## 6. Install the agent rules

Copy the block from `agent-rules.md` (markers included) into the instructions
file the agent reads every session. It goes in **one file, never two**: Claude
Code reads `CLAUDE.md` or `AGENTS.md`, not both, and duplicating it makes it
load twice or leaves one copy unread.

**Before choosing:** if the block is already in the user's global instructions
file (`~/.claude/CLAUDE.md` or their agent's equivalent), the rules already
apply to all their projects: don't write it into the project, and tell them. If
this project needs a different document language than the global one, write
only a `Logbook language: <language>` line in the project's instructions file.

**Destination in the project**, the first rule that applies, looking at the
repo root:

1. There's a `CLAUDE.md` that imports `@AGENTS.md` → `AGENTS.md`.
2. There's a `CLAUDE.md` → `CLAUDE.md`.
3. There's only an `AGENTS.md` → `AGENTS.md` (so other agents read it too).
4. There's neither → create `CLAUDE.md` with just the block.

If the user prefers the rules to apply to all their projects, offer the global
file instead of the project's.

**How to write it:**

- Fill in the `Logbook language:` line with the document language. When
  replacing an existing block, **keep the language it already had** unless the
  user chose a new one.
- If the destination already has the markers, replace **everything** from the
  line starting with `<!-- logbook:start` through `<!-- logbook:end -->`, both
  included. Otherwise, append it at the end of the file, separated by a blank
  line.
- Don't touch anything outside the markers.
- If you find a logbook section **without markers** (older, hand-written
  version), propose replacing it with the block; don't delete it without their
  OK.
- If the block appears in another file besides the destination, say so and
  propose removing the extra copy.

## 7. Wrap-up

- Summarize what was migrated/renamed, codes kept or assigned, next available
  numbers (`TD/RM/WL`), what stayed conceptual, the document language and which
  file the agent rules ended up in.
- Don't commit unless the user asks (everything goes through git → they can
  review with `git diff` and revert if something is off).
