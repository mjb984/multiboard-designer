# Multiboard Designer: feasibility and getting the part files

_Researched 2026-10-17. Sources are linked at the bottom. Anything marked **(inferred)** is my judgement and was not checked against a source._

## Bottom line

- **Feasible as a personal tool, built in phases.** Placing parts, snapping them, collision checks, labeled mock-up shapes and a parts list are all well within reach with three.js and existing libraries. The hard parts are getting snapping accurate for every part type, remixing (boolean ops on meshes), and the slice → print-queue step.
- **Files:** they're hosted on **Thangs** (multibuild.io's Parts Library links out to `than.gs`). Download them by hand into a local library folder that the app reads. The Terms **forbid scraping and bulk download**, and the license **forbids redistributing the original files**, so the app shouldn't fetch them automatically or ship them in a public repo.

## 1. How to get the files

| Question | Answer | Source |
|---|---|---|
| Where are they? | The multibuild.io Parts Library (`multibuild.io/parts`). Parts and packs link to Thangs (`than.gs/m/...`, designer "MultiBuild"). multiboard.io now redirects to multibuild.io. | multibuild.io, /get-started, /parts |
| Free? | "All individual, functional MultiBuild parts are FREE to download (or will be after an early access period)." The Community Promise says core and advanced parts become free for personal use within 6 months of release. Packs, **Stack Prints**, generators, and cosmetic and branded parts can stay member-only. | multibuild.io, /community-promise |
| Format | The printing guidelines say files are **.STL** with print orientation already set. Thangs shows a generic Download button. | docs.multibuild.io printing guidelines |
| Bulk download / API | **No public API found.** Section 5 of the Terms prohibits trying to "Scrape, spider, crawl, bulk-download or otherwise attempt to extract data or content from the Site ... in an automated or systematic manner". | /terms-conditions |
| Can we redistribute? | No. "You may not share or redistribute copies or mass link repositories of the original Designs." Personal use, download and modification are allowed. | /license |
| Remixes | Allowed and shareable when the change is "more than minor edits", under the same license and with credit. Multiboard gets a broad license to your remixes. Commercial use needs the Commercial ("Multi Partner") subscription. | /license |
| Software/apps | The license summary doesn't address apps that load or render the models. **(inferred)** A private, personal tool that reads files you downloaded yourself fits "personal use". Bundling the files into a public or hosted app would be redistribution. | /license |

**Recommended workflow**
1. Make a free Thangs account. Download the parts you need from the Parts Library: tiles, snaps, pins/clips, bolts, and the hooks/brackets/shelves for the rack. Consider a membership if you want the Stack Print files and packs.
2. Put them in a local `library/` folder, e.g. `library/<category>/<part>.stl`. The app indexes that folder. Add `library/` to `.gitignore`; the repo holds only our metadata (snap points, part IDs), never the STLs.
3. To automate later, ask Multiboard for written permission first. The Terms carve out "express prior written permission".
4. Community remixes on Printables/MakerWorld each have their own license, so check each one. I didn't find an official mirror of the core library outside Thangs.

## 2. Feasibility by feature

| Feature | Difficulty | How |
|---|---|---|
| 3D workspace, import STL, move/rotate | Easy | three.js (or react-three-fiber) + STLLoader + TransformControls |
| Basic shapes as component mock-ups (mini PC, PSU, fans) with labels | Easy | Box/cylinder primitives sized in mm, text labels (CSS2D or troika-three-text) |
| Accurate grid snapping of tiles | Easy–medium | Multiboard uses **25 mm** spacing between multiholes and pegboard holes (from the part descriptions). Tile snap points can be generated procedurally from the grid. |
| Snapping accessories (snaps, hooks, brackets, pins) | **Hard (data, not code)** | STLs carry no connection info, so each part needs a small metadata file: its connector type (large thread, small thread, peg, snap) plus position and orientation. The snapping code is simple; writing metadata for every part is the real work. Start with the ~20 parts the rack needs. |
| Collision detection | Medium | `three-mesh-bvh` for fast mesh-vs-mesh intersection; flag overlaps in red. The 0.25 mm design tolerance has to be ignored or snapped-together parts will show false hits. |
| Parts list (incl. connectors, clips, bolts) | Easy | Every placed instance carries its part ID. Connectors are counted automatically from the joints that snapping creates. Export CSV. |
| Remixing (cut, extend, add holes, merge) | Medium–hard | `manifold-3d` (WASM) for reliable booleans on meshes. Parametric edits beyond booleans (e.g. "make this bracket 10 mm longer") need re-modelling, possibly in OpenSCAD/CadQuery. |
| Plate layout (arrange parts on the build plate) | Medium | 2D bin-packing of part footprints; export a .3mf with parts placed |
| Slicing | Hard in-browser, **medium via CLI** | Don't write a slicer. Run **OrcaSlicer / PrusaSlicer / Bambu Studio CLI** on a small local backend with saved printer profiles. |
| Queue to printer | Medium, printer-dependent | Klipper/Moonraker and OctoPrint have simple HTTP upload+print APIs. **(inferred)** Bambu printers are harder: third-party control goes through LAN mode and recent firmware has restricted it. Which printer do you use? |
| Stacked tile prints, 0.8 mm nozzle | **Medium–hard; needs test prints** | The official guide is written for a **0.4 mm nozzle, 0.2 mm layers, 0.25 mm tolerance**, with ironing stacks separated by a 0.2 mm gap. It says nothing about 0.8 mm. **(inferred)** Flat tiles should be fine at 0.8 mm, but threads and snaps will probably lose fit at that line width, so print connectors with 0.4 mm or calibrate with the test files. The app can generate stacks (N tiles + 0.2 mm gaps) and pick layer heights that divide evenly into the gap. |

## 3. Suggested phases

1. **MVP (the rack itself):** local library indexer, 3D workspace, tile grid snapping, hand-written snap metadata for the ~20 rack parts, labeled box mock-ups for the mini PC/PSU/fans, collision highlighting, CSV parts list. This alone lets you design the under-desk rack.
2. **Print prep:** plate layout + 3MF export, stack-print generator with a 0.8 mm profile, slicing through the OrcaSlicer CLI.
3. **Remix:** boolean cut/merge with manifold-3d; save remixes as new library parts.
4. **Print queue:** send to the printer (Moonraker/OctoPrint first, Bambu if needed) and track job status.

Suggested stack **(inferred)**: Vite + React + react-three-fiber in the browser, plus a small local Node or Python service for file indexing, slicer CLI calls and the printer API. Everything runs on your machine, which also keeps the licensed files local.

## Open questions for Mauricio
- Which printer(s) and firmware (Bambu, Prusa, Klipper)? That decides the queue step.
- Membership: free parts only, or will you buy one for Stack Prints/packs?
- Rack: hanging under the desk or standing, and which mini PCs (size and count)?

## Sources
- https://multibuild.io/ (multiboard.io redirects here)
- https://multibuild.io/get-started
- https://multibuild.io/parts
- https://multibuild.io/license
- https://multibuild.io/terms-conditions
- https://multibuild.io/community-promise
- https://multibuild.io/memberships
- https://docs.multibuild.io/beginner-section/printing-guidelines
- https://thangs.com/designer/MultiBuild/post/Refined%20Multiboard%20License-5240
- https://thangs.com/designer/MultiBuild/3d-model/12x12%20MU%20-%20Center%20Grid%20Interfitted%20-%20MultiBoard%20Octagon%20Plate-977693
