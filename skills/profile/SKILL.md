---
name: profile
description: >-
  Create, show, or change the project-guide profile: the one file per user on
  each machine that holds the projects root, the worktrees folder, the scopes
  with their hosts and namespaces, the default tracker, and where each memory
  kind lives. Use when the user says "set up my profile", "create the
  project-guide profile", "show my profile", "change my projects root", or
  "point the shared memory somewhere else", and when the new, adopt, or sync
  skill finds no profile. Do NOT use to change a project's project.yaml (that
  is adopt), or to store credentials.
---

# Profile

## Procedure

1. Read `${CLAUDE_PLUGIN_ROOT}/references/conventions.md` ("The profile")
   and `${CLAUDE_PLUGIN_ROOT}/references/profile.example.yaml` for the shape.
2. Locate the profile: the path in the environment variable
   `PROJECT_GUIDE_PROFILE` when it is set; else the path written in the
   one-line file `.project-guide` in the user's home folder. Then do what
   the user asked: create it when the file is missing, show it, or change
   one value.
3. Create. Ask in one batch, offering the example's defaults:
   - `projects_root`: the one flat folder holding every project.
   - `worktrees_dir`: where worktrees nest inside a project (default
     `.claude/worktrees`).
   - `scopes`: for each, a name, its meaning, whether it is a name prefix,
     and the remote host and namespace its projects go to.
   - `tracker`: the default tracker's kind (one that has a recipe, a skill
     to create, read, update, and close a ticket there) and its URL pattern
     with `{key}`.
   - `memory`: for `personal` and `shared`, the kind of memory and the
     location; `repo` needs none. Leave a kind empty when the user has none.
   - `shared_namespaces`, optional: remote namespaces of repos other people
     use, so sync sends their updates through review.
   Ask where to keep the file when the environment variable does not name
   one (suggest `.project-guide.yaml` in the home folder). Write it in the
   example's shape and order, with only the user's answers, then write the
   one-line `.project-guide` pointer holding its path, unless the
   environment variable already names it. Show the result.
4. Show. Print the profile's values grouped as in the example, and say which
   file they came from and how it was found.
5. Change one value. Show the current value and the new one, write only that
   key, and leave every other line, comment, and the file's line endings as
   they are. A changed `projects_root` or `worktrees_dir` moves nothing on
   disk: say so, and that existing projects and worktrees stay where they
   are until the user moves them.
6. When another skill called this one, return to that skill's next step
   with the profile's path.

## Notes

- One profile per user on each machine. It holds locations and names, never
  credentials, tokens, or passwords; for a memory or tracker that needs a
  key, it names the location only.
- The profile is the only place the actual memory locations are named.
  `project.yaml` names only the memory kind, so never copy a location from
  the profile into a project.
- Never create the profile inside a project's repository, and never commit it.
- Writing the profile or the pointer file changes only those two files;
  nothing under the projects root is touched.
