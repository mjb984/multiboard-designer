# Decisions

- **Single HTML file, no build step.** three.js 0.170 and three-mesh-bvh 0.8.3 load from jsDelivr via an import map. Easy to open locally and to publish as a hosted page. Revisit if the app outgrows one file.
- **Part files stay local.** The app reads STLs through a folder picker; nothing is uploaded or committed, because the Multiboard license forbids redistribution.
- **Snap data instead of auto-detection.** STLs carry no connection info. Each part gets a mount face and grid offset (default 12.5 mm from the part's edge), stored per file name and exportable as JSON.
- **Slicing stays in Bambu Studio for now.** The designer exports plain 3MF per plate; Bambu Studio handles profiles, slicing and sending to the H2C.
