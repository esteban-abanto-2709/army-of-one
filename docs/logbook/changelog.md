# Changelog

Permanent record of all finished work. Indexed by task code
(`TD-`, `RM-`, `WL-`). Reverse order: newest on top.

**Entry format:**

```
## [CODE] Title (YYYY-MM-DD HH:MM)
Summary in ≤2 lines of what was done.
```

---

## [TD-007] init gaps found translating a real logbook (2026-10-25 16:51)
The block now always goes into the project and the user's global file never changes that and is never edited; `init` gains a translation procedure (what stays literal, header, verification), skips set-up steps when the logbook exists, and `spec.md` settles which labels to use.

## [RM-002] Use the repo version of the skill (2026-10-25 16:28)
This folder is a local marketplace and `project-kit` is installed from it; edits to the repo load in place, no reinstall. The old copy in `~/.claude/skills/logbook` is gone.

## [RM-003] README and LICENSE (2026-10-25 16:24)
MIT `LICENSE`, a root `README.md` (what it is, install, the logbook commands, always-on block, language) and a short `project-kit` README; `plugin.json` gains homepage, repository, license and keywords.
