# Working in this repo

- This repo is a plugin. Consumers install it from its remote on the `stable` ref. Work lands on `main`; promote `main` to `stable` deliberately, never as a side effect.
- Everything here is generic: no person, company, team, product, machine, or real URL. Say "the user", "the tracker", "the memory system", "the profile". Machine-specific values belong in a profile, not in this repo. The one exception is the `author` field in the plugin manifests.
- Skills follow the house skill conventions: generic voice, under 100 lines, bundled files referenced as `${CLAUDE_PLUGIN_ROOT}/...`.
- Any change to the rules in `references/conventions.md` gets a dated entry in `references/changelog.md`.
- Folders matching `*-instance/` are separate repositories and are ignored here.
