# Data sources

## Primary source: NYC Building Footprints

Official NYC Open Data building-footprint data is the starting point for the MVP.

Dataset page:
https://data.cityofnewyork.us/d/3g6p-4u5s

The dataset exposes building footprint geometry and fields including identifiers, construction year, ground elevation, roof height, status, and MapPLUTO BBL. The source is updated regularly by NYC.

Important: field names, units, and semantics must be verified against the current source documentation before transformation. Do not assume every numeric-looking field is already in the units expected by the UI.

## Useful related source: Building Footprints Historic

Official NYC historical building-footprint data can support later demolition/history features.

Dataset page:
https://data.cityofnewyork.us/Housing-Development/Building-Footprints-Historical-Shape/s5zg-yzea

This is explicitly post-MVP unless needed to resolve a source-quality question.

## Potential enrichment sources after MVP

Only add these after the basic atlas is performant and trustworthy:

- MapPLUTO / PLUTO for land-use and lot/property attributes
- NYC neighborhood boundaries for filtering and summary statistics
- landmark designation data
- DOB permit / construction data
- zoning data
- property assessment data

## Acquisition strategy

For the data spike, prefer querying/downloading only the Manhattan subset or preprocessing the citywide source locally into a Manhattan-only artifact.

Do not commit enormous raw exports to Git. Keep acquisition reproducible with scripts and record source URLs, retrieval date, filters, transformations, CRS, and units.

## Required source fields for MVP

Investigate and preserve, when available:

- geometry
- BIN
- BBL / MapPLUTO BBL
- construction year
- roof height
- ground elevation
- source status
- source last-edited date

## Questions the data spike must answer

1. How many current building footprints are in Manhattan?
2. What percentage have a usable construction year?
3. What percentage have a usable positive roof height?
4. Are construction year and roof height consistent enough for direct visualization?
5. What are the main outlier patterns?
6. What identifier is most reliable for future joins: BIN, BBL, or another source key?
7. How large is a Manhattan-only GeoJSON payload?
8. Is static GeoJSON acceptable, or should the project move directly to vector tiles / PMTiles?
9. What neighborhood-boundary source should be used for spatial filtering?

## Provenance rule

Every derived field used by the application should be traceable either to an official source field or to a documented transformation. Any inferred or imputed values must be explicitly labeled and should not be introduced in the MVP unless necessary.
