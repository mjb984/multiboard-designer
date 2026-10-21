# Printing notes

## Printer
- Bambu Lab H2C (one printer). Plate: 305 × 320 mm with one nozzle, 300 × 320 mm with both.
- Hotends on hand: 0.2, 0.4, 0.6 and 0.8 mm for both nozzles (some need to be loaded into the rack).

## Official Multiboard guidance (docs.multibuild.io printing guidelines)
- 0.4 mm nozzle, 0.2 mm layers, 3 walls, 15% infill, no supports.
- Parts are designed with 0.25 mm tolerance; STLs come in print orientation.
- Tile stacks: 0.2 mm gap between tiles with ironing, or PLA tiles with PETG spacers on a multi-material printer.
- Matte PLA recommended. Tall parts (e.g. MultiBins > 100 mm) may need slight Z scaling for shrinkage.

## Findings
- **2026-10-21 (Mauricio):** printing with a 0.8 mm nozzle, the holes need post-processing (cleanup) before parts fit. Working assumption: keep threads, snaps and anything with holes on 0.4 mm (or test 0.6 mm), and use 0.8 mm only where hole fit does not matter. To test: a small tile at 0.6 mm to see if holes come out clean.
