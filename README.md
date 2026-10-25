# army-of-one

Skills for developers who build projects on their own with AI.

When you work alone, nobody keeps the backlog, remembers the shortcuts you took
or tells you where to start today. These skills give that job to your coding
agent, in plain Markdown files that live in your repo.

## Plugins

| Plugin | What it does | Skills |
|---|---|---|
| [`project-kit`](plugins/project-kit) | Keep a project on course: what was done, what's next, what's wrong | `logbook` |

## Install

In Claude Code, add the catalog once:

```bash
claude plugin marketplace add esteban-abanto-2709/army-of-one
```

Then install the plugin:

```bash
claude plugin install project-kit@army-of-one
```

The skills follow the open [Agent Skills](https://agentskills.io) format, so
other agents can use them too: copy a skill folder (for example
`plugins/project-kit/skills/logbook`) into wherever your agent loads skills
from.

## logbook

A git-versioned project logbook under `docs/logbook/`, with four files:

| File | Code | Holds |
|---|---|---|
| `technical-debt.md` | `TD-###` | Something wrong now in existing code, with a 1-10 risk. |
| `roadmap.md` | `RM-###` | Committed work, ordered by priority. |
| `wishlist.md` | `WL-###` | Ideas, maybe never. |
| `changelog.md` | — | Permanent record of everything finished. |

Every entry has a code that is never reused, so you can just say *"let's work
on RM-007"*. When a task starts it's marked in progress; when it's done it
moves to the changelog with its code.

### Commands

Run them as `/project-kit:logbook <command>`, or just ask in your own words.

- `init` — set up the logbook in this project, or migrate the TODO lists,
  backlogs and changelogs you already have into it.
- `next` — recommend one task to start with. It favors getting started over
  "the most important thing", which is usually the most overwhelming one.
- `audit` — sweep the code for technical debt. Nothing is written until you
  approve the findings.

### Always on

`init` writes a short, marked block into your `CLAUDE.md` or `AGENTS.md` (only
one of them), so the agent follows the rules in every session, even when the
skill isn't loaded: debt goes to the logbook instead of a code comment,
finished tasks move to the changelog. Running `init` again replaces the block
without touching the rest of the file.

### Language

The logbook can be written in any language, separate from the one you talk in.
`init` asks and saves it in the block as `Logbook language: English`. A
logbook never mixes languages: if the files are in another language, `init`
offers to translate them, keeping every code.

## License

[MIT](LICENSE)
