# Codex Skills

Repository-style Codex plugin marketplace for local or GitHub-hosted Codex plugins.

## Plugins

- `build-android-apps`: Android emulator/device browser mirroring, UI automation, preview launchers, logcat/crash diagnosis, and proof bundles.

## Local Marketplace

Marketplace manifest:

```text
.agents/plugins/marketplace.json
```

Plugin layout:

```text
plugins/
  build-android-apps/
    .codex-plugin/plugin.json
    skills/
      android-emulator-browser/
        SKILL.md
        references/
        scripts/
```

To install this marketplace locally, add this repository root as a Codex plugin marketplace.
