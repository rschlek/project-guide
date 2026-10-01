# Project Guide

A small standard for how projects are laid out, named, hosted, and described, packaged as a plugin for agent harnesses.

- `references/conventions.md`: the rules.
- `references/profile.example.yaml`: the shape of the per-machine profile that holds the projects root, scopes, hosts, tracker, and memory system.
- `references/changelog.md`: changes to the rules.
- `template/`: the four files every project carries.
- `skills/new`: create a new project to the standard.
- `skills/adopt`: bring an existing repository up to the standard, in place.

## Profile

The skills find the machine's profile through the environment variable `PROJECT_GUIDE_PROFILE`, or else a one-line file `.project-guide` in the home folder containing the profile's path. Start from `references/profile.example.yaml`.
