---
name: sync
description: >-
  Bring the project-guide base block and conventions copy up to date in every
  adopted repository under the projects root in one run: plan, show the user,
  then write, commit by path, and push on the user's go, opening a pull
  request where the default branch refuses a direct push. Use when the user
  says "sync my projects", "roll out the standard", "update the repos to the
  new version of the standard", or "which repos are behind the standard". Do
  NOT use to bring a repository to the standard for the first time (that is
  adopt), to create a project (that is new), or to change project.yaml.
---

# Sync the standard

## Procedure

1. Locate the profile: the path in the environment variable
   `PROJECT_GUIDE_PROFILE` when it is set and the file exists; else the path
   written in the one-line file `.project-guide` in the user's home folder. If
   neither exists, ask the user where the projects root is. Read its
   `projects_root` and `worktrees_dir` (default `.claude/worktrees`).
2. Plan, which only reads, with Python 3.9 or later:
   `python ${CLAUDE_PLUGIN_ROOT}/scripts/sync.py --root <projects_root>
   --worktrees-dir <worktrees_dir> --json`. Narrow it with `--only a,b` or
   `--skip a,b` when the user names repos.
3. Show the user the table: each repo's state, action, and reason, and the
   standard version. Say which repos will be updated, which will only get a
   local copy, and which are skipped and why.
4. On the user's go, run the same command with `--push`. For a run the user
   wants kept local, use `--commit` (commits, no push) or `--apply` (writes,
   no commit). A repo without a remote is committed and left unpushed.
   Before the run, say that other sessions may be working in these repos;
   the script skips any repo with a lock, staged work, local changes to the
   two files, a different branch checked out, or a branch behind its remote.
5. For each repo reported as "needs a pull request", the script has pushed
   the commit to the named `standard/project-guide-<version>` branch. Open a
   pull request from that branch into the default branch through the repo's
   review process, with whatever connected tool serves that host, and say
   so. If no tool can, give the user the branch name and the repo. Say what
   the script reports about the local default branch: it keeps the commit
   and is ahead of its remote until the pull request merges.
6. Report the result: repos updated, repos with a pull request, repos with a
   local copy only, and each skipped repo with its reason, so the user can
   clear the cause and run sync again.

## Notes

- A repo the plan marked skip is never touched, not even by hand to finish
  the job; the user clears the reason and runs sync again.
- Sync never adopts a repo, never sets `visibility` or any other
  `project.yaml` field, and never moves, renames, or deletes anything.
- The script writes only `AGENTS.md`, inside the base block markers, and
  `docs/project-conventions.md`, and commits exactly those two paths. In a
  repo whose copy is excluded from git (one someone else owns), it updates
  the local copy and never commits.
- It never stashes, forces, rewrites history, or changes the commit
  identity. A run on an unchanged standard reports every repo current.
