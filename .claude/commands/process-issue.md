---
description: Work a GitHub issue end to end — plan, build, test, open a PR
argument-hint: <issue number>
---

Work on GitHub issue #$ARGUMENTS for Inkwell. Read `CLAUDE.md` first and follow its hard rules.

# PLAN
1. Run `gh issue view $ARGUMENTS` to get the issue details.
2. Understand the problem the issue describes. Its "Out of Scope" section is binding.
3. Ask me clarifying questions if anything is ambiguous. Don't guess on anything touching ink, sync or file format.
4. Look for prior work on this issue:
   - Search `scratchpads/` for earlier notes.
   - Search PRs (`gh pr list --state all --search "<keywords>"`) for history.
   - Search the codebase for relevant files, and read `PLAN.md` for decisions that are already settled.
5. Think hard about splitting the issue into small, manageable tasks.
6. Write the plan in a new scratchpad, `scratchpads/<issue#>-<slug>.md`, including a link to the issue.

# CREATE
- Create a branch: `git checkout -b issue-$ARGUMENTS-<slug>`.
- Solve the issue in small steps, following the plan.
- Commit after each step with a descriptive message that references the issue (e.g. "Add Stroke codec round-trip #5"). One logical change per commit.
- Push straight after every commit: `git push origin <branch-name>`.

# TEST
- Write Swift Testing / XCTest tests for the expected behaviour. NoteCore logic must have unit tests. Every ink transform needs tests that show its input is unchanged and that revert is exact.
- If the UI changed, use XcodeBuildMCP to build, launch the iPad simulator, click through the change and take screenshots.
- Run the full suite (`swift test --package-path NoteCore`, then `xcodebuild test` for the app) and `swiftlint`.
- If tests fail, fix them. All tests must pass before you move on.

# DEPLOY
- Open a PR with `gh pr create`. The body should link the issue ("Closes #$ARGUMENTS") and end with:
  - **Built**: what changed
  - **Tested**: what was tested, and how
  - **Untested / risks**
  - **Manual iPad/Mac checks for Luca**: exact steps and what to look for. Write "None" if there aren't any.
- Stop there. Luca checks that CI is green, merges, and runs `/clear` before the next issue.
