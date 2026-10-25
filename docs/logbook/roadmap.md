# Roadmap

Committed work: what will be done. Code `RM-###` (never reused).
Ordered by priority, top first. When a task is finished it moves to the
changelog and is deleted from here.

**Entry format:**
- **Goal:** what we want to achieve.
- **Scope:** (optional) what's in and what's out.
- **Open questions:** (optional) what must be decided when starting.
- **Done when:** clear completion criterion.
- **Date** and **Status** (Open / In progress).

---

## [RM-001] Classify problems: TD, BUG and SEC
- **Goal:** stop `technical-debt.md` from being the bucket for anything that's wrong.
- **Scope:** `TD` only for code the user doesn't notice (a refactor fixes it); new `BUG` for wrong behavior; new `SEC` for security, with a disclosure rule (an open vulnerability isn't written in detail in a public repo). Product friction and missing features go to `RM`/`WL`. A decision rule in `spec.md`, the new formats, and `init`/`audit`/the agent block updated.
- **Done when:** `spec.md` has the decision rule and the three formats, and classifying the open TDs of a real project with it leaves no doubtful case.
- **Date:** 2026-10-25 · **Status:** Open

## [RM-004] Test the published skill with an agent
- **Goal:** see how an agent that has never seen the skill reacts to it, after publishing.
- **Scope:** a throwaway project; install from GitHub; an agent runs each case and reports. Cases:
  - `init` on an empty project: asks the language, creates only `docs/logbook/`, writes the block into a new `CLAUDE.md`.
  - `init` with only `AGENTS.md`, with `CLAUDE.md` importing `@AGENTS.md`, and with both: the block lands in the right file, once.
  - `init` run twice: no duplicate block, the language line is kept.
  - Block also in the global file: `init` still writes it into the project, mentions the duplicate and doesn't edit the global file.
  - Configured English with Spanish files: keeps writing Spanish, offers translation; translating keeps every code, date and literal product text. (Passed on a real project before the TD-007 fixes.)
  - Passive rules in a fresh session without invoking the skill: debt noticed goes to `technical-debt.md`, not a code comment; starting a task marks `In progress`; finishing moves it to the changelog with the local time.
  - `next`: one recommendation + two alternatives, in the conversation language, no emojis, offers to mark it in progress.
  - `audit`: confirms before writing, doesn't repeat debt already resolved in the changelog.
  - No subcommand: shows the help in the user's language.
- **Done when:** every case passes or has its fix recorded here.
- **Date:** 2026-10-25 · **Status:** Open
