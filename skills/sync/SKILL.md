---
name: sync
description: >-
  Bring the project-guide base block and conventions copy up to date in every
  repository under the projects root whose project.yaml is committed, adding
  them where missing, and keep a local copy current where project.yaml is
  local only; archived projects are skipped. Plan, show the user, then write,
  commit by path, and push on the user's go; a repo other people use always
  gets a review branch and a pull request. Use when the user
  says "sync my projects", "roll out the standard", "update the repos to the
  new version of the standard", or "which repos are behind the standard". Do
  NOT use for a repository without a committed project.yaml (bringing it to
  the standard is adopt), to create a project (that is new), or to change
  project.yaml.
---

# Sync the standard

## Procedure

1. Locate the profile: the path in the environment variable
   `PROJECT_GUIDE_PROFILE` when it is set and the file exists; else the path
   written in the one-line file `.project-guide` in the user's home folder. If
   neither exists, ask the user where the projects root is. Read its
   `projects_root`, `worktrees_dir` (default `.claude/worktrees`), and the
   optional `shared_namespaces` list.
2. Plan, which only reads, with Python 3.9 or later:
   `python ${CLAUDE_PLUGIN_ROOT}/scripts/sync.py --root <projects_root>
   --worktrees-dir <worktrees_dir> --shared-namespaces <a,b> --json`, leaving
   out `--shared-namespaces` when the profile lists none. Narrow it with
   `--only a,b` or `--skip a,b` when the user names repos.
3. Show the user the table: each repo's state, action, and reason, and the
   standard version. Say which repos will be updated, which will only get a
   local copy, and which are skipped and why.
4. On the user's go, run the same command with `--push`. For a run the user
   wants kept local, use `--commit` (commits, no push) or `--apply` (writes,
   no commit). A repo without a remote is committed and left unpushed.
   Before the run, say that other sessions may be working in these repos;
   the script skips any repo with a lock, staged work, local changes to the
   two files, a different branch checked out, or a branch behind its remote.
   A shared repo (its `origin` is in a shared namespace) always goes through
   review: the script reads it from the remote default branch, builds the
   commit without touching the checkout, and pushes it only to a review
   branch. Only when the user specifically approves a direct change for named
   repos in this run, add `--direct <a,b>`; those repos take the ordinary
   path.
5. For each repo reported as "needs a pull request", the script has pushed
   the commit to the named `standard/project-guide-<version>` branch. Open a
   pull request from that branch into the default branch through the repo's
   review process, with whatever connected tool serves that host, and say
   so. If no tool can, give the user the branch name and the repo. For an
   own repo whose remote refused the push, say what the script reports: the
   local default branch keeps the commit until the pull request merges.
6. Report the result: repos updated, repos with a pull request, repos with a
   local copy only, and each skipped repo with its reason, so the user can
   clear the cause and run sync again.

## Notes

- A repo the plan marked skip is never touched, not even by hand to finish
  the job; the user clears the reason and runs sync again.
- Which repos it covers: one whose `project.yaml` is committed gets the
  block and the copy, added where missing and kept current; one whose
  `project.yaml` is local only (a repo someone else owns) gets a local copy;
  one with no `project.yaml`, or one not committed yet, is left to adopt
  unless it already carries a block or a copy. A project whose
  `project.yaml` says `archived` is always skipped; a parked one is not.
  The standard's own repository is skipped.
- Sync never sets `visibility` or any other `project.yaml` field, and never
  moves, renames, or deletes anything.
- The script writes `AGENTS.md` (the block only, or a new file from the
  template) and `docs/project-conventions.md`, and commits only those paths.
  Where `project.yaml` or the copy is local only, it never commits and never
  touches a tracked `AGENTS.md`; it may add the copy's path, once, to the
  repo's local exclude file so the copy never shows as untracked.
- It never stashes, forces, rewrites history, or changes the commit
  identity. A run on an unchanged standard reports every repo current.
- On a shared repo the script never reads or writes the working tree, the
  index, or a local branch, and never pushes the default branch. A review
  branch that already exists with other content is reported, not forced.
