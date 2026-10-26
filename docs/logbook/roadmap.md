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
