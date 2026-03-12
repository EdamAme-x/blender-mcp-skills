# Failure Patterns

## Table of Contents
- Flat lighting
- Midtone soup
- Default-lens syndrome
- Random-detail disease
- Material sameness
- Toy-scale look
- Over-DOF
- Wet-everything look
- Background competition
- Fix order

## Flat lighting

- Symptom:
  - Everything is visible but nothing feels designed.
- Cause:
  - Key and fill are too similar.
  - No shadow shape is controlling form.
- Fix:
  - Rebuild with one dominant key.
  - Lower fill.
  - Add negative fill or rim only after key reads.

## Midtone soup

- Symptom:
  - The image feels muddy and indecisive.
- Cause:
  - Foreground, hero, and background live in the same value band.
- Fix:
  - Regroup values into separate bands.
  - Give the hero the strongest local contrast.

## Default-lens syndrome

- Symptom:
  - The shot looks like an unplanned viewport screenshot.
- Cause:
  - Camera lens was never chosen intentionally.
- Fix:
  - Re-select the lens based on story intent.
  - Check whether wider or longer lens improves hierarchy.

## Random-detail disease

- Symptom:
  - The render looks busy but not rich.
- Cause:
  - Detail was added uniformly at every scale.
- Fix:
  - Restore large-medium-small structure.
  - Remove detail from non-hero areas first.

## Material sameness

- Symptom:
  - Metal, plastic, paint, and rubber all feel related in a bad way.
- Cause:
  - Roughness ranges overlap too much.
  - Lighting is too flat to reveal differences.
- Fix:
  - Separate material classes by roughness and specular response.
  - Recheck under directional light.

## Toy-scale look

- Symptom:
  - The scene feels miniature even if modeling is competent.
- Cause:
  - No convincing scale anchor.
  - Microdetail dominates macro structure.
- Fix:
  - Add believable scale cues.
  - Rebalance detail toward larger forms.

## Over-DOF

- Symptom:
  - The image feels like it is hiding problems behind blur.
- Cause:
  - `f-stop` is too low for the framing and subject scale.
- Fix:
  - Raise `f-stop`.
  - Reconfirm which plane actually needs focus.

## Wet-everything look

- Symptom:
  - Everything looks glossy, oily, or artificially premium.
- Cause:
  - Specular highlights are being used as decoration.
- Fix:
  - Reduce highlight spread.
  - Reserve strong specular behavior for selected materials.

## Background competition

- Symptom:
  - The eye keeps leaving the hero.
- Cause:
  - Background contrast, saturation, or detail is too strong.
- Fix:
  - Reduce background contrast first.
  - Then reduce background sharpness or saturation.

## Fix order

- Fix composition before material polish.
- Fix lens choice before DOF polish.
- Fix value grouping before color tuning.
- Fix lighting hierarchy before adding fog, bloom, glare, or other cosmetics.
- Fix silhouette and background competition before adding small detail.
