---
name: arcgis-docs-lookup
description: Look up ArcGIS documentation against authoritative Esri sources and verify an API exists at a pinned version. Use when the user needs an ArcGIS API reference, ArcGIS Pro, Enterprise, or Notebook Server docs, or when another skill must confirm a class, method, global, or function is available at a target version.
---

# ArcGIS Docs Lookup

Answer every ArcGIS question from the first-party source that *owns* it — never a stale mirror, a wrong-product page, or an unverified forum post.

## Route to the owning source

- **developers.arcgis.com** — ArcGIS Maps SDK for JavaScript, ArcGIS API for Python, the REST API, and Arcade references.
- **pro.arcgis.com** — ArcGIS Pro, including ArcPy and geoprocessing.
- **enterprise.arcgis.com** — ArcGIS Enterprise, Portal, and Notebook Server administration and runtime docs.

**Never cite ArcMap, ArcCatalog, or ArcGIS Desktop documentation.** It describes a retired product whose APIs have diverged from Pro and Enterprise. If a search returns an ArcMap or ArcGIS Desktop page, discard it and find the Pro or Enterprise equivalent.

## Pin the version

Enterprise docs are version-scoped by URL path (e.g. `.../enterprise/11.2/...`). Pin every Enterprise URL to the target version you are working against — the release the caller named, or the one the user is on. An unversioned or mismatched Enterprise URL is not an acceptable citation.

## Treat Community as a hypothesis, not a source

Esri Community, GeoNet, and Stack Exchange threads are leads to verify, never the citation. Trace every claim back to the owning first-party doc before relying on it.

## Match the depth to the question

- **Quick existence or signature check** ("does this class/method/global exist at version N") — read the owning reference page directly and answer inline. No file written.
- **Genuine investigation** (a migration surface, a breaking-change sweep, synthesis across many pages) — escalate to the `research` skill if it is available, passing these routing and version rules so the background agent obeys them. If `research` is not installed, do the investigation inline against the same first-party sources.

## Done when

Every claim is backed by a first-party URL on the correct domain, pinned to the target version wherever the docs are version-scoped, and no ArcMap/Desktop page or unverified Community thread remains as a citation.
