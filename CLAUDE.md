# Repo conventions for Claude Code

## Minimize GitHub Actions costs — standing, every repo

Owner ask 2026-09-20, standing, **strong emphasis**: every session working
in this repo (and every other repo this account uses — this is a personal
account policy, not repo-specific, so it lives in each repo's own
`CLAUDE.md`/`AGENTS.md` rather than being assumed to carry over
automatically) must actively minimize GitHub Actions minutes and
API/runner load. CI time is a real, metered cost, not a free side-effect
of pushing.

**Before pushing:**

- **Verify everything possible locally first** — run this project's own
  tests, linters, or build, whatever exists, before pushing. A push that
  turns CI red because a check that could have run locally wasn't run is
  a wasted CI cycle.
- **Batch fixes into one push, not several.** Finish resolving every
  conflict/failure visible before pushing, rather than pushing after each
  individual fix and letting CI re-run on every intermediate state.
- **One push per logical change per branch** — no speculative or
  exploratory pushes to see what CI says.

**While a PR is open (once this repo has CI):**

- **Never poll CI in a tight loop.** Use webhook subscriptions or a
  scheduled check-in spaced in tens of minutes, not repeated immediate
  re-checks.
- **Never re-run a job speculatively** — only to confirm a genuine flake,
  at most once.
- **Never push an empty commit or close/reopen a PR to kick CI.**
- **Don't dispatch a scheduled/manual workflow** unless the task
  actually needs its output.

**Current state (as of 2026-09-20): this repo has no GitHub Actions
workflows configured.** This section is a standing default that applies
the moment any are added, so the discipline doesn't have to be
re-derived later — not a claim that CI exists today.

This governs *how much CI runs*, not *what gets merged* — it never
licenses skipping a required check or weakening a guardrail. The
cheapest CI run is the one that passes the first time because the
change was verified locally first.
