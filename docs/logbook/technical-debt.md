# Technical Debt

Shortcuts, pending decisions and future risks in this project.
Code `TD-###` (never reused). Once resolved, the entry moves to the changelog
and is deleted from here.

**Entry format:**
- **Location:** affected `file:line`.
- **Risk:** 1 to 10 (1-3 cosmetic · 4-6 slows down/moderate · 7-9 latent bug or security · 10 critical).
- **Problem:** what's wrong, condensed.
- **Future impact:** what it can cause if left alone.
- **Suggestion:** (optional) how to fix it, in one line. A hint for whoever picks it up, not a spec.
- **Date** and **Status** (Open / In progress).

---

## [TD-009] Rough edges found by the stranger test
- **Location:** `plugins/project-kit/skills/logbook/reference/init.md`, `reference/spec.md`
- **Risk:** 3/10
- **Problem:** found in the RM-004 run:
  - `init` doesn't ask the language when the user's global file has a `Logbook language:` line; it only shows it in the plan, so a project silently inherits it.
  - "Already set up?" looks at `docs/logbook/`, but after an `init` with nothing to migrate that folder is empty and git doesn't keep it; the block's markers are a better signal.
  - The format example in the changelog header starts with `## [CODE]`, so anything that greps `^## \[` counts it as an entry; unclear whether its placeholders get translated.
  - Nothing says the `In progress` marker goes in the `Status` field, nor to keep the file's line endings.
  - When the global file has an older copy of the block, `init` only mentions the duplicate, not that it's out of date.
  - `audit` has no guidance on depth, so a quick sweep mostly returns TODO comments.
  - Not covered: the passive rules in a fresh session that never invoked the skill.
- **Future impact:** projects end up in a language the user never chose; the other points make results vary between agents.
- **Suggestion:** always ask the language in `init` with the resolved one as default; detect set-up by the markers; one line each for the rest.
- **Date:** 2026-10-25 · **Status:** Open
