# Roadmap

## Phase 1: design bench (done 2026-10-21)
- [x] Load STLs from a local folder, grouped by category
- [x] 3D bench with 25 mm grid, face snapping, move/rotate with snap
- [x] Stand-in shapes with labels and presets (mini PC, fans, PSU, switch)
- [x] Collision detection (three-mesh-bvh)
- [x] Parts list with connectors counted separately, CSV export
- [x] Project save/open, autosave in the browser
- [x] Per-part snap data (mount face, grid offset), exportable JSON
- [ ] Verify grid offsets against real tile/snap STLs
- [x] Save/resume: autosave indicator, part files remembered in the browser (IndexedDB), New asks twice
- [x] Multi-select (Shift+click) with align Min/Center/Max per axis; Center on board (C); Alt+click centers while placing
- [x] Clip-hole detection and hole-to-hole snapping; clips needed estimated from lined-up holes
- [ ] Verify hole detection and the hole-size → clip mapping on real Multiboard parts

## Phase 2: print prep (in progress)
- [x] Plate packing for the H2C (305 × 320 mm), 3MF export per plate
- [x] Nozzle per part group (defaults: fine detail 0.4; tiles, panels, beams, bars 0.6; shelves, bins, baskets 0.8), one nozzle size per plate, nozzle column in the CSV
- [ ] Tile stack prints (ironing stack with 0.2 mm gaps, or PLA/PETG multi-material)
- [ ] Bambu-flavored 3MF (multi-plate project) so one file holds all plates

## Phase 3: remix
- [ ] Boolean cut/merge with manifold-3d, save remixes as new library parts

## Phase 4: print queue
- [ ] Slice via Bambu Studio / OrcaSlicer CLI
- [ ] Send to the H2C (Bambu Connect URL scheme, LAN Developer Mode, or Bambu Local Server)

## First project: under-desk mini PC rack
- [ ] Decide hanging vs. standing
- [ ] List the mini PCs (model, size, count), fans, power, switch
- [ ] Lay out the rack in the designer, check collisions and airflow gaps
