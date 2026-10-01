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
3. Look at the repo: folder name, the `origin` remote, README, existing agent
   files, `.gitignore`, and any existing `project.yaml`. The tree is clean
   when no tracked file is modified or staged; untracked files do not block.
   If it is not clean or another session appears to be working in the repo,
   stop and report before writing anything.
4. Decide ownership from the namespace of `origin`: the user's own repo, a
   shared repo the user leads, or a repo someone else owns (see "Repos shared
   with other people" in the conventions). When it is not evident, ask.
5. Add whichever of the four standard files are missing, from
   `${CLAUDE_PLUGIN_ROOT}/template`. Never overwrite an existing README or
   agent file. A `CLAUDE.md` whose only content is `@AGENTS.md`, blank lines
   aside, already conforms. If a long `CLAUDE.md` exists with no `AGENTS.md`,
   propose moving its content into `AGENTS.md` and ask before doing it.
6. Fill `project.yaml` from what the repo shows: `project` from the repo
   name (of `origin` when there is one, else the folder name); `title` from
   the README's first heading, left out when there is none or it only
   repeats the slug; `scope` from a scope the profile marks as a prefix when
   the folder name starts with it, else the one scope whose host and
   namespace match `origin`. When several scopes match, none does, or there
   is no `origin`, leave `scope` empty and ask, offering any matches.
   `summary` drafted from the README and confirmed with the user (if the
   user cannot confirm, write the draft and list it as unconfirmed). Leave
   unknown fields empty. If `project.yaml` already exists, fill only its
   empty fields and propose changes to filled ones.
7. If the profile's worktrees folder is not ignored, add the ignore line:
   in `.gitignore` in the user's own repo, in the local exclude file in a
   shared repo. In a repo someone else owns, also list the added standard
   files in the local exclude file.
8. Report what is still missing against the standard, such as no remote, a
   name that does not match the naming rule, a repo not directly under the
   profile's projects root, or committed credentials. Say which files were
   added and what happens to them: in the user's own repo they are left
   uncommitted; in a shared repo the user leads they are left uncommitted and
   go in through the repo's review, with only the fields true for everyone;
   in a repo someone else owns they are excluded and never committed.

## Notes

- Change nothing beyond adding files and ignore lines unless the user agrees.
- Added files follow the repo's own line-ending and formatting rules.
- Never move or rename the repository.
- In a shared repo, ignore lines go in the local exclude file, never in
  `.gitignore`.
