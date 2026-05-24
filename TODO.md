# Slice_AQPH TODO

## CI Results (Pass 1)

- [x] DRC: FAIL — 4 errors (3x starved_thermal spoke count on F.Cu, 1x unconnected_items) + 107 warnings (silk_edge_clearance)
- [x] ERC: FAIL (blocked by DRC errors in combined make target) — 8 ERC warnings (missing libs: SparkFun-LED, SparkFun-DiscreteSemi, kml-custom; missing Conn_01x10_Female; +12V mismatch)
- [x] Fab: FAIL (blocked by DRC errors)
- [ ] gen-kibot-index: SKIPPED (upstream failed)
- [ ] deploy-pages: SKIPPED (upstream failed)

## Pass 2 – Pre-fab Review

- [ ] Fix 3x starved thermal relief (F.Cu zone spoke count)
- [ ] Fix 1x unconnected items (missing connection)
- [ ] Address silk_edge_clearance warnings (107)
- [ ] Add missing custom KiCad libs (SparkFun-LED, SparkFun-DiscreteSemi, kml-custom)
- [ ] Verify BOM completeness
- [ ] Confirm board outline and mounting holes
- [ ] Update README.md (still says "Slice Template")
