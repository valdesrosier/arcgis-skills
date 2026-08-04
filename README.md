# ArcGIS Skills

A set of [agent skills](https://github.com/mattpocock/skills) that give an AI coding assistant (GitHub Copilot, Claude, and other skill-aware agents) real, current expertise across the Esri / ArcGIS developer stack — client and authoring surfaces like **Experience Builder**, the **ArcGIS Maps SDK for JavaScript**, **Arcade**, and the **ArcGIS API for Python & Notebooks**; server-side **Custom Data Feeds** provider development; and authoritative **docs lookup**.

They are designed to **compose with [Matt Pocock's skills](https://github.com/mattpocock/skills)** — see [Recommended: pair with Matt Pocock's skills](#recommended-pair-with-matt-pococks-skills) — but every skill here works fully standalone with none of his installed.

## The skills

| Skill                        | What it does                                                                                                                                                                                                                                                     |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **arcgis-docs-lookup**       | Routes documentation questions to the authoritative Esri source (developers / pro / enterprise), never ArcMap or Desktop, version-scoping every Enterprise URL. Escalates to a `research` skill for deep investigations.                                         |
| **arcade**                   | Authors Arcade expressions for the correct **profile** (popup, labeling, field calculation, attribute rules) and verifies every global and function exists at the target Arcade version.                                                                         |
| **js-sdk**                   | Builds and migrates apps with the ArcGIS Maps SDK for JavaScript — resolves the target version, knows the 3.x / 4.x / 5.x generation boundaries, avoids the dead AMD path, and pins Calcite.                                                                     |
| **python-notebook**          | Writes ArcGIS API for Python for hosted ArcGIS Notebooks (Standard vs Advanced runtimes) or local installs, with a hard guard around destructive data operations.                                                                                                |
| **exb-widget**               | Builds Experience Builder Developer Edition custom widgets at the correct **compile version**, checks the Node/pnpm gate, and holds the manifest invariants.                                                                                                     |
| **arcgis-custom-data-feeds** | Builds ArcGIS Enterprise **Custom Data Feeds** — Node.js/Koop providers that expose an external system as a Feature Service — pinned to the target Enterprise version and its 12.0 generation boundary, with a guard around editable providers' upstream writes. |

`python-notebook`, `js-sdk`, and `arcgis-custom-data-feeds` each embed a destructive-operation guard: before any irreversible data call — a hosted-feature delete, or a Custom Data Feeds provider's upstream update/delete — the agent must name the target, show what it is, confirm it isn't production, and prefer a dry-run — so each skill stays self-contained.

## How they work — you don't invoke them

These are **model-invoked** skills. You don't type a command; you just describe your task in plain language and the agent recognizes it and applies the right skill:

```
You: "Help me write a popup Arcade expression that shows parcel area in acres."
        ↓  (matches the arcade skill's description)
Agent: reads arcade/SKILL.md → identifies the profile → pins the version → writes it.
```

Each skill's one-line description stays in the agent's context; when your intent matches, the agent loads that skill's full instructions and follows them. Being explicit about the technology ("an **Experience Builder** widget", "the **ArcGIS Python API**") makes the match near-certain.

## Installation

**Via the `skills` CLI** — installs into your project's `.agents/skills/`:

```bash
npx skills@latest add valdesrosier/arcgis-skills
```

**Or copy the folders** — copy the skill folder(s) you want from [`skills/`](skills/) into your project's `.agents/skills/` directory. Every skill is self-contained; `arcade` and `js-sdk` verify APIs through `arcgis-docs-lookup`, so include it if you want that step.

Either way, any skill-aware agent (GitHub Copilot, Claude, Codex) picks them up automatically whenever the workspace is open — no per-chat setup.

## Recommended: pair with Matt Pocock's skills

These were built to slot into [Matt Pocock's skill system](https://github.com/mattpocock/skills) and follow its conventions (front-loaded descriptions, one trigger per branch, checkable completion criteria, progressive disclosure). Two ways they benefit from his set:

- **During a grill.** Run his `/grill-with-docs` (or `/grilling` + `/domain-modeling`) to stress-test an ArcGIS design decision, and these skills fire automatically on-topic — bringing version discipline and API verification into the interview.
- **Deep research.** `arcgis-docs-lookup` hands heavy investigations to his `research` skill when it's installed, and falls back to inline research when it isn't.

Install his set with:

```bash
npx skills@latest add mattpocock/skills
```

Nothing here edits or depends on his files — the composition is additive.

## Design principles

- **No baked version facts.** Version relationships change (the Experience Builder build command and output path changed at 1.17). Skills encode the _procedure_ for discovering the current version and point at the live version anchor that owns their stack — the [Esri version matrix](https://developers.arcgis.com/javascript/latest/version-matrix/) for the JS-family skills, the [Enterprise SDK CDF guide](https://developers.arcgis.com/enterprise-sdk/guide/custom-data-feeds/) for Custom Data Feeds — rather than hardcoding a value that will silently go stale.
- **A safety guard for destructive data operations.** Before any irreversible data operation — a `truncate` / `delete` / `overwrite` / feature deletion against hosted data, or an editable Custom Data Feeds provider's upstream update/delete — the agent must name the target, show what it is, confirm it isn't production, and prefer a dry-run — pulled deterministically as an explicit step, never left to chance.
- **Never cite retired products.** Documentation lookups route to current sources and explicitly avoid ArcMap, ArcCatalog, and ArcGIS Desktop docs.

The architectural decisions behind these choices are recorded in [`docs/adr/`](docs/adr/), and project terminology in [`CONTEXT.md`](CONTEXT.md).

## Standalone or composed

Every skill is portable — drop a single folder into any skill-aware repo and it works with zero other skills present. Pairing with Matt Pocock's skills is a recommendation, not a requirement.

## Repository layout

Skills are published under a top-level [`skills/`](skills/) directory — the [skills.sh](https://skills.sh) source layout that `npx skills add` reads — and this is the only copy committed to the repo. For local development they're also mirrored under `.agents/skills/`, which is **git-ignored**: that folder additionally holds Matt Pocock's skills (installed as a dev dependency), and neither his skills nor the mirror are redistributed here. Regenerate the mirror by copying from `skills/`.

Each skill is self-contained: the destructive-operation guard is inlined into `js-sdk`, `python-notebook`, and `arcgis-custom-data-feeds` rather than shared, so nothing is lost when the CLI copies a single skill folder.

## License

Add your preferred license (e.g. MIT) as a `LICENSE` file before publishing.
