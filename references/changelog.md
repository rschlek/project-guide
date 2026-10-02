# Changelog

Changes to the rules in `conventions.md`, newest first.

## 2026-10-01

- Sync sends every update to a repo in one of the profile's `shared_namespaces` through review: it reads the repo from its remote default branch, builds the commit without touching the checkout, and pushes it only to a review branch, unless the user approves a direct change for named repos in that run. The profile gains the optional `shared_namespaces` key. The standard version stays 0.6.0 (version 0.6.2).
- Sync covers every repo whose `project.yaml` is committed, adding the base block and the conventions copy where either is missing; a repo whose `project.yaml` is local only gets a local, excluded copy and no commit; a repo without a committed `project.yaml` is left to adopt; a project whose `project.yaml` says `archived` and the standard's own repository are skipped. The standard version stays 0.6.0 (version 0.6.1).
- The base block and the conventions copy carry the standard version, the release in which the block or these rules last changed, instead of the plugin version, so a release that changes neither leaves every repo current. The sync skill updates the block and the copy across the projects root in one run (version 0.6.0).
- `visibility` gains a second value, `internal`: anyone inside the organization that hosts the repo can read it. An internal repo may name that organization, its teams, and its internal systems, but never holds other people's personal details, credentials, or data extracts; the public cleaning pass is unchanged. The user decides whether a remote is private, internal, or public, and a reference never points at a more private repo in that order (version 0.5.0).
- Every project now carries `docs/project-conventions.md`, a copy of these rules whose first line names the version it was copied from, and its `AGENTS.md` opens with a marked base block of the rules every session needs. Both are replaced whole when the standard updates and never edited locally; project-specific guidance goes below the block. In a repo someone else owns, the copy is excluded and a tracked `AGENTS.md` is left without the block (version 0.4.0).
- A project's remote is private unless the user decides it is public. A public repo carries `visibility: public` in `project.yaml`, and its first public push follows a cleaning pass: nothing identifying in files or history, a commit identity the user wants published, and a license (version 0.4.0).
- "Code shared between projects" names the one exception to never referencing a branch: a repo published as a plugin publishes on a `stable` branch that moves only by deliberate promotion from `main`, and a catalog may follow it (version 0.4.0).
- Scope says whose the project is and where it is hosted, not who uses it; the summary says who it serves (version 0.4.0).

## 2026-09-30

- Added "Repos shared with other people": in a shared repo the user leads, the standard files go in through review with only team-wide facts in `project.yaml`; in a repo someone else owns, they stay local in the exclude file. `project` now equals the repo name, so it holds for a repo adopted outside the projects root (version 0.3.0).
- Added "Code shared between projects": one copy and one owner, an ordered test for how one project references another's code, and two guard rails (version 0.2.0).
- Initial version.
