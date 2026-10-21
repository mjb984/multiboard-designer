# Decisions

- **Single HTML file, no build step.** three.js 0.170 and three-mesh-bvh 0.8.3 load from jsDelivr via an import map. Easy to open locally and to publish as a hosted page. Revisit if the app outgrows one file.
- **Part files stay local.** The app reads STLs through a folder picker; nothing is uploaded or committed, because the Multiboard license forbids redistribution.
- **Snap data instead of auto-detection.** STLs carry no connection info. Each part gets a mount face and grid offset (default 12.5 mm from the part's edge), stored per file name and exportable as JSON.
- **Slicing stays in Bambu Studio for now.** The designer exports plain 3MF per plate; Bambu Studio handles profiles, slicing and sending to the H2C.
- **Clip holes are found from the mesh.** The app slices a part 1.2 mm inside a face, keeps closed loops that run opposite to the outline (voids), are roughly round and at least 3 mm across, and treats them as clip holes. Placing a part shifts it up to ~19 mm so the most holes line up (same size within 25%, centers within 0.6 mm). Each lined-up hole counts as one clip; the clip type per hole size is the user's choice (defaults: 12 mm and up → Multipoint snap, smaller → pegboard pin). Thresholds are tested on stand-in geometry only and may need tuning for real threaded holes.
- **Part files are cached in the browser's IndexedDB** so layouts reopen with their parts. It stays on the user's computer, consistent with the license; "Forget remembered parts" clears it.
