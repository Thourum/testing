# Fixture instructions

- This is a static Git/Bistro diff fixture, not a runnable application. See README.md for expected results and review/viewed checkpoints.
- There are no dependencies or runnable type-check, lint, or test scripts. Do not add frameworks or fabricate check commands; trivial string constants need no tests.
- Run `git diff --check` to validate whitespace in tracked working changes. It does not validate untracked files, TypeScript semantics, or Bistro outcomes; inspect new file paths and contents separately.
- Work only on the approved task in this existing worktree. The controller handles commits, refs, pushes, rebases, and PRs after review; never move or push `master`.
- Keep `.bistro-setup/` untracked and unpublished. Future patchsets require explicit user `continue`. Worker agents must not spawn nested subagents; the controller continues subagent-driven development. Do not change permissions/settings.
