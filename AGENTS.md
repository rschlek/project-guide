# Working in this repo

- This repo is a plugin. Consumers install it from its remote on the `stable` ref. Work lands on `main`; promote `main` to `stable` deliberately, never as a side effect.
- Everything here is generic: no person, company, team, product, machine, or real URL. Say "the user", "the tracker", "the memory system", "the profile". Machine-specific values belong in a profile, not in this repo. The exceptions are the `author` field in the plugin manifests and this repository's own public URL (https://github.com/rschlek/project-guide), which the template and skills write into every project.
- Skills follow the house skill conventions: generic voice, under 100 lines, bundled files referenced as `${CLAUDE_PLUGIN_ROOT}/...`.
- This repository is the source of the standard, so it carries no `docs/project-conventions.md` copy of its own.
- Any change to the rules in `references/conventions.md` gets a dated entry in `references/changelog.md`.
- The version in the base block's start marker in `template/AGENTS.md` is the standard version, and the skills and `scripts/sync.py` read it from there. In a release, set it (in the marker and in the sentence below it) to the release version only when that release changes the base block text or `references/conventions.md`; otherwise leave it, so adopted repos need no update.
- Folders matching `*-instance/` are separate repositories and are ignored here.
