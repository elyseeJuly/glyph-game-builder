# Glyph Spec

Use this reference to define the character vocabulary before implementing the renderer. The purpose is to prevent unstable symbol meanings, inaccessible color-only feedback, and decorative terminal layouts that do not carry gameplay.

## Minimal schema

```yaml
medium: ascii | unicode | ansi-inspired | hybrid
runtime: browser

grid:
  coordinate_system: row-column
  width: <number>
  height: <number>
  cell_policy: fixed | responsive
  font_family: monospace

layers:
  - background
  - terrain
  - actor
  - item
  - effect
  - ui

glyphs:
  - id: player
    char: "@"
    role: semantic
    display_width: 1
    layer: actor
    meaning: player_position
    state_binding: player.position
    interaction: controllable
    fallback: "P"
    legend: true
    non_color_cue: position

  - id: fog
    char: "·"
    role: atmospheric
    display_width: 1
    layer: effect
    state_binding: weather.fog
    legend: false
    gameplay_meaning: null

  - id: frame_corner
    char: "┌"
    role: decorative
    display_width: 1
    layer: ui
    state_binding: null
    legend: false
```

## Roles

### Semantic glyph

A glyph is semantic when the player must understand it, or when game rules depend on it. It must have a stable meaning, an explicit state binding, and a legend or other discoverable explanation. Its meaning must not depend only on color.

### Atmospheric glyph

An atmospheric glyph expresses mood or a state-adjacent effect such as fog, static, heat, decay, or corruption. It may change with state, but it must not be the only way to discover a required objective, danger, or control.

### Decorative glyph

A decorative glyph provides framing, spacing, texture, or terminal identity. It has no gameplay meaning and no state binding. Removing it must not change the result of a session.

## Required checks

- Give every semantic glyph a unique meaning within its layer.
- Record display width for glyphs that may not occupy one browser cell.
- Keep semantic, atmospheric, and decorative glyphs in separate lists or clearly marked records.
- Provide a fallback for important non-ASCII glyphs when practical.
- Use text, position, shape, or labels in addition to color for important information.
- Keep layers deterministic; decorative effects must not cover semantic glyphs.
- Add a small legend when the mapping is not self-evident.
