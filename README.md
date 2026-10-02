# Project Guide

A small standard for how projects are laid out, named, hosted, and described, packaged as a plugin for agent harnesses.

- `references/conventions.md`: the rules.
- `references/profile.example.yaml`: the shape of the per-machine profile that holds the projects root, scopes, hosts, tracker, and memory system.
- `references/changelog.md`: changes to the rules.
- `template/`: the four files a new project starts from. The skills also give every project `docs/project-conventions.md`, a copy of the rules, and fill the base block at the top of its `AGENTS.md`. The version in the block's start marker is the standard version: the release in which the block or the rules last changed.
- `scripts/sync.py`: places, compares, and updates the base block and the conventions copy; the skills run it.
- `skills/new`: create a new project to the standard.
- `skills/adopt`: bring an existing repository up to the standard, in place.
- `skills/sync`: bring the base block and the conventions copy up to date in every adopted repo under the projects root, in one run.

## Profile

The skills find the machine's profile through the environment variable `PROJECT_GUIDE_PROFILE`, or else a one-line file `.project-guide` in the home folder containing the profile's path. Start from `references/profile.example.yaml`.
