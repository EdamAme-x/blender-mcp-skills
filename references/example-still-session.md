# Example Still Session

## Table of Contents
- Scenario
- Good user request
- Initial spec excerpt
- MCP execution loop
- Review log example
- Why this works

## Scenario

Create a premium still render of a compact desk lamp for a design-portfolio cover.

- Goal:
  - Make the lamp feel expensive, engineered, and calm.
- Output:
  - One hero still.
- Base recipe:
  - `Industrial hero still` from `style-recipes.md`.

## Good user request

```text
Use $blender-mcp-skills.
Create a premium hero still of a compact desk lamp for a portfolio cover.
I want brushed metal, soft black painted parts, and a warm bulb accent.
Keep the background simple and architectural, not a studio infinity wall.
Start by writing the still spec, collection plan, and review plan.
Then set up the scene in Blender MCP with EEVEE-first workflow.
Do not freestyle materials before the camera and hero frame are locked.
```

## Initial spec excerpt

```md
# Project
- Project Name: AST_LAMP_PORTFOLIO_STILL
- Goal: Create a premium hero image of a compact desk lamp that reads as engineered and tactile.
- Output: still
- Delivery Format: PNG
- Resolution: 2560x1440
- Aspect Ratio: 16:9
- Unit System: metric
- Scale Reference: lamp height 0.42m
- Style Sentence: Quiet premium industrial product shot with warm accent light and strong metal-vs-paint separation.
- Hero Frame: 100
- Definition of Done:
  - hero silhouette reads at thumbnail size
  - brushed metal, paint, and emissive bulb all separate clearly
  - background supports the lamp without competing

# Collection Plan
- COL_SRC_HERO: lamp body, hinges, bulb housing, base, cable anchor
- COL_SHOT_010: hero placement and any shot-local helper duplicates
- COL_LIGHT: key, fill, rim, bounce cards
- COL_CAM: CAM_SHOT_010
- COL_RENDER_HELPER: ground matte, reflection test card

# Still Shot Spec
## SHOT_010
- Frame: 100
- Purpose: portfolio hero frame
- Main Subject: desk lamp
- Composition: lamp occupies 60 percent of height, angled three-quarters toward camera, negative space on right for title safe area
- Camera Type: perspective
- Lens / Focal Length: 70mm
- Camera Height / Angle: slightly below bulb line, 8 degrees upward
- Focus Target: front edge of bulb housing
- f-stop: 4.0
- Lighting Plan: hard warm key from upper left, cool soft fill from right, thin rim on rear edge
- Materials To Build: brushed aluminum arm, satin black painted base, translucent warm bulb cover
- Collections Used: COL_SRC_HERO, COL_SHOT_010, COL_LIGHT, COL_CAM, COL_RENDER_HELPER
- Hero Reference: premium product photography with controlled hard key and restrained reflections
- Accept If:
  - silhouette is legible without zooming
  - bulb accent does not clip or flatten the metal
  - black paint remains readable against background
- Reject If:
  - lamp reads as toy scale
  - background edge contrast competes with hero
  - DOF hides hinge detail
```

## MCP execution loop

1. Write or update the still spec.
2. Create `COL_SRC_HERO`, `COL_SHOT_010`, `COL_LIGHT`, `COL_CAM`, `COL_RENDER_HELPER`.
3. Move every lamp object out of default `Collection`.
4. Build blockout and confirm overall scale.
5. Lock `CAM_SHOT_010` at `70mm` before material polish.
6. Render frame `100` in `EEVEE` at `50%`.
7. Adjust light hierarchy until silhouette and material classes separate.
8. Build materials only after the frame works in grayscale.
9. Re-render frame `100` plus one secondary frame if reflections shift too much with angle.
10. Only after pass, switch to `Cycles GPU` and final-check frame `100`.

## Review log example

```md
# Review Log
- 2026-03-13 01:20 - SHOT_010 - fail
  - Symptom: lamp base merges into background and the warm bulb bloom makes the head shape unreadable
  - Cause hypothesis: background value is too close to base paint; bulb emissive is acting as a fill light instead of an accent
  - Fix target: darken background midtones behind base, reduce bulb emissive contribution, strengthen rear rim only on the head contour
  - Next check frame: 100

- 2026-03-13 01:42 - SHOT_010 - fail
  - Symptom: metal arm still looks like gray plastic
  - Cause hypothesis: roughness range is too narrow and key light angle is too frontal
  - Fix target: widen brushed metal roughness breakup, rotate key 12 degrees to produce longer highlight travel
  - Next check frame: 100

- 2026-03-13 02:05 - SHOT_010 - pass
  - Symptom: none blocking
  - Cause hypothesis: n/a
  - Fix target: move to Cycles GPU final check with Simplify on and Light Paths 7
  - Next check frame: 100
```

## Why this works

- The request forbids freestyle lookdev before camera lock.
- The spec makes scale, lens, and material targets explicit.
- The review log separates symptom from fix target, so iteration stays disciplined.
- The hero frame is stable enough that Cycles is used only after the image already works.
