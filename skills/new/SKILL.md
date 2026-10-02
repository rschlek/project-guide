---
name: new
description: >-
  Create a new project to the project standard: a named folder under the
  projects root from the template, the standard files including a local copy
  of the conventions, project.yaml filled, git initialized, worktrees ignored,
  a remote created (private unless the user decides it is internal or
  public), and a first commit pushed. Use when the user says "new project",
  "start a project", "create a repo for X", "set up a project for X", or
  "scaffold a project to the standard". Do NOT use for an existing
  repository (that is adopt), or for adding a worktree to a project.
---

# New project

## Procedure

1. Read `${CLAUDE_PLUGIN_ROOT}/references/conventions.md` for the rules.
2. Locate the profile: the path in the environment variable
   `PROJECT_GUIDE_PROFILE` when it is set and the file exists; else the path
   written in the one-line file `.project-guide` in the user's home folder. If
   neither exists, ask the user where the projects root is and offer to create
   a profile from `${CLAUDE_PLUGIN_ROOT}/references/profile.example.yaml`.
3. Ask for the scope (from the profile's list), the subject, a human-readable
   title, a one-sentence summary saying what it is and who it is for, and
   whether it is private, internal, or public (private unless the user
   decides otherwise). Ask once whether other people work on the project.
   Build the name per the naming rule. Stop if a folder of that name already
   exists under the projects root.
4. Copy `${CLAUDE_PLUGIN_ROOT}/template` to `<projects_root>/<name>`.
5. In `project.yaml`, set `project` to the name, and `title`, `summary`, and
   `scope`, plus `visibility: internal` or `visibility: public` for an
   internal or public project, and `shared: true` when other people work on
   it; otherwise leave that line out. Put the title and the summary in
   `README.md`.
6. Fill the base block and write the conventions copy with Python 3.9 or
   later: `python ${CLAUDE_PLUGIN_ROOT}/scripts/sync.py --repo
   <projects_root>/<name> --add --worktrees-dir <worktrees_dir>`, with the
   profile's worktrees folder (default `.claude/worktrees`). It sets the
   worktrees folder in the `AGENTS.md` block and writes
   `docs/project-conventions.md` at the standard version.
7. Check that no `<...>` placeholder remains in `README.md`, `project.yaml`,
   `AGENTS.md`, or the copy's first line (the rules themselves use `<...>`
   in examples).
8. Initialize git on `main`. Add a `.gitignore` that ignores the profile's
   worktrees folder.
9. For a public project, first run the cleaning pass from the conventions:
   nothing identifying in the files, the commit identity the user wants
   published, and a license the user picks. For an internal project, check
   the files against the internal rule. Then confirm with the user and
   create the remote, with the visibility the user chose, named after the
   folder, on the host and namespace the profile gives for the scope, and add
   it as `origin`.
10. Make the first commit, whether or not a remote exists. Push only when
    `origin` exists and the user confirms.

## Notes

- Creating the remote and pushing are outward-facing; each needs the user's
  go, for a public project too, after the cleaning pass. If the user
  declines the remote, leave the project local and say that it has no remote
  yet, which the standard requires.
- Never write credentials or data extracts into the new project.
