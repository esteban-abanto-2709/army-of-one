# audit — technical-debt sweep of the code

Goal: review the code for debt and fill `technical-debt.md`. It's a
**deliberate, heavy** sweep (that's why it's a command, not automatic).

## 1. Before scanning — read what's already known

- Read `docs/logbook/technical-debt.md` (open debt) and
  `docs/logbook/changelog.md` (resolved debt, `TD` prefix). This avoids
  **duplicates** and reporting what's already fixed, and gives you the next
  available `TD-###` code (highest used +1 across the open file + changelog).

## 2. Scan

- If a path is given as context (`audit apps/api`), limit the sweep to it.
  Otherwise, the whole repo (excluding `node_modules`, `dist`, `.next`, build
  output).
- Look for the usual categories: missing input validation, swallowed errors,
  security risks (auth, secrets, injection), performance problems (N+1, loading
  everything into memory), fragile coupling, dead code, hardcoded
  configuration, `TODO/FIXME/HACK` comments (and propose migrating them to the
  logbook!).

## 3. Deduplicate and score

- Drop what's already in `technical-debt.md` or resolved in the changelog.
- Assign **risk 1-10** using the scale in `spec.md` (1-3 cosmetic · 4-6 slows
  down/moderate · 7-9 latent bug or security · 10 critical).

## 4. Confirm BEFORE writing

- **Don't write directly.** Present the proposed findings as a list (location
  + risk + problem in one line), sorted by risk, highest first.
- Let the user drop or edit items. Only after their OK, add the entries to
  `technical-debt.md` in the `spec.md` format, in the document language, with
  the correct consecutive `TD-###` codes.

## 5. Wrap-up

- Summarize how many entries were added and with which codes. Don't commit
  unless asked.
