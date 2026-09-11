# Project brief

## Working title

Manhattan Building Age 3D Atlas

## One-line product definition

A playful, explorable 3D map of Manhattan where every building is extruded by height and colored by construction year so users can visually explore how old or new the built environment is.

## Why this project exists

This is a portfolio project intended to demonstrate geospatial data engineering, spatial joins, public-data integration, 3D visualization, frontend performance, and analytical product design. It should feel fun enough that a user wants to explore it even without a specific research question.

## Product principles

1. **Visual first.** The map should communicate something before the user reads documentation.
2. **Truth over polish.** Missing, conflicting, or suspicious source values must be surfaced honestly.
3. **Fast first interaction.** A user should see Manhattan quickly rather than wait for a massive all-NYC payload.
4. **Progressive complexity.** Build a compelling narrow MVP before adding zoning, permits, landmarks, or historical layers.
5. **No fake precision.** Do not infer construction years, heights, or neighborhood membership without an explicit and documented method.
6. **Portfolio-quality engineering.** Prefer reproducible transformations, validation, tests, and clear architecture over one-off notebook logic.

## MVP scope

The first complete version should support:

- Manhattan-only building footprints.
- 3D extrusion using a trustworthy height field when available.
- Construction-year color scale from oldest to newest.
- A distinct neutral style for unknown/missing construction year.
- Pan, zoom, rotate, and pitch.
- Click/select a building and show:
  - construction year
  - roof height
  - BIN
  - BBL / MapPLUTO BBL when available
  - basic source metadata useful for debugging
- Construction-year range filter.
- Neighborhood filter.
- Age legend.
- Responsive desktop-first interface that remains usable on mobile.
- Reproducible data preparation script/pipeline.
- Basic tests or validation checks for transformed data.

## Explicitly out of MVP

Do not add these until the core atlas is stable:

- user accounts
- AI/LLM features
- property valuation models
- redevelopment prediction
- permit histories
- zoning analytics
- landmark overlays
- historical time slider
- all five boroughs
- complex backend services that are unnecessary for a static/read-heavy MVP

## Recommended technical direction

Codex should validate choices before implementation, but a sensible starting architecture is:

### Frontend

- TypeScript
- React-based frontend
- A WebGL mapping stack capable of performant polygon extrusion, such as MapLibre GL JS or deck.gl
- Minimal UI framework; avoid bloating the project before map performance is understood

### Data preparation

- Python for data acquisition/cleaning/geospatial transformation
- GeoPandas / Shapely where appropriate
- Output optimized for browser delivery rather than shipping raw citywide source files directly

### Data delivery

Prefer the simplest architecture that meets performance needs:

1. static preprocessed artifacts for the first MVP, or
2. vector tiles / PMTiles if raw GeoJSON becomes too large.

Do not introduce a database solely because one might be useful later.

## Data model concept

A normalized building record should preserve source identifiers and include fields similar to:

- `building_id`
- `bin`
- `bbl`
- `construction_year`
- `roof_height_ft`
- `ground_elevation_ft`
- `neighborhood`
- `geometry`
- `source_last_edited`
- `source_status`

Actual field names and units must be verified from source documentation before transformation.

## Data-quality rules

At minimum, validate:

- geometry validity
- Manhattan-only filtering
- null construction-year rate
- implausible construction years
- null/zero/negative roof heights
- duplicate source identifiers
- coordinate reference system
- unit conversions
- unexpectedly large or tiny geometries

Never silently coerce a bad value into a plausible value.

## UX concept

The map is the hero. UI should stay subordinate to it.

Suggested desktop structure:

- full map canvas
- compact left-side controls for search/filtering
- small persistent legend
- right-side or floating building detail panel after selection

Primary visual encoding:

- **height** = physical building height
- **color** = construction year / age

The color ramp should make old-vs-new immediately legible and remain distinguishable for common forms of color-vision deficiency. The original concept is red for older buildings through green for newer buildings, but accessibility and perceptual clarity should be evaluated before locking the final palette.

## Milestones

### Milestone 1 — Data spike

- confirm official source dataset(s)
- download/query Manhattan subset
- inspect schema and units
- quantify missing construction years/heights
- produce a small sample artifact

### Milestone 2 — First 3D Manhattan render

- scaffold frontend
- load a representative Manhattan subset
- render building polygons
- extrude by height
- add basic age coloring

### Milestone 3 — MVP interactions

- full Manhattan data strategy
- click/select building
- details panel
- legend
- year filter
- neighborhood filter

### Milestone 4 — Reliability/performance

- optimize payload/rendering
- add validation/tests
- loading/error states
- responsive behavior
- document architecture and reproducibility

### Milestone 5 — Portfolio polish

- refined visual design
- screenshots/demo
- clear README architecture section
- deployment
- document interesting findings from the data

## Future directions

Potential post-MVP work:

- historical/demolished building footprints
- construction timeline animation
- permit overlays
- landmark status
- zoning and FAR
- property valuation
- neighborhood-level age distributions
- block-level urban change summaries
- redevelopment-likelihood modeling

## Definition of done for v1

A user can open the deployed site, immediately recognize Manhattan in 3D, understand the age color encoding, inspect individual buildings, filter the view, and trust that the values shown came from documented public data. The project can be cloned and rebuilt from documented steps without private data or undocumented manual preprocessing.
