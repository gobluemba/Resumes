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

## Back up the code, and back up what the code stores

Owner ask, standing: treat backup coverage as two separate questions for
every project — the code itself, and any real data or user-uploaded
files the application stores outside of git (documents, images,
resumes, database records, anything a user submitted).

The code. A single git host is not a backup — it is the primary copy.
If a repo matters, know whether a second copy exists somewhere
independent of that host (a mirror to a different provider, a periodic
bundle/archive, or equivalent) and say so plainly when asked about a
project's durability. Don't assume "it's on GitHub" answers the
question.

Data the code stores. When a project accepts uploads, stores generated
documents, or persists anything a real user provided, treat backup
coverage as a first-class question, not an afterthought:

- "Backup configured" is not the same claim as "data protected." A
  backup step that has never been exercised by an actual restore is
  unverified, not safe. State the difference plainly rather than
  treating the two as equivalent.
- A backup that lives on the same platform/provider as the primary
  storage is not independent — a single outage or account issue can
  take out both. Note this as a real gap when you see it, not a
  defensive nitpick.
- If a project handles real user data or documents and has no
  demonstrated backup/restore path at all, surface that explicitly and
  plainly — per the audit calibration rule, label it observed (if you
  can point to real data with no protection) or defensive (if it's a
  plausible-but-unconfirmed gap), and let the user decide whether to
  act, rather than silently assuming someone else already covered it.

This rule is about awareness and honest reporting — it does not
authorize building backup infrastructure unasked, migrating storage
providers, or taking any action with data on your own initiative.
Surfacing the gap and proposing the fix is the job; standing up new
infrastructure is a separate, explicit decision the user makes.
