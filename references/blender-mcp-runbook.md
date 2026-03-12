# Blender MCP Runbook

## Table of Contents
- Operating stance
- Baseline loop
- Still loop
- Animation loop
- Review checkpoints
- Finaling rules

## Operating stance

- Do not freeform inside Blender MCP.
- Update the spec first, then issue scene changes.
- Keep one active goal per cycle: layout, camera, lighting, material, or review.
- Render proof beats viewport confidence.

## Baseline loop

1. Read the active spec.
2. Pick the current gate.
3. Apply only changes that serve that gate.
4. Render the planned frame or range.
5. Compare against `Accept If` and `Reject If`.
6. Log pass, fail, or unknown in the spec.
7. Only then move to the next gate.

## Still loop

Use when delivery is a hero frame.

1. Build collection layout first.
2. Block out the hero and background masses.
3. Lock the lens.
4. Lock the hero frame.
5. Build the light hierarchy.
6. Build the hero materials.
7. Render the hero frame in `EEVEE` at reduced resolution.
8. Render one or two secondary check frames if DOF or reflections are sensitive.
9. Move to `Cycles GPU` only after the hero frame passes.

## Animation loop

Use when delivery contains motion.

1. Build collection layout first.
2. Block out the key poses or key camera states.
3. Lock the lens family before polishing motion.
4. Define `Review Frames` and `Short Range Preview` in the spec.
5. Validate single frames before validating ranges.
6. Render short ranges in `EEVEE` at reduced resolution.
7. Fix timing, continuity, and staging before high-quality lookdev polish.
8. Move to `Cycles GPU` only for final representative checks and final output.

## Review checkpoints

- For layout:
  - Render the hero frame or the strongest composition frame.
- For lighting:
  - Render the highest-contrast frame.
- For materials:
  - Render the frame where specular behavior is most visible.
- For motion:
  - Render the peak-action range, not the whole shot.
- For transitions:
  - Render the last frames before and after the transition boundary.

## Finaling rules

- `EEVEE` during exploration.
- `Cycles GPU` for final verification and delivery.
- Start final checks with `Simplify` enabled.
- Start final checks with `Light Paths <= 7`.
- Raise cost only if a visible failure requires it.
- Never solve composition mistakes with higher samples.
- Never solve hierarchy mistakes with post effects first.
