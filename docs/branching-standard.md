## Rule

Every task gets its own branch. Never commit directly to `main`; it only changes by merging a finished task branch.


## Naming

```
t-<NN>-<short-slug>
```

- `NN` is the task number, matching the ClickUp task (`t-02`, `t-03`).
- `short-slug` is 2-4 lowercase, hyphenated words naming the deliverable.
- Examples: `t-02-frame-spec`, `t-03-motors-props`.
- Work not tied to a task (tooling, docs fixes) uses a short descriptive name, such as `docs-branching-standard`.


## Workflow

1. Start from an up-to-date `main`:
   ```
   git switch main && git pull
   git switch -c t-<NN>-<short-slug>
   ```
2. Commit on the branch following `docs/commit-standard.md`.
3. When the task's done-test is met, open a pull request into `main`.
4. After the merge, delete the branch.


## Rules

- One task per branch, matching the one-task-per-commit rule.
- Branch from `main`, not from another task branch, unless the task depends on unmerged work. Say so in the PR if it does.
- If you notice you are on `main` with uncommitted work, create the branch before committing: `git switch -c t-<NN>-<short-slug>`.


## Before you start

- [ ] On `main` and up to date before branching
- [ ] Branch name is `t-<NN>-<short-slug>`
- [ ] `git branch --show-current` is not `main`
