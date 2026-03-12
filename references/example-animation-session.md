# Example Animation Session

## Table of Contents
- Scenario
- Good user request
- Initial spec excerpt
- MCP execution loop
- Review log example
- Why this works

## Scenario

Create a 72-frame looping teaser of a floating perfume bottle rotating slowly inside a moody illuminated chamber.

- Goal:
  - Make the bottle feel luxurious and weightless.
- Output:
  - Short seamless loop.
- Base recipe:
  - `Looping motion teaser` plus parts of `Moody cinematic environment`.

## Good user request

```text
Use $blender-mcp-skills.
Build a 72-frame seamless loop of a floating perfume bottle inside a moody illuminated chamber.
The bottle is the hero. The chamber exists only to frame it.
I want premium cosmetic-ad lighting with one clear key light and restrained volumetric depth.
Start from the animation spec template, define review frames and short preview ranges, then set up collections in Blender MCP.
Keep work in EEVEE until the loop seam, motion, and hero hierarchy pass review.
```

## Initial spec excerpt

```md
# Project
- Project Name: AST_PERFUME_LOOP
- Goal: Create a seamless luxury loop centered on a floating perfume bottle with slow, elegant motion.
- Output: loop
- Delivery Format: MP4 and image sequence
- Resolution: 1920x1920
- Aspect Ratio: 1:1
- FPS: 24
- Global Frame Range: 1-72
- Unit System: metric
- Scale Reference: bottle height 0.16m
- Loop Requirement: yes
- Style Sentence: Premium cosmetic-ad loop with restrained motion, glossy glass, and controlled warm-cool contrast.
- Definition of Done:
  - loop seam is invisible
  - bottle remains dominant through all review frames
  - glass, liquid, cap, and label separate clearly

# Collection Plan
- COL_SRC_HERO: bottle glass, liquid, cap, label, floating rig controls
- COL_SRC_ENV: chamber walls, pedestal ring, background panels
- COL_SHOT_010: loop placement and shot-local helpers
- COL_LIGHT: key strip, fill bounce, rim kicker, volume helper
- COL_CAM: CAM_SHOT_010
- COL_FX: subtle volume cone and dust motes if needed

# Shot Timeline
## SHOT_010
- Frames: 1-72
- Purpose: seamless social teaser loop
- Main Subject: floating perfume bottle
- Composition: bottle centered slightly low, chamber arcs framing top and sides, clear negative space around silhouette
- Camera Type: perspective
- Lens / Focal Length: 55mm
- Camera Height / Angle: level with bottle logo, 3 degree downward tilt
- Focus Target: front label plane
- f-stop: 5.6
- Camera Motion: very slow 8 degree arc from left to right, matched to loop seam
- Subject Motion: bottle rotates 18 degrees over the loop with slight vertical drift returning to origin
- Lighting Plan: warm vertical key from rear-left, cool fill from front-right, narrow rim for cap edge
- Materials To Build: clear glass, tinted liquid, brushed cap metal, subtle printed label
- Collections Used: COL_SRC_HERO, COL_SRC_ENV, COL_SHOT_010, COL_LIGHT, COL_CAM, COL_FX
- Review Frames: 1, 18, 36, 54, 72
- Short Range Preview: 1-24, 25-48, 49-72
- Transition In: frame 72 must match frame 1 in pose, value structure, and camera framing
- Transition Out: same as transition in
- Accept If:
  - seam between 72 and 1 is not visible
  - bottle label remains readable at peak highlight
  - chamber never overtakes hero contrast
- Reject If:
  - loop depends on motion blur to hide seam
  - glass reflections strobe frame to frame
  - DOF causes label readability collapse at frame 36
```

## MCP execution loop

1. Write the animation spec with explicit seam rules.
2. Create hero, environment, light, camera, fx, and shot collections before animation polish.
3. Block out chamber and bottle with correct real-world scale.
4. Lock lens family and framing before polishing motion curves.
5. Define review frames `1, 18, 36, 54, 72` and preview ranges `1-24`, `25-48`, `49-72`.
6. In `EEVEE`, render frame `1` and `36` first to validate hierarchy.
7. Render range `1-24` at low resolution to check motion feel.
8. Render frames `72` and `1` side by side to validate seam.
9. Only after seam and hierarchy pass, refine glass and label materials.
10. Move to `Cycles GPU` for frame `1`, `36`, and a short seam range around `68-72` plus `1-4`.

## Review log example

```md
# Review Log
- 2026-03-13 03:10 - SHOT_010 - fail
  - Symptom: seam is visible because the chamber highlight band shifts between frame 72 and frame 1
  - Cause hypothesis: camera arc and bottle rotation return, but area light rotation does not
  - Fix target: drive chamber key light orientation from the same loop controller or freeze the light and move only the camera
  - Next check frame/range: frames 68-72 and 1-4

- 2026-03-13 03:32 - SHOT_010 - fail
  - Symptom: label becomes unreadable near frame 36 when front fill drops too low
  - Cause hypothesis: fill is physically elegant but too weak for ad readability
  - Fix target: raise localized fill on label plane, not global fill, and reduce cap highlight spill
  - Next check frame/range: frame 36 and range 25-48

- 2026-03-13 03:58 - SHOT_010 - pass
  - Symptom: none blocking
  - Cause hypothesis: n/a
  - Fix target: final representative Cycles GPU checks on frame 1, frame 36, and seam range
  - Next check frame/range: 1, 36, 68-72, 1-4
```

## Why this works

- The loop seam is treated as a first-class spec item, not an afterthought.
- Review ranges are defined before polishing, so render time stays bounded.
- Hierarchy is checked before expensive glass refinement.
- The environment is constrained to support the bottle instead of stealing attention.
