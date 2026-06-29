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
| Skill / slash entry | `android-emulator-browser` | `plugins/build-android-apps/skills/android-emulator-browser/` | Bundled skill that appears in the Codex slash command list and mirrors adb-connected Android devices from Codex. |

## Install

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add peterchoee/codex-skills
```

Then install the plugin you want from that marketplace:

```bash
codex plugin add build-android-apps@codex-skills
```

Verify that the plugin is installed and enabled:

```bash
codex plugin list | rg -C 2 'build-android-apps@codex-skills'
```

The status should show `installed, enabled`.

For local development from a checked-out copy, add the local repository as the
marketplace root instead:

```bash
codex plugin marketplace add /absolute/path/to/codex-skills
codex plugin add build-android-apps@codex-skills
```

After installation, restart Codex or open a new session so the bundled skill is
loaded.

In the Codex app, type `/` and choose `Android Emulator Browser` from the
slash command list. Codex includes enabled skills in that list. You can also
invoke the skill directly in the composer:

```text
$android-emulator-browser
```

In debug output or generated skill lists, plugin-installed skills may appear
with their plugin namespace:

```text
build-android-apps:android-emulator-browser
```

To update an existing install from GitHub:

```bash
codex plugin marketplace upgrade codex-skills
codex plugin remove build-android-apps@codex-skills
codex plugin add build-android-apps@codex-skills
```

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
`skills/` directory, with one `SKILL.md` per skill. Skill UI metadata for the
Codex app lives in `skills/<skill-name>/agents/openai.yaml`.

When adding a plugin:

1. Create `plugins/<plugin-name>/.codex-plugin/plugin.json`.
2. Add bundled skills under `plugins/<plugin-name>/skills/<skill-name>/`.
3. Add `agents/openai.yaml` inside each skill that should have a friendly
   Codex app slash-list label and default prompt.
4. Add or update the plugin entry in `.agents/plugins/marketplace.json`.
5. Add `plugins/<plugin-name>/README.md` for plugin-specific documentation.
6. Restart Codex and verify the plugin appears in the `Codex Skills`
   marketplace.

When adding a skill to an existing plugin:

1. Create `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`.
2. Keep the frontmatter `name` and `description` clear enough for Codex to
   decide when to load it.
3. Put long workflow details in the skill folder and keep executable helpers in
   `scripts/` when they make the skill easier to maintain.
