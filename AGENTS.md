# Laterna

Personal render monitor and USD inspector for a Houdini/Solaris (Karma) workflow. It is also a learning project: Sandro must be able to explain and extend every part without AI.

Rules shared with other projects are in `.claude/rules/`. An agent that does
not load that directory itself reads `working.md`, `writing.md` and
`simplicity.md` there before starting.

## Status

Phase 0: verification and setup. No application code yet. See `docs/ROADMAP.md`.

## Stack (see `docs/DECISIONS.md`)

- Backend: Python (FastAPI planned). OpenUSD via `usd-core`, EXR via OpenImageIO/OpenEXR, GPU via `nvidia-ml-py`.
- Frontend: React in the browser, served by the backend.
- Render machine: Windows now, Linux later. Code must run on both. NVIDIA GPU. Houdini Education now, Indie later.

## Commands

```sh
python3 .claude/suite-check.py   # every health check in .claude/suite.json
```

Before calling a task done, run `python3 .claude/suite-check.py`. A check it
reports as skipped did not pass. Add build, test and run commands here when
Phase 1 starts.

## Where things live

- `docs/BRIEF.md`: project brief (goals, phases, non-goals).
- `docs/ROADMAP.md`: phases and the current checklist.
- `docs/DECISIONS.md`: every non-obvious choice. Add an entry when you make one.
- `docs/ARCHITECTURE.md`, `docs/CONVENTIONS.md`: structure and code style.
- `docs/brand/`: logo files and brand rules (mark, wordmark, colours).
- `docs/learn/`: beginner explanations. `docs/learn/PROGRESS.md` records what Sandro has learned and built.
- `tests/fixtures/`: real husk logs, EXRs and USD files from Sandro's machine. Houdini is not available in Claude's environment, so these are the ground truth.

## Rules

- Work in small steps.
- Prefer simple, readable code over clever code.
- Stay inside the current phase. Ask before adding anything from a later phase.
- Laterna installs nothing into Houdini and never uses a Houdini licence (no hython, no Houdini libraries).
- Laterna never converts or re-saves Houdini files, and contains no SideFX code (EULA, see DECISIONS).
- Houdini/USD/Karma behaviour: if unsure, say so and propose how to verify on Sandro's machine. Never guess.
- Every new module gets a `docs/learn/<module>.md` page in the same session.
- Update `docs/learn/glossary.md` when a new technical term appears.

## Task tracking
Work is tracked in GitHub Issues. Every issue carries a `type:`, an `area:` and
exactly one priority (`p0`-`p3`) label. The issue forms ask for it and the
`issue-priority` workflow applies it; an issue opened through the API (by an
agent) sets the label in the same call, `p2` when unclear. Close issues from
the pull request with `Fixes #N`.

## Commits & pull requests

- One pull request per piece of work, never one per tweak. Its `## Changelog`
  section gives each change a line (`- feature: ...`, `- fix: ...`,
  `- chore: ...`). Split only for risk, an independent revert or a different
  release.
- Changelog lines and titles are public release-notes copy: imperative,
  sentence case, no trailing period, no em dashes.
- Every pull request needs an `area:` label, plus a `type:` label when it has
  no Changelog section, before it can merge (the `pr-labelled` status). Which
  type: see `.github/pull_request_template.md`.

## Files that come from the template

Some files are owned by sandrogekeler/AllesSandro and must not be edited here:
`.claude/rules/template-files.md` lists them.

## Docs

Describe what is on disk, in the present tense. Intent goes in
`docs/ROADMAP.md` as an unchecked item. Unsure whether something landed?
Check before writing it down.

## Do not

- Commit secrets, `.env` files or credentials.
- Edit generated files or lockfiles by hand; regenerate them.
