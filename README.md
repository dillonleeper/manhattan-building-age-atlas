# Manhattan Building Age 3D Atlas

An interactive 3D visualization of Manhattan buildings by age, height, neighborhood, and property characteristics.

## Product idea

Explore Manhattan as a living architectural timeline. Buildings are extruded in 3D and conditionally colored by construction year, making it easy to see where the city is oldest, newest, tallest, and most transformed.

The first version stays deliberately narrow: **show Manhattan building footprints in 3D, color them by construction year, and let users inspect and filter them.**

## MVP

- Render Manhattan building footprints in 3D.
- Extrude buildings using roof height where available.
- Color buildings on an old-to-new age scale.
- Click a building to inspect core attributes.
- Filter by construction year and neighborhood.
- Include a clear legend for building age.
- Handle missing or implausible construction years explicitly instead of silently fabricating values.

## Initial data

The primary source is NYC Open Data's current **Building Footprints** dataset. It includes polygon geometry plus fields such as BIN, BBL, construction year, ground elevation, and roof height.

See [`docs/DATA_SOURCES.md`](docs/DATA_SOURCES.md) for the source plan and data-quality notes.

## Planned evolution

After the MVP works well, likely extensions include:

1. Building class, stories, zoning, landmark status, and property characteristics.
2. Neighborhood and construction-era summaries.
3. Historical building footprints and demolition history.
4. A time slider showing how Manhattan changed.
5. Permit and redevelopment layers.
6. Urban-change analytics rather than only visualization.

## Development

The project is being developed with Codex. [`PROJECT.md`](PROJECT.md) is the source of truth for scope, architecture, sequencing, and product decisions. [`AGENTS.md`](AGENTS.md) contains repository-level instructions for coding agents.

## License

MIT
