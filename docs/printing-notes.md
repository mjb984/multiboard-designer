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

## Nozzle strategy (researched 2026-10-21, not yet tested on our printer)

Goal: faster than 0.4 mm without holes that need cleanup.

| Part group | Nozzle | Why |
|---|---|---|
| Snaps, bolts, pins, clips, threads | 0.4 mm (high-flow if available) | Small parts that need a precise fit; they print fast anyway, so a bigger nozzle saves little. |
| Tiles / plates | **Test 0.6 mm** at 0.2-0.24 mm layers with X-Y hole compensation | Tiles take most of the print time. Holes come out undersized with bigger nozzles; hole compensation offsets them in the slicer instead of post-processing. |
| Big plain parts (shelves, bins, spacers, mock-up brackets) | 0.8 mm | No precise holes, so speed wins. |

What the sources say:
- **One nozzle size per print.** Mixing 0.4 and 0.8 mm in a single H2C print is not supported in Bambu Studio; one forum user got it working with a hand-built file and the printer warned about the mismatch. Two tool changes per layer would also eat the time saved. So: separate plates per nozzle size. (forum.bambulab.com/t/259143)
- **0.6 vs 0.4 on Bambu:** forum testers saw only ~10% speed gain at the same 0.2 mm layer height, because the 0.4 nozzle is already near the hotend's melt limit. The real gain from a bigger nozzle comes from taller layers. (forum.bambulab.com/t/2164)
- **High-flow hotend:** Bambu's high-flow hotends claim up to 62.5% more volumetric flow and up to 30% shorter prints. A retailer lists a 0.4 mm high-flow hotend for the H2C. This may be the best way to speed up fit-critical parts without losing detail.
- **X-Y hole compensation** (Bambu Studio > Process > Quality) grows every closed hole by the set amount; Bambu's example: hole 0.5 mm too small, set +0.25 mm. (wiki.bambulab.com/en/software/bambu-studio/xy-hole-contour-compensation)
- **Stack printing** (several tiles in one tall print, 0.2 mm gaps + ironing) cuts operator time more than nozzle size does: one overnight print instead of one plate per tile.

### Test plan
1. Print a 2x2 tile three ways: 0.4 / 0.2 layer (baseline), 0.6 / 0.24 layer with hole compensation +0.1 mm, 0.8 / 0.3 layer with hole compensation +0.2 mm.
2. Print one bolt and one snap at 0.4 mm.
3. Record print time and fit (bolt threads in by hand? snap clicks?) for each tile in the table below, then adjust compensation by 0.05 mm steps.

| Tile | Nozzle / layer | Hole comp. | Time | Bolt fit | Snap fit | Notes |
|---|---|---|---|---|---|---|
| 2x2 | 0.4 / 0.20 | 0 | | | | baseline |
| 2x2 | 0.6 / 0.24 | +0.10 | | | | |
| 2x2 | 0.8 / 0.30 | +0.20 | | | | |
