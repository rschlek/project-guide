---
name: new
description: >-
  Create a new project to the project standard: a named folder under the
  projects root from the template, the four standard files, project.yaml
  filled, git initialized, worktrees ignored, a private remote created, and a
  first commit pushed. Use when the user says "new project", "start a
  project", "create a repo for X", "set up a project for X", or "scaffold a
  project to the standard". Do NOT use for an existing repository (that is
  adopt), or for adding a worktree to a project.
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
   title, and a one-sentence summary saying what it is and who it is for.
   Build the name per the naming rule. Stop if a folder of that name already
   exists under the projects root.
4. Copy `${CLAUDE_PLUGIN_ROOT}/template` to `<projects_root>/<name>`.
5. In `project.yaml`, set `project` to the name, and `title`, `summary`, and
   `scope`. Put the title and the summary in `README.md`. No `<...>`
   placeholder may remain in any file.
6. Initialize git on `main`. Add a `.gitignore` that ignores the profile's
   worktrees folder.
7. Confirm with the user, then create the private remote, named after the
   folder, on the host and namespace the profile gives for the scope, and add
   it as `origin`.
8. Make the first commit, whether or not a remote exists. Push only when
   `origin` exists and the user confirms.

## Notes

- Creating the remote and pushing are outward-facing; each needs the user's
  go. If the user declines the remote, leave the project local and say that
  it has no private remote yet, which the standard requires.
- Never write credentials or data extracts into the new project.
