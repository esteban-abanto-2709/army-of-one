---
name: logbook
description: Project logbook system — tracks technical debt (TD), committed roadmap work (RM), wishlist ideas (WL), and a permanent changelog under docs/logbook/. Invoke as "/logbook init" to set up or migrate the system in the current project, "/logbook next" to recommend one task to start, or "/logbook audit" to scan the codebase for technical debt. Use whenever the user wants to set up project tracking, asks what to work on next, or wants a technical-debt audit.
---

# Logbook

A lightweight, git-versioned project tracking convention that lives under
`docs/logbook/`. Four files, each with a code prefix:

| File | Prefix | Holds |
|---|---|---|
| `technical-debt.md` | `TD-###` | Something **wrong now** in existing code. |
| `roadmap.md` | `RM-###` | **Committed** work that will be done. |
| `wishlist.md` | `WL-###` | Ideas, **maybe never**. |
| `changelog.md` | — | **Permanent** record of everything finished. |

The full convention (formats, code rules, task cycle, special cases) lives in
`reference/spec.md`. The passive day-to-day rules (don't leave debt as code
comments; record it in the logbook; move finished committed tasks to the
changelog) live in a marked block that `init` writes into the agent's
instructions file (`CLAUDE.md` or `AGENTS.md`; see `reference/agent-rules.md`),
so they apply in every session even without this skill loaded — this skill is
the source of truth for the heavier mechanics and the three on-demand commands.

## How to run

1. **Always read `reference/spec.md` first.** Every subcommand depends on the
   shared convention defined there.
2. Parse the **first word** of the argument as the subcommand, then read its
   procedure file and follow it:
   - `init`  → `reference/init.md` — set up or migrate the system here.
   - `next`  → `reference/next.md` — recommend one task to start.
   - `audit` → `reference/audit.md` — scan the codebase for technical debt.
3. Anything after the subcommand is **extra context**. Example:
   `/logbook audit apps/api` scopes the audit to that path.
4. **No subcommand (just `/logbook`), or `help` / `?` / `-h`** → don't run
   anything; print this help verbatim and wait for the user to choose:

   > **Logbook** — seguimiento del proyecto en `docs/logbook/`.
   >
   > - `/logbook init` — monta o migra el sistema en este proyecto.
   > - `/logbook next` — te recomienda una tarea para arrancar (rompe la inercia).
   > - `/logbook audit` — barre el código en busca de deuda técnica.
   >
   > Podés añadir **contexto** después del subcomando, p. ej.:
   > `/logbook audit apps/api` (acota el barrido a esa ruta) ·
   > `/logbook next rápido` (sesga hacia un quick-win).
   >
   > ¿Cuál corro?

## Hard rules

- **Never query git** (or any external source) to obtain dates or times.
  Timestamps are the local clock at the moment a task is finished. Reading git
  to discover loose files during `init` migration is fine; deriving *timestamps*
  from it is not.
- Codes are **never reused** (see `reference/spec.md`).
- Respect "folder ready, files on demand": never create empty logbook files.
