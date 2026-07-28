# ArcGIS Skills

Terminology specific to this repo's ArcGIS skill set, layered on top of Matt Pocock's skill-authoring system. Skill-system terms (model-invoked, user-invoked, context pointer, leading word, etc.) are defined in that system's glossary and are not restated here.

## Language

**Shared version anchor**:
The live Esri version-matrix URL that maps an ArcGIS Enterprise release to its ArcGIS Maps SDK for JavaScript, Calcite, and Arcade versions. The single source of truth every version-needing skill points at rather than restating.
_Avoid_: version table, version map, version matrix (when referring to the canonical live source)

**Destructive operation guard**:
The policy each data-touching skill embeds and must satisfy before emitting code that irreversibly changes ArcGIS data — name the target, show what it is, confirm it is not production, prefer a dry-run, never emit blind. Scoped to data operations only, not credentials or org hygiene.
_Avoid_: safety check, confirmation prompt (when referring to this specific policy)
