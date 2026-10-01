# Project conventions

The rules a project follows. Machine-specific values (the projects root, scopes, hosts, tracker, memory system) live in the profile, never here.

## Layout

- All projects live under one projects root, flat at the top level. Each entry is one repo, or a parent repo with nested child repos.
- A project gets a parent only when it needs two or more repos for a hard reason: a different host, a different visibility, or a separately deployable part. The parent ignores its children in `.gitignore`. Children are independent repos, not submodules.

## Files every project carries

Every project has these four files, even if some are blank:

- `README.md`: a human-readable summary, plus anything else a reader or agent needs.
- `AGENTS.md`: project-specific agent guidance only.
- `CLAUDE.md`: one line, `@AGENTS.md`.
- `project.yaml`: all structured facts about the project.

Written material goes in `docs/` by convention. Nothing else is prescribed. Credentials and data extracts are never committed.

There is no state file. Status lives in the tracker item (for tracked work), in the memory system (for the user's own sessions), and in git history.

## project.yaml

Required:
- `project`: the slug; equals the top-level folder name in the projects root.
- `summary`: one sentence, what it is and who it is for.

Optional:
- `title`: a human-readable name.
- `scope`: one of the profile's scopes, or `none`.
- `repo_role` and `repos`: multi-repo projects only. `repo_role` is `parent` or this repo's role; `repos` maps role to remote URL.
- `tracking`: map of tracker system to item reference.
- `memory`: tag, state model, instance, and bank, as applicable.
- `links`: sources, outputs, docs, people.
- `parked` or `archived`: a dated decision (`since`) with a `reason`. Present only when deliberately set.

The test for any field or file: if it can become false without anyone doing anything, it does not belong. Activity is read from git, never declared.

One-way pointers: a manifest never lists a repo on a more private host than its own. A private repo may point at a more public one, never the reverse.

Tracker mapping: a repo with a single outcome points at its smallest stable tracker item. A monorepo serving many outcomes points at the larger grouping item.

## Naming and hosting

- The folder name equals the repo name.
- New projects are named `<scope>-<subject>`, lowercase with hyphens. The scope comes from the profile's list; a scope marked as no prefix is left off.
- Existing shared repos are not renamed just to conform.
- Every project has a private remote from creation. The profile maps each scope to a host and namespace.

## Worktrees

- Worktrees nest inside the project, in the folder the profile names (default `.claude/worktrees/<purpose>`). One widely used harness only supports that location; git and other harnesses accept any path, so one location serves all of them.
- Keep worktrees out of version control: `.gitignore` in a repo the user owns, the local exclude file (`.git/info/exclude`) in a shared repo.
- One session per worktree.
- A worktree's branch is pushed, or the worktree is not left overnight.
- A worktree is removed when its branch merges.
- Never run a doubled-force clean (`git clean -ffd` or similar) in a main checkout; it deletes nested worktrees and child repos.

## The profile

One profile file per machine holds the values these rules refer to: `projects_root`, `worktrees_dir`, `scopes` (each with its meaning, whether it is a name prefix, and its remote host and namespace), `tracker` (kind and a URL pattern with `{key}`), and `memory` (kind and bank). See `profile.example.yaml`.
