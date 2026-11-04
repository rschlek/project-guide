# Project Guide

A small standard for how projects are laid out, named, hosted, and described, packaged as a plugin for agent harnesses.

- `references/conventions.md`: the rules.
- `references/profile.example.yaml`: the shape of the profile, one per user on each machine, that holds the projects root, the worktrees folder, scopes and their hosts, the default tracker, and where each memory kind (`personal`, `shared`, `repo`) lives.
- `references/changelog.md`: changes to the rules.
- `template/`: the files a new project starts from. Its `project.yaml` carries the required `project` and `summary`, and optional `title`, `owner` (required for a live project), `scope`, `tracking` (a primary tracker and optional secondaries), `memory` (tag and kind, never a location), `links` (`related`, `depends_on` with project, repo, artifact, and version, and `agents`), `visibility`, `shared`, `parent`, and `paused` or `archived`. The skills also give every project `docs/project-conventions.md`, a copy of the rules, and fill the base block at the top of its `AGENTS.md`. The version in the block's start marker is the standard version: the release in which the block or the rules last changed.
- `scripts/sync.py`: places, compares, and updates the base block and the conventions copy; the skills run it.
- `skills/profile`: create, show, or change the profile; the other skills run it when no profile exists.
- `skills/new`: create a new project to the standard.
- `skills/adopt`: bring an existing repository up to the standard, in place.
- `skills/sync`: bring the base block and the conventions copy up to date in every adopted repo under the projects root, in one run.
- `agents/standards.md`: the agent that runs the heavy phases of the new, adopt, and sync skills, and restructures such as splitting a repo, across many repositories; it proposes every push, remote, and deletion.

## Profile

The skills find the user's profile on this machine through the environment variable `PROJECT_GUIDE_PROFILE`, or else a one-line file `.project-guide` in the home folder containing the profile's path. The profile skill creates it from a few questions; or start from `references/profile.example.yaml`.
