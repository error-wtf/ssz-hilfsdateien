# Fetching ALMA Data via Astroquery.Alma

ALMA files can be massive (>100 GB). To protect local bandwidth, the download utility filters ALMA products to select only FITS or README documentation by default.

## ALMA Science Archive Reference

- Search methods: Object resolves, cone regions, TAP query SQL
- Product filters: fits (calibrated images / cubes), readme (QA documentation)
- Raw visibilities (.ms) are skipped by default.
