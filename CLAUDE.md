# CLAUDE.md

This file guides Claude Code (and other agents) working in this repository.

**Read [DEVELOPMENT.md](DEVELOPMENT.md) before doing any development work here.** It is the
canonical source of truth for building, type-checking, linting, and testing. Build internals
are documented in [docs/build.md](docs/build.md).

## Work isolation

Before modifying code, documentation, tests, or configuration for a task, create a new branch
and a dedicated Git worktree for that task. Do all edits, builds, and tests from the dedicated
worktree; do not work directly in the primary checkout.

For example, from the primary checkout:

```sh
git worktree add -b <task-branch> .worktrees/<task-slug> HEAD
cd .worktrees/<task-slug>
```

Always place task worktrees under the primary checkout's `.worktrees/` directory so they remain
inside the repository workspace and its sandbox write boundary. Use a short, descriptive branch
and directory name. Before creating the worktree, inspect the current branch and working-tree
status. Do not move or copy unrelated uncommitted changes into the task worktree. If the agent
was already started inside a dedicated worktree and branch for the current task, use it instead
of creating another worktree.

## Essentials

- **Build:** `npm run build` (both targets). See [docs/build.md](docs/build.md).
- **Type-check:** `npm run typecheck` — **Lint:** `npm run lint`
- **Unit/browser tests:** `npm test` (vitest; no clipboard, runs anywhere).
- **E2E:** `npm run test:e2e:docker`. The full e2e suite **must run in Docker** — the
  clipboard-smoke project uses the real system clipboard. Read results from
  `test-results/results.json`, not stdout. See
  [DEVELOPMENT.md → E2E tests](DEVELOPMENT.md#e2e-tests-playwright).

Run `npm run typecheck`, `npm run lint`, and `npm test` before considering a change complete.

## Agent skills

### Issue tracker

Issues and PRDs are tracked in this repository's GitHub Issues. See `docs/agents/issue-tracker.md`.

### Triage labels

Triage uses the five default canonical labels. See `docs/agents/triage-labels.md`.

### Domain docs

This is a single-context repository. See `docs/agents/domain.md`.
