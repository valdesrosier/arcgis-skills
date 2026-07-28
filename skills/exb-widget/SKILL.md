---
name: exb-widget
description: Build ArcGIS Experience Builder Developer Edition custom widgets at the correct compile version. Use when the user develops, builds, or registers an ExB custom widget, edits its manifest.json, or targets specific ArcGIS Enterprise versions with a widget.
---

# Experience Builder Custom Widget

Developer Edition custom widget work. The **compile version** is the constraint everything else hangs on — fix it before writing any widget code.

## Establish the version floor first — before any code

1. Read `client/package.json` in the Dev Edition install for the actual ExB version in use. Never assume a version.
2. Ask which ArcGIS Enterprise version(s) must run this widget.
3. The **compile target is the lowest** of those Enterprise versions — ExB runs widgets compiled in *earlier* versions but not *newer* ones, and the version a widget was **compiled in** is what matters.
4. Pick the Dev Edition version that uses the **same JS SDK version** as that target Enterprise — see [VERSIONS.md](./VERSIONS.md), and re-verify against Esri's release-versions page.

The `exbVersion` field in `manifest.json` is declarative and **not enforced** — hand-editing it downward does not backport a widget. Only compiling in the lower version does.

## Check the Node and pnpm gate before running anything

ExB is gated on Node major version, and the gate differs by ExB release. Confirm the Node and recommended pnpm versions for the exact ExB version in use — see [VERSIONS.md](./VERSIONS.md) — before `install` or `start`. A wrong Node major fails the toolchain.

## Keep the manifest invariants

`manifest.json` requires `name`, `type`, `version`, `exbVersion`, and `translatedLocales`. `name` must exactly match the widget's folder name — a mismatch breaks the widget.

## Branch on the output target

The workflow forks by where the widget is going:

- **Dev loop** — `npm start`; watch the built output under `client/dist`.
- **Download build** — produces a distributable widget. The build command and its output path have changed across ExB releases, so read the current build script and output folder from `client/package.json` scripts rather than assuming.
- **Portal registration** — register the widget with the portal. This requires CORS enabled for the portal domain on the hosting server, and JSON may need registering as a MIME type.

## Done when

The compile version is fixed to the lowest target Enterprise's matching Dev Edition; Node and pnpm are verified for that ExB version; the manifest invariants hold with `name` equal to the folder name; and the steps match the chosen output target.
