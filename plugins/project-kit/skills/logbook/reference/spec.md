# Logbook — full convention

All project work is recorded in four files under `docs/logbook/`, **always
versioned in git** (git is the backup for everything that gets deleted). `docs/`
itself stays for conceptual material (vision, project definition); the
operational record lives under `docs/logbook/`.

| File | Prefix | Holds |
|---|---|---|
| `technical-debt.md` | `TD-###` | Something **wrong now** in existing code. |
| `roadmap.md` | `RM-###` | **Committed** work that will be done. |
| `wishlist.md` | `WL-###` | Ideas, **maybe never**. |
| `changelog.md` | — | **Permanent** record of everything finished. |

Folder ready, files on demand: each file is created (with its header template
below) the first time there is something real to put in it. Don't create empty
files, or any file other than these four.

## Language

Two languages, kept apart:

- **Document language:** what the logbook files are written in. Configurable.
- **Conversation language:** what you answer the user in (recommendations,
  summaries, help). Always the language the user is speaking.

The document language is set by a line `Logbook language: <language>` in the
agent's instructions files. Resolve it in this order:

1. A `Logbook language:` line in the project's `CLAUDE.md` / `AGENTS.md`.
2. Otherwise, the line in the user's global instructions file.
3. Otherwise, the language the existing logbook files are written in.
4. Otherwise (new project, nothing configured): `init` asks; outside `init`,
   use the conversation language.

**Never mix languages inside the logbook.** If the configured language and the
existing files disagree, keep writing in the files' language and tell the user,
once, that `init` can translate them. Text kept as is because it is literal
(code, product text, quotes; see "Translating" in `init.md`) isn't mixing.

Templates below are in English. Which labels to use:

- **Creating a file:** the template, in the document language.
- **Adding to an existing file:** the labels the file already uses.
- **Translating a file** (`init`): the template in the new language.

## Code rules

- **One counter per prefix.** `TD`, `RM` and `WL` each count on their own,
  starting at `001`: the first debt is `TD-001` even if `RM-005` exists. The
  next number for a prefix = highest code **with that same prefix** +1, looking
  at its open file + the changelog; codes with other prefixes don't count.
  (Older logbooks that used one shared counter keep their codes; they simply
  continue from each prefix's highest.)
- **Never reused.** (A code burned by a process mistake that never represented
  a real task may be reclaimed.)
- The prefix only says which file the task lives in (`RM-007` → `roadmap.md`).

## Task lifecycle

The user asks to work by code: *"let's work on RM-007…"*. It works the same
for `RM`, `TD` and `WL`: a `WL` **is executed straight from the wishlist**,
without promoting it first.

1. **On start:** mark the entry `In progress (YYYY-MM-DD)` in its file (a WIP
   marker, in case the session is cut short).
2. **On finish:** move the entry to the changelog **keeping its own prefix** (a
   finished `WL` goes in as `WL`, a `TD` as `TD`) and **delete it** from its
   file. The changelog records all three types.

Executing a task **doesn't change its code**.

## Special cases

- **Promoting `WL → RM`:** a **priority decision**, not a step to execute: the
  user decides an idea becomes committed work, even if it won't be done now.
  Only when the user asks; never propose it as a requirement to work on a `WL`.
  Delete the `WL`, create a new `RM`. **It doesn't go through the changelog**
  (nothing was finished, only moved).
- **Discarding (wontfix):** **silent deletion** from its file. Git keeps the
  history; nothing goes to the changelog.
- **Unified technical debt:** a resolved `TD` **also** moves to the changelog
  and is deleted. No `Status: Resolved` is kept inside the file.

## Timestamps

The changelog date and time are the local clock when the task is finished.
**Never query git (or any other external source) for them:** the commit comes
later, when the user makes it, so its time is not when the work ended.

---

# Formats and headers

## `technical-debt.md` (`TD-###`)

Entry:

```markdown
## [TD-001] Short title
- **Location:** `path/to/file.ext:line`
- **Risk:** N/10
- **Problem:** Condensed description of what's wrong.
- **Future impact:** What it can cause if left alone.
- **Suggestion:** (optional) how to fix it, in one line.
- **Date:** YYYY-MM-DD · **Status:** Open
```

Risk scale:

```
1-3  cosmetic / no functional impact
4-6  slows development down or moderate risk
7-9  latent bug, data loss or security
 10  critical, tackle immediately
```

Header template (when creating the file):

```markdown
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
```

## `roadmap.md` (`RM-###`)

Ordered by priority: the top entry is the next one to do. New entries go where
their priority puts them, not at the end.

Entry:

```markdown
## [RM-001] Short title
- **Goal:** what we want to achieve.
- **Scope:** (optional) what's in and what's out.
- **Open questions:** (optional) what must be decided when starting.
- **Done when:** clear completion criterion.
- **Date:** YYYY-MM-DD · **Status:** Open
```

Header template:

```markdown
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
```

## `wishlist.md` (`WL-###`)

Entry (lightweight, no fields):

```markdown
## [WL-001] Short title
The idea in 1–2 lines.
```

Header template:

```markdown
# Wishlist

Possible ideas and improvements, no commitment (maybe never). Code `WL-###` (never reused).
If an idea is promoted, it's deleted from here and a new `RM` is born.

**Format:** title + the idea in 1–2 lines, no fields.

---
```

## `changelog.md`

Entry (reverse order, newest on top):

```markdown
## [CODE] Title (YYYY-MM-DD HH:MM)
Summary in ≤2 lines of what was done.
```

Header template:

~~~markdown
# Changelog

Permanent record of all finished work. Indexed by task code
(`TD-`, `RM-`, `WL-`). Reverse order: newest on top.

**Entry format:**

```
## [CODE] Title (YYYY-MM-DD HH:MM)
Summary in ≤2 lines of what was done.
```

---
~~~
