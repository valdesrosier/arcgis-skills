# Experience Builder Versions

> **Re-verify every fact here against Esri's Experience Builder release-versions page before relying on it.** ExB shifts these across releases; this file is a cache, not the source of truth.

## ExB release ↔ JS SDK version

Experience Builder Developer Edition bundles a specific ArcGIS Maps SDK for JavaScript version, which must match the target ArcGIS Enterprise. Resolve the pairing from the release-versions page together with the shared version matrix — <https://developers.arcgis.com/javascript/latest/version-matrix/>.

## Node.js gate

- ExB 1.20+ requires Node 20 or higher.
- ExB 1.12+ supports Node 16, 18, 19, and 20 — but **not** Node 17.

Verify the exact Node range and the recommended pnpm version for the specific ExB version in use against the release-versions page.
