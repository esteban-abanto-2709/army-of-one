# Changelog

Permanent record of all finished work. Indexed by task code
(`TD-`, `RM-`, `WL-`). Reverse order: newest on top.

**Entry format:**

```
## [CODE] Title (YYYY-MM-DD HH:MM)
Summary in ≤2 lines of what was done.
```

---

## [TD-010] Codes counted across prefixes (2026-10-25 22:21)
The numbering rule now says one counter per prefix, starting at `001`, in `spec.md`, the agent block, `init` and `audit`; existing codes are not renumbered.

## [RM-004] Test the published skill with an agent (2026-10-25 19:38)
Installed from GitHub and run by a fresh session on a third-party repo plus three sandboxes: help, `init` (twice), `audit`, `next`, lifecycle and every block destination passed, with Spanish templates. Gaps found are in TD-009.

## [TD-008] init still left three small cases to guesswork (2026-10-25 19:26)
`init.md` now says a loose line repeating a logbook rule counts as an unmarked section, a project's own header note goes after the template's `---`, and one `init` run is one commit.

## [TD-007] init gaps found translating a real logbook (2026-10-25 16:51)
The block now always goes into the project and the user's global file never changes that and is never edited; `init` gains a translation procedure (what stays literal, header, verification), skips set-up steps when the logbook exists, and `spec.md` settles which labels to use.

## [RM-002] Use the repo version of the skill (2026-10-25 16:28)
This folder is a local marketplace and `project-kit` is installed from it; edits to the repo load in place, no reinstall. The old copy in `~/.claude/skills/logbook` is gone.

## [RM-003] README and LICENSE (2026-10-25 16:24)
MIT `LICENSE`, a root `README.md` (what it is, install, the logbook commands, always-on block, language) and a short `project-kit` README; `plugin.json` gains homepage, repository, license and keywords.
