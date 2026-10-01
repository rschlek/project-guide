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
   `PROJECT_GUIDE_PROFILE` when it is set and the file exists; else the path
   written in the one-line file `.project-guide` in the user's home folder. If
   neither exists, ask the user where the projects root is and offer to create
   a profile from `${CLAUDE_PLUGIN_ROOT}/references/profile.example.yaml`.
3. Look at the repo: folder name, remotes, README, existing agent files,
   `.gitignore`, and any existing `project.yaml`. If the working tree is not
   clean or another session appears to be working in the repo, stop and
   report before writing anything.
4. Add whichever of the four standard files are missing, from
   `${CLAUDE_PLUGIN_ROOT}/template`. Never overwrite an existing README or
   agent file. If a long `CLAUDE.md` exists with no `AGENTS.md`, propose moving
   its content into `AGENTS.md` and ask before doing it.
5. Fill `project.yaml` from what the repo shows: `project` from the folder
   name; `title` from the README's first heading; `scope` from a scope the
   profile marks as a prefix when the folder name starts with it, else the
   one scope whose host and namespace match the remote, else empty and ask;
   `summary` drafted from the README and confirmed with the user (if the user
   cannot confirm, write the draft and list it as unconfirmed). Leave unknown
   fields empty. If `project.yaml` already exists, fill only its empty fields
   and propose changes to filled ones.
6. Report what is still missing against the standard, such as no remote, a
   name that does not match the naming rule, a repo not directly under the
   profile's projects root, worktrees not ignored, or committed credentials.
   Say which files were added and that they are left uncommitted.

## Notes

- Change nothing beyond adding files unless the user agrees.
- Added files follow the repo's own line-ending and formatting rules.
- Never move or rename the repository.
- In a shared repo, propose the local exclude file rather than editing
  `.gitignore`.
