# testing

This repository tests Git/GitHub performance and Bistro review behavior with a static diff fixture, not a runnable application. There are no project type-check, lint, or test scripts. `git diff --check` checks tracked working changes for whitespace errors, not TypeScript correctness or Bistro behavior.

## Fixture checkpoints

1. **Baseline (Task 1):** `a.ts`, `b.ts`, and `removed.ts` each export a distinct baseline string constant. The controller reviews and commits this baseline, then creates `bistro-test/base` before Task 2.
2. **Initial PR patchset (Task 2; not executed yet):** change only the string value in those three files. Expect exactly three modified files relative to the fixture base. Load the PR in Bistro and record its review/mark-viewed state, then stop until the user explicitly says `continue` before any later patchset.
3. **Later patchset 2 (not executed now):** change only `b.ts` relative to the initial review, add `new.ts`, delete `removed.ts`, and leave `a.ts` unchanged. Expected since-review classification: `a.ts` unchanged, `b.ts` changed, `new.ts` new, `removed.ts` removed. A deleted file remains in the PR diff even though it is missing from the tree. Record the review/viewed checkpoint, then stop until the user explicitly says `continue` before the next patchset.
4. **Later patchset 3 (not executed now):** advance the isolated fixture base by inserting lines before the existing content of `a.ts`, then force-push a pure rebase of patchset 2 with no additional feature edits. Check upstream-only changes against the saved review/viewed state: `a.ts` content is unchanged since review despite shifted line positions; `b.ts` and `new.ts` remain present and `removed.ts` remains deleted.

A separate PR 2 settings-reset check is a later checkpoint, not established by this baseline. App-upgrade, cache/head-loss, and settings-reset outcomes require manual verification; these small fixtures do not automatically establish them or demonstrate that all tests pass.

The controller handles all commits, refs, pushes, rebases, and PR creation after review. Never move or push `master`. Keep `.bistro-setup/` artifacts untracked and unpublished. Stop at each approved checkpoint; do not execute future patchsets without instruction.
