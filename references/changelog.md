# Changelog

Changes to the rules in `conventions.md`, newest first.

## 2026-09-30

- Added "Repos shared with other people": in a shared repo the user leads, the standard files go in through review with only team-wide facts in `project.yaml`; in a repo someone else owns, they stay local in the exclude file. `project` now equals the repo name, so it holds for a repo adopted outside the projects root (version 0.3.0).
- Added "Code shared between projects": one copy and one owner, an ordered test for how one project references another's code, and two guard rails (version 0.2.0).
- Initial version.
