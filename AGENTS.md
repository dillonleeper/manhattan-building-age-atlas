# Agent instructions

Read `PROJECT.md` before making architectural or product decisions.

## Priorities

1. Keep the MVP narrow and working.
2. Prefer official NYC public data and preserve source identifiers.
3. Make all data transformations reproducible.
4. Treat map performance and payload size as first-class engineering constraints.
5. Do not add AI/LLM features to this project unless explicitly requested.
6. Do not invent values for missing construction year, height, geometry, neighborhood, or other attributes.
7. Document material assumptions and unit conversions.

## Development workflow

- Work in small, reviewable commits.
- Before introducing a dependency, explain why it is needed and prefer established libraries.
- Add tests or validation for nontrivial data transformations.
- Keep generated/raw data out of Git when it is large or reproducible.
- Never commit secrets, API tokens, local `.env` files, or machine-specific state.
- Update `PROJECT.md` when a product/architecture decision materially changes the plan.
- Update `README.md` when setup or user-facing behavior changes.

## First task

Start with the data spike described in `PROJECT.md` rather than scaffolding a large application blindly:

1. Inspect the official NYC Building Footprints source and documentation.
2. Determine how to isolate Manhattan reliably.
3. Verify construction-year and roof-height fields and units.
4. Measure nulls/outliers and note data-quality issues.
5. Produce a small browser-friendly sample artifact.
6. Recommend the frontend/rendering approach based on observed geometry volume and performance requirements.

Do not build the entire application in the first pass.
