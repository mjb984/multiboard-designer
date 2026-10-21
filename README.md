# Multiboard Designer

A browser tool for planning [Multiboard](https://multibuild.io) builds in 3D: load your own downloaded STL parts, snap them to the 25 mm grid, mock up real components (mini PCs, fans, power bricks), catch collisions, get a parts list, and pack parts onto print plates for a Bambu H2C.

First build: an under-desk mini PC rack with external cooling and cable management.

## Run it

- **Hosted:** the published copy is at https://claude.ai/artifact/5DhdSLEkPxCcdjUGa28dRy (private to the owner).
- **Locally:** open `index.html` in Chrome or Edge. It needs internet once to load three.js from jsDelivr. No build step.

Then click **Open parts folder** and choose the folder with your Multiboard STLs. Files are read in the browser and never uploaded.

## Using it

| Action | How |
|---|---|
| Place a part | Click it in the library, then click a board face (or the floor). R turns it 90°, Shift+click keeps placing, Esc cancels. |
| Move / rotate | Select it, then G or R (or the toolbar). Snap: 25 / 12.5 / 5 / 1 mm. |
| Mock component | + Box, + Cylinder, or a preset. Set size and label in the Selected panel. |
| Fix snapping for a part | Selected panel: Mount face (side touching the board) and Grid offset (edge to first hole). Remembered per file; Download snap data to keep it. |
| Collisions | Overlaps turn red and are listed. Parts snapped onto each other are ignored by default. |
| Parts list | Right panel. Download CSV or Copy. |
| Print | Print plates: pick a nozzle per part group, then parts are packed in their STL print orientation onto 305 × 320 mm plates, one nozzle size per plate. Download each plate as .3mf, open in Bambu Studio, slice, send. |

## Part files and license

Part files come from the multibuild.io Parts Library (hosted on Thangs). The license allows personal use and modification but **forbids redistributing the original files**, and the site terms forbid scraping and bulk download. So:

- Download parts by hand into a local `library/` folder (git-ignored).
- Never commit STL/3MF files to this repo.

Details: [docs/research-feasibility-and-downloads.md](docs/research-feasibility-and-downloads.md).

## Docs

- [docs/roadmap.md](docs/roadmap.md): phases and what is done
- [docs/printing-notes.md](docs/printing-notes.md): printer setup and print findings
- [docs/decisions.md](docs/decisions.md): why things are built the way they are
