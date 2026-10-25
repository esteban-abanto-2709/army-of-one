# Agent rules — the block `init` writes

The day-to-day rules (recording debt, task lifecycle, codes) must apply in
**every** session, even when the skill isn't loaded. That's why `init` copies
this block into the instructions file the agent always reads (see `init.md`,
step 6).

Copy it **as is**, markers included, filling in `<language>` with the document
language. Everything between `<!-- logbook:start` and `<!-- logbook:end -->`
belongs to the skill: running `init` again replaces it whole (keeping the
language line).

~~~markdown
<!-- logbook:start — written by the logbook skill (init); replaced whole when it runs again -->
## Logbook (`docs/logbook/`)

Logbook language: <language>

Every project records its work in four git-versioned files under
`docs/logbook/`. `docs/` itself stays for conceptual material (vision,
definition); the operational record lives under `docs/logbook/`.

| File | Prefix | Holds |
|---|---|---|
| `technical-debt.md` | `TD-###` | Something **wrong now** in existing code. |
| `roadmap.md` | `RM-###` | **Committed** work that will be done. |
| `wishlist.md` | `WL-###` | Ideas, **maybe never**. |
| `changelog.md` | — | **Permanent** record of everything finished. |

**Passive rules (always on, no command):**

- **Language:** logbook entries are written in the logbook language above; the
  conversation stays in the user's language. If the existing files are in
  another language, keep theirs (never mix) and mention that `init` can
  translate them.
- **Technical debt:** if you notice it while working, record it in
  `technical-debt.md` (never as a code comment). Entry format:

  ```markdown
  ## [TD-001] Short title
  - **Location:** `path/to/file.ext:line`
  - **Risk:** N/10  (1-3 cosmetic · 4-6 slows down/moderate · 7-9 latent bug or security · 10 critical)
  - **Problem:** what's wrong, condensed.
  - **Future impact:** what it can cause if left alone.
  - **Date:** YYYY-MM-DD · **Status:** Open
  ```

- **Task lifecycle:** when **starting** a task (`RM`, `TD` or `WL`) mark it
  `In progress (YYYY-MM-DD)` in its file; when **finishing**, move it to
  `changelog.md` keeping its prefix and delete it from its file. Changelog
  format (reverse order): `## [CODE] Title (YYYY-MM-DD HH:MM)` + summary in ≤2
  lines. **The date/time is the local clock at finish; never query git for
  it.**
- **Codes:** never reused; the next one = highest used +1 looking at the open
  file + changelog. Executing a task doesn't change its code: a `WL` is worked
  on directly and goes into the changelog as `WL`. Promoting `WL → RM` is only
  a priority decision the user asks for, never a prior step.
- **Files on demand:** don't create empty files; each one is born the first
  time there is something real to put in it.

**Heavy mechanics → `logbook` skill:** to set up or migrate the system
(`init`), recommend a task (`next`) or audit debt (`audit`), use the skill. It
holds the full formats, special cases (WL→RM promotion, wontfix) and
procedures.
<!-- logbook:end -->
~~~
