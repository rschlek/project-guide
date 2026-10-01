---
name: adopt
description: >-
  Bring an existing repository up to the project standard in place: add the
  missing standard files, fill project.yaml from what the repo already shows,
  and report every gap against the standard without moving or renaming
  anything. Use when the user says "adopt this repo", "bring this project up
  to the standard", "add a project.yaml", "make this repo conform", or "check
  this repo against the standard". Do NOT use for creating a new project
  (that is new), or for moving or renaming a repository.
---

# Adopt a repository

## Procedure

1. Read `${CLAUDE_PLUGIN_ROOT}/references/conventions.md` for the rules.
2. Locate the profile: the path in the environment variable
   `PROJECT_GUIDE_PROFILE`; else the path written in the one-line file
   `.project-guide` in the user's home folder. If neither exists, ask the user
   where the projects root is and offer to create a profile from
   `${CLAUDE_PLUGIN_ROOT}/references/profile.example.yaml`.
3. Look at the repo: folder name, remotes, README, existing agent files,
   `.gitignore`, and any existing `project.yaml`.
4. Add whichever of the four standard files are missing, from
   `${CLAUDE_PLUGIN_ROOT}/template`. Never overwrite an existing README or
   agent file. If a long `CLAUDE.md` exists with no `AGENTS.md`, propose moving
   its content into `AGENTS.md` and ask before doing it.
5. Fill `project.yaml` from what the repo shows: `project` from the folder
   name, `scope` from the remote's host and the profile, `summary` drafted
   from the README and confirmed with the user. Leave unknown fields empty.
6. Report what is still missing against the standard, such as no remote, a
   name that does not match the naming rule, worktrees not ignored, or
   committed credentials.

## Notes

- Change nothing beyond adding files unless the user agrees.
- Never move or rename the repository.
- In a shared repo, propose the local exclude file rather than editing
  `.gitignore`.
