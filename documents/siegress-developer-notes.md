# Siegress — Developer Notes

## Technologies used

- HTML5, CSS, and vanilla JavaScript with ES modules.
- Three.js and WebGL for 3D rendering, with custom shader effects.
- Canvas 2D for reading map colors and editing map.png.
- Web Audio API for footsteps; HTML audio for music.
- GLB/glTF models and Three.js animation mixers.
- Vite, Node.js, and npm for local development and builds.
- OpenAI Sites Vite plugin for build integration.
- Blender/Python tree-generation utility included in the repository.

## Early September 2025 — Drury Village begins

- Generated hills, trees, and buildings from a hand-editable map image.
- Created in-game interpreter that converted map colors to rendered in-game features.
- Had boundary walls along the edges of the map.
- Added gravity and jumping.
- The monster already had walking, running, and attack animations.
- Generated its GLB model from a 2D drawing using Meshy.ai.
- Rigged and animated it with either Meshy.ai or Adobe’s Mixamo; I do not recall which service.
- Began at the beginning of September 2025; this phase is based on my recollection.

## January 6–7, 2026 — MegaFuture232 baseline

- Imported the existing map-driven world demo.
- Smoothed terrain heights.
- Changed generic Christmas trees into a typical fractal tree shape.
- Commits: `8842e28` → `2919c2a`.

## January 12, 2026 — camera controls

- Added camera controls and first/third-person toggling.

## January 23–24, 2026 — tooling and startup

- Built material-preview tools with FBX/GLB support and custom toon/specular shaders.
- Added a loading screen; integrated it into the main page.
- Fixed `.png` versus `.PNG` asset references.
- Removed mousewheel camera zoom during startup changes.
- Commits: `a79e583` → `c54986e`.

## January 24–25, 2026 — weekend game jam

- Participated in a weekend-long game jam during the January 2026 snowstorm.
- The January 24–26 work below was part of that game-jam effort.
- Added story content.
- Commits: `a9cad59` → `43aa005`.

## January 25, 2026 — loading and simulation state

- Integrated startup flow before entering the game.
- Preloaded images while the world loaded.
- Loaded the entire world over a tethered cellphone connection during the snowstorm.
- Waited for prewarming before signaling readiness; intended to support slow networks.
- Added death/respawn state, saved spawn
- Tagged collision support types so branches could trigger a separate hazard.
- Commits: `b535727` → `fade44e`.

## January 26, 2026 — audio and cleanup

- Preloaded audio bytes; initialized Web Audio later in the start flow.
- Recorded myself crunching through the snow and used those recordings for the footsteps.
- Added walking footsteps with cadence, sample variation, and pitch variation.
- Added looping music on the initial user gesture.
- Fixed a preload path to use cached image URLs.
- Removed a duplicate footstep helper.
- Large formatting commit mostly reorganized existing code.
- Commits: `07f0d58` → `3a8b798`.

## Between January and September — SuperFutureTheLostUtopia

- Refined rounded hills and more convincing mountains.
- Added day/night lighting with moving shadows and highlights.
- Expanded animated 3D asset use; GLB support already existed in January.
- Studied and developed more convincing procedural Douglas firs.
- Carried this implementation into Siegress.
- Based on my recollection; exact dates and commits are unavailable.

## September 8–9, 2026 — Siegress import and map geometry

- Imported the accumulated game: 5,776 lines in the main HTML file.
- Already included procedural firs, instancing, terrain, collision, camera, loading, and audio.
- Replaced fixed site walls with geometry fitted from map pixels.
- Used seeded randomized line fitting, inlier scoring, and fallback geometry.
- Derived exclusion zones and spawn regions from map data.
- Revised wall tracing to handle disconnected paths.
- Commits: `6294aa6` → `832d1ed`.

## September 13–14, 2026 — wall, camera, and terrain corrections

- Resampled seawalls at roughly 20 world-unit spacing.
- Added segment overlap, deeper embedding, and a larger collision buffer.
- Replaced camera lifting with an eight-step search along the camera boom.
- Earlier camera correction changed the intended look-up angle.
- Added custom terrain shading with screen-space dithering.
- Changed the map to clean up geometry and address island visibility, according to the commit message.
- Commits: `e75f375` → `becb707`.

## September 14–15, 2026 — incremental modularization

- Used GPT Work Mode (an agentic workflow) to suggest how to make the code more atomic.
- Kept a checklist of planned modules in the code and checked them off one at a time.
- The checklist let me pick up where I left off when GPT Work Mode reached its compute limits.
- Extracted 15 systems one at a time.
- Split audio, preloading, developer console, startup UI, and materials into modules.
- Split terrain, water, trees, site walls, and seawalls into modules.
- Split collision, camera, and animated asset systems into modules.
- Passed dependencies and changing state through factory options and getters.
- Reduced terrain processing passes and loaded the hosting plugin only for builds.
- Moved large asset loading off the initial readiness path.
- Loaded animation assets concurrently and disposed superseded objects.
- Main HTML still owned movement, hazards, world assembly, and the loop.
- Commits: `b8ae3b9` → `3f1dcf8`.

## September 16, 2026 — fallbacks and interacting runtime states

- Showed a bounding rectangular prism when the monster or player GLB models were unavailable.
- Added a timed meter, threshold-based slowdown, and a timed reset interaction.
- Coordinated UI, camera mode, movement restrictions, and respawn resets.
- Added pursuit with different acquisition/loss radii and short tracking memory.
- Used camera projection and terrain raycasts to check visibility before repositioning.
- Pursuit used direct targeting and local collision handling; no pathfinding system.
- Commits: `242d9a6` → `d6bfe4a`.

## September 23–24, 2026 — rendering and reusable geometry

- Added modular ambient effects and billboard rendering.
- Disambiguated overlapping map-marker colors during wall extraction.
- Replaced animated canvas title rendering with a static image.
- Reused tree geometry and boundary behavior for the giant tower on top of one of the mountains.
- Added the tower’s collision shape and pulsing light effect.
- Revised spawn-marker semantics.
- Commits: `f8560c2` → `1bb61fd`.

## September 25, 2026 — traversal, editing, and support geometry

- Estimated terrain gradient using central differences.
- Applied a 0.25 movement multiplier above a 45-degree slope threshold.
- Shared traversal rules across moving entities.
- Added a speedometer based on actual displacement.
- Added real-time road making in the world, with undo, to update map.png.
- Laid out roads by feeling out what the hills, valleys, and slopes allowed, avoiding labor-intensive guess-and-check edits to map.png.
- Made sloped wall rendering agree with interpolated collision-top heights.
- Used previous position to handle landing, jumping off, and leaving wall edges.
- Fixed a wall-edge collision response that shoved the player away.
- Made the camera follow jumping and elevated support.
- Added terrain-conforming mound geometry and fatal-fall tracking.
- Commits: `40ceaf5` → `3e2edbc`.

## September 26, 2026 — explicit support colliders and layered map data

- Replaced the mound’s terrain-height override with separate structure geometry and a roof collider.
- Preserved elevated spawn height during respawn.
- Encoded eight jetty levels with map colors.
- Instanced blocks by level; combined consecutive pixels into platform colliders.
- Restored underlying world data from a baseline image where markers overwrote terrain/water.
- Reconstructed terrain under markers with inverse-distance weighting.
- Reduced sprint from 80 to 9 m/s; raised fatal-fall threshold from 8.5 to 10.2 units.
- Commit: `c332147`.

## What I would revisit

- Separate terrain, water, and object metadata into distinct layers.
- Extract movement, hazards, and world orchestration from the main HTML.
- Add repeatable checks for wall edges, jumping, landing, and elevated respawns.
- Measure loading and frame costs before claiming performance improvements.
- Make loading failures and save failures visible and recoverable.

## Evidence

- 55 inspected commits: 26 in MegaFuture232; 29 in Siegress.
- January and September dates are verified Git author dates in New York time.
- Imported baselines establish existing features, not their original creation dates.
- Earlier and intervening phases are recollections; no missing rationale is invented.
- Source review completed October 3, 2026; no runtime performance measurements.
- Repositories: [MegaFuture232](https://github.com/mcdowellj87/MegaFuture232) · [Siegress](https://github.com/mcdowellj87/Siegress).
