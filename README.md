# Codex Skills

Personal Codex skills and plugins for reusable agent workflows.

This repository is a public, repo-scoped Codex plugin marketplace. It collects
installable Codex plugins and their bundled skills in one place, so the same
agent workflows can be reused across local projects.

## Catalog

| Type | Name | Path | Description |
| --- | --- | --- | --- |
| Marketplace | `codex-skills` | `.agents/plugins/marketplace.json` | Repo marketplace manifest that exposes plugins from this checkout. |
| Plugin | `build-android-apps` | `plugins/build-android-apps/` | Android app development plugin for device mirroring, automation, previews, and debugging. |
| Skill | `android-emulator-browser` | `plugins/build-android-apps/skills/android-emulator-browser/` | Bundled skill used by `build-android-apps` to mirror and control adb-connected Android devices from Codex. |

## Install

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add peterchoee/codex-skills
```

For local development from a checked-out copy:

```bash
codex plugin marketplace add /absolute/path/to/codex-skills
```

Then open `/plugins` in Codex, choose the `Codex Skills` marketplace, and
install the plugin you want.

## Repository Layout

```text
.
|-- .agents/
|   `-- plugins/
|       `-- marketplace.json
|-- plugins/
|   `-- build-android-apps/
|       |-- README.md
|       |-- .codex-plugin/
|       |   `-- plugin.json
|       `-- skills/
|           `-- android-emulator-browser/
|               |-- SKILL.md
|               |-- agents/
|               |-- references/
|               `-- scripts/
`-- README.md
```

## Plugin Details

Each plugin owns its own README. Start here for plugin-specific usage,
requirements, scripts, and skill behavior:

| Plugin | README |
| --- | --- |
| `build-android-apps` | `plugins/build-android-apps/README.md` |

## Maintenance

Each plugin lives under `plugins/<plugin-name>/` and includes a required
`.codex-plugin/plugin.json` manifest. Bundled skills live under that plugin's
`skills/` directory, with one `SKILL.md` per skill.

When adding a plugin:

1. Create `plugins/<plugin-name>/.codex-plugin/plugin.json`.
2. Add bundled skills under `plugins/<plugin-name>/skills/<skill-name>/`.
3. Add or update the plugin entry in `.agents/plugins/marketplace.json`.
4. Add `plugins/<plugin-name>/README.md` for plugin-specific documentation.
5. Restart Codex and verify the plugin appears in the `Codex Skills`
   marketplace.

When adding a skill to an existing plugin:

1. Create `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`.
2. Keep the frontmatter `name` and `description` clear enough for Codex to
   decide when to load it.
3. Put long workflow details in the skill folder and keep executable helpers in
   `scripts/` when they make the skill easier to maintain.
