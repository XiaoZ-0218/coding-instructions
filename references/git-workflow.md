# Git commit & branch workflow

## Upstream branch & worktrees

- **Upstream branch**: the branch you cut feature branches from and eventually merge back into.
- When the user is already in a **git worktree**: that worktree's current branch is the upstream. Cut the feature branch **inside the same worktree**; do **not** create extra worktrees.

## 0. New project initialization

For a new project, **initialize Git first**, then write business code:

```bash
git init
# create a proper .gitignore and README.md
git add -A && git commit -m "chore: initial commit"
```

- Do **not** attach remotes automatically; the user handles remotes.

### Python projects

If the project uses Python, use **[uv](https://docs.astral.sh/uv/)** for dependency and environment management:

```bash
uv init
uv python pin 3.12
uv add pytest
uv run pytest
```

- Prefer `uv add`, `uv run`, and `uv sync` over `pip`, `pipenv`, `poetry`, or `conda`.
- Commit `uv.lock` for reproducible environments.
- Full conventions: [python.md](python.md).

## 1. Feature-branch development

Before starting a feature/fix, cut a branch from upstream:

| Prefix | Purpose | Example |
| ------ | ------- | ------- |
| `feature/` | New feature | `feature/user-login` |
| `fix/` | Bug fix | `fix/null-pointer-in-auth` |
| `test/` | Tests | `test/add-unit-tests` |
| `docs/` | Docs | `docs/update-readme` |

```bash
git checkout -b feature/user-login <upstream-branch>
```

## 2. Commit convention

- Format: `<type>: <description>`
- **Commit after each logical step**; split mixed intents into separate commits.
- Pausing midway: `wip: ...`
- Full type table, examples, and AI commit rules: **must read** [commit-messages.md](commit-messages.md).

## 3. Pre-merge tests & permission (mandatory)

1. Run the project's full test suite (unit/integration/e2e, as applicable).
2. After tests pass, report to the user: change summary + test results, and **explicitly ask for merge permission**.
3. Merge **only after explicit user approval**; never merge on your own.
4. If CI/CD exists, wait for the pipeline to pass.

## 4. Merging back to upstream (prefer rebase, never squash)

Default flow: **rebase the feature branch onto upstream, then fast-forward merge** — keep every individual commit, no squash, no merge node.

0. **If the repo has a remote: prefer a Pull Request** instead of a local merge — push the feature branch and open a PR (e.g. `gh pr create`), let the user review and merge it there. Only merge locally when the user explicitly asks, or when there is no remote.
1. On the feature branch, rebase onto the latest upstream:
   ```bash
   git fetch  # if a remote exists
   git rebase <upstream-branch>
   ```
   Resolve conflicts **on the feature branch**, then re-run tests.
   If the feature branch was already pushed to a remote, the rebase rewrites its history — push back with `git push --force-with-lease` (safe only for your own feature branch; never force-push shared branches).
2. Check out upstream and fast-forward merge:
   ```bash
   git checkout <upstream-branch>
   git merge --ff-only <feature-branch>
   ```
3. **Never** use squash merge (`--squash` / GitHub "Squash and merge"); each logical commit must survive intact. When merging a PR on the remote, choose **rebase merge** (or fast-forward), never squash.
4. Only fall back to `git merge --no-ff` when the user explicitly asks for a merge node (e.g. preserving a release boundary).

## 5. Post-merge cleanup

```bash
git checkout <upstream-branch>
git branch -d feature/user-login
# delete the remote feature branch too, if any
```

## AI agent git rules

1. New feature/fix: cut a feature branch before touching code.
2. **Commit proactively** after every meaningful change; don't wait to be asked.
3. User says "save progress / leave it" → `wip`.
4. Before merging: full tests → report → **wait for permission**.
5. Merging: with a remote, prefer a Pull Request; otherwise `git rebase` onto upstream + `--ff-only`; never squash; `--no-ff` only when the user explicitly asks.
