# Scene Composition and Glyph Diorama

Read this reference when a glyph game presents a recognizable place, object, vehicle, environment, or stateful visual beat. It prevents dense character art from remaining a technical diagram, prevents labels from doing the work of illustration, and prevents prose from claiming visible motion that the scene never shows.

This is an optional visual-scene mode. Do not force it onto a grid-first arcade game when the playfield itself is the clearest composition.

## Contents

- [Core rule](#core-rule)
- [Scene contract](#scene-contract)
- [One dominant subject](#one-dominant-subject)
- [Choose a camera grammar](#choose-a-camera-grammar)
- [Layer responsibilities](#layer-responsibilities)
- [Label-blind recognition check](#label-blind-recognition-check)
- [Motion contract](#motion-contract)
- [State-bound visual change](#state-bound-visual-change)
- [Stage and mobile hierarchy](#stage-and-mobile-hierarchy)
- [Reusable visual grammar](#reusable-visual-grammar)
- [Scene verification checklist](#scene-verification-checklist)

## Core rule

Use this priority order:

> **Silhouette first. Motion second. Text third. Decoration last.**

The player should normally identify the category of the main subject before reading its explanatory label. Exact fictional identity can remain unknown when the game intends uncertainty.

## Scene contract

Extend the Glyph Spec with a compact scene record when a dedicated visual stage is useful:

```yaml
scene:
  mode: side-silhouette | field-composition | instrument-geometry
  dominant_subject: "the thing the player should notice first"
  recognition_target: "ship | dock | debris field | signal | ..."
  stage_policy: dedicated-stage | full-playfield | inline-composition
  layers:
    - background
    - structure
    - subject
    - state-object
    - effect
    - annotation
  state_bindings:
    - state: hull.condition
      visual_change: subject.patch-pattern
  motion:
    ambient: []
    semantic_continuous: []
    transition: []
```

Keep the scene contract separate from the core game rules. It describes how state becomes visible; it must not invent state that the game engine does not own.

## One dominant subject

Each scene or narrative beat should have one primary visual subject. Supporting elements establish spatial relationships but must not compete for first recognition.

Examples:

- a dock with one ship attached;
- a debris field with one readable orbit structure;
- a damaged relay with one visible asymmetry;
- an unresolved signal represented by one pulse geometry.

If a scene contains several equally important subjects, split it into successive states or use a field composition with an explicit focal object. Do not solve the problem by adding more labels and borders.

## Choose a camera grammar

Use a consistent grammar for a class of subjects instead of switching arbitrarily between icons, blueprints, specimen cards, and panels.

### Side silhouette

Use for ships, docks, large wrecks, tools, and structures whose identity depends on outline or attachment.

### Field composition

Use for debris, stars, routes, open space, crowds of objects, and environments whose meaning depends on relative position or drift.

### Instrument geometry

Use for signals, scans, unresolved objects, phase relationships, and phenomena that are only available through measurement.

Instrument geometry is a special mode. Do not use a universal scan-box wrapper for every scene.

## Layer responsibilities

Author the scene conceptually in this order:

```text
background / atmosphere
→ terrain or structure
→ primary subject
→ state object or item
→ effect / motion
→ optional annotation
```

Semantic glyphs must remain stable and visible. Atmospheric glyphs may express dust, static, light, drift, heat, decay, or interference. Decorative glyphs may frame or texture the scene but must not cover semantic content or become required for the objective.

An implementation may use multiple `<pre>` blocks, positioned glyph nodes, DOM/CSS, or another browser-native renderer. Preserve the responsibilities even when the technical layers differ.

## Label-blind recognition check

For a visual-scene slice, temporarily hide:

- location and object labels;
- explanatory prose;
- diagnostic headers and footers;
- nonessential annotations.

Ask what category of thing or place remains visible. The exact name is not required. A human visual check is appropriate here; do not replace it with a string-presence test.

If the category is not recognizable, simplify or redraw the silhouette, spatial relationship, or motion signature before adding more glyph density. Do not preserve recognition by shrinking the font until it is unreadable.

## Motion contract

Separate motion into three classes:

### Ambient motion

Nonessential life such as star breathing, dust drift, weak lights, or tiny idle float. It may stop under reduced-motion settings.

### Semantic continuous motion

Motion that the game claims the world is continuously performing, such as debris rotation, signal pulsing, wreck drift, venting, or a machinery cycle. It needs a visible glyph manifestation. A generic scan sweep is not a substitute for world motion.

### Transition motion

Short, player-triggered changes such as clamps retracting, a subject separating from a dock, a scan locking, an object being removed, or a signal resolving. It should clarify a state transition and return control promptly.

All motion must be low-cost, local, and subordinate to reading. Under `prefers-reduced-motion`, replace continuous motion with a readable static cue or low-frequency state swap. Persistent state must remain visible without animation alone.

## State-bound visual change

Use an explicit path:

```text
game state
→ scene variant
→ semantic glyph set
→ effect / motion classes
→ browser rendering
```

Examples of valid changes include a damaged silhouette gaining a breach, a repaired structure gaining a stable carrier path, or a revisited field changing its physical arrangement. Merely replacing an English label or adding random noise is not a persistent visual state change.

Prefer CSS keyframes or state-class changes when they are sufficient. Use JavaScript to bind real state and select variants; avoid a per-frame JavaScript renderer unless the chosen loop genuinely requires it.

## Stage and mobile hierarchy

When a dedicated stage is used, prefer this order:

```text
small title
→ scene stage
→ short prose or reading
→ contextual status
→ choices / controls
```

Keep prose outside critical fixed-width geometry. Keep choices separate from the scene so touch targets remain clear. Preserve silhouette readability at the target phone width; simplify the composition before shrinking glyphs excessively. A wider tablet layout may grant the stage more space without turning the scene into a dashboard.

## Reusable visual grammar

Before adding bespoke action art, ask:

> Can this visual grammar support ten related objects or events?

Prefer reusable forms such as:

- object silhouette;
- diagnostic specimen;
- unresolved partial form;
- field/map composition;
- text-only state when a drawing adds no information.

Keep routine human actions in prose unless the action itself is the visual subject. Avoid one-off hands, feet, faces, or cinematic mini-scenes that create an accidental sprite or animation pipeline.

## Scene verification checklist

- Does the scene ask one primary question?
- Is there one dominant subject?
- Is the category recognizable without labels and explanatory prose?
- Are semantic, atmospheric, and decorative elements separated?
- Does each persistent visual change come from real state?
- Does every claimed visible continuous motion have a matching visual cue?
- Does transition motion show a player-triggered world change?
- Does reduced-motion mode remain understandable?
- Can the scene fit the target mobile viewport without unreadable glyphs?
- Can the grammar be reused across related content?
- Would removing a border, label, or effect improve clarity without losing meaning?
