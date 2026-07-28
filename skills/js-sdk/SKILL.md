---
name: js-sdk
description: Build and migrate apps with the ArcGIS Maps SDK for JavaScript at the target ArcGIS Online or Enterprise version. Use when the user works with @arcgis/core, map components, MapView or SceneView, or migrates between 3.x, 4.x, or 5.x.
---

# ArcGIS Maps SDK for JavaScript

## Resolve the target first

Determine whether the app targets **ArcGIS Online** or a **specific ArcGIS Enterprise version**, then resolve the SDK version from the live Esri version matrix — <https://developers.arcgis.com/javascript/latest/version-matrix/> — rather than assuming "latest." The Enterprise release pins the SDK version, which in turn pins Calcite.

## Know the generation boundaries

These are not ordinary version steps — treat them as distinct products where noted:

- **3.x** — retired 2024-07-01. Not a migration target.
- **4.x** — a complete rewrite of 3.x, not an increment. Moving 3.x → 4.x is a rewrite.
- **5.x** — continues 4.x under semantic versioning: minor bumps are backward-compatible, major bumps are breaking.
- Migrating **3.x → 5.x is a rewrite, not an upgrade**.

## Use ES modules or components — the AMD path is dead

4.31 was the last release of the `arcgis-js-api` AMD npm package; its AMD TypeScript declarations and `@arcgis/cli` are retired. Build with `@arcgis/core` ES modules or the components packages. Do not scaffold AMD.

## Prefer components over widgets

Components are the recommended path. If you use widgets, **or** initialize `MapView`/`SceneView` programmatically, you must manually include the core API CSS stylesheet — omitting it renders the view broken.

## Pin Calcite

Pin Calcite to the version the target SDK uses (from the version matrix above), or a greater compatible minor.

## Verify before you propose API

Before proposing any class, method, or property, confirm through `arcgis-docs-lookup` that it exists at the pinned version. When moving between versions, read the breaking-changes guide rather than assuming a method still exists.

## Guard destructive edits

Before emitting any code that deletes or overwrites data — `FeatureLayer.applyEdits` with deletes, `deleteFeatures`, or an editor widget wired to a live layer — stop and satisfy every point in order. This covers irreversible data operations only, not credentials or org hygiene.

1. **Name the target.** State the org/portal and the exact item or layer id the operation hits. An unnamed target is a stop.
2. **Show what it is.** Display the layer's title, type, and feature count so the user sees what they are about to lose.
3. **Confirm it is not production.** Say so explicitly and get the user's confirmation before proceeding.
4. **Prefer the reversible form first.** Offer a read-only query or a count so the blast radius is known before the destructive call runs.
5. **Never emit blind.** Withhold the destructive call until 1–4 are satisfied and the user confirms — even when the user sounds certain.

Enforcement shape for this SDK: check whether the layer URL is hardcoded or config-driven and whether it currently points at production, and place the confirmation in the app flow before the write runs.

## Done when

The target and SDK version are resolved from the matrix; no AMD scaffolding remains; components (or CSS-included widgets) are chosen deliberately; Calcite is pinned to a compatible version; every proposed API is verified at the pinned version; and any destructive edit has passed through the guard.
