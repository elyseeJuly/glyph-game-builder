# Browser Glyph Rendering

Read this reference when the game uses Unicode, ANSI-inspired styling, responsive character cells, or mobile browser output. Its purpose is to prevent aligned terminal mockups from becoming broken browser layouts.

## Rendering rules

- Use an actual monospace font and preserve whitespace and line breaks.
- Treat display width as a rendering concern, not simply a JavaScript string length.
- Test full-width characters, combining marks, and Emoji before using them in semantic positions.
- Keep important semantic glyphs within a known character-cell budget.
- Prefer a controlled glyph palette over arbitrary Unicode decoration.
- Use CSS classes or spans to emulate ANSI-inspired color and emphasis in a browser; do not assume raw terminal escape sequences will render correctly in HTML.
- Ensure important information has a non-color cue.
- Test at least one narrow mobile viewport and one wider viewport when the project claims responsive support.
- Prevent decorative layers from changing hit targets or covering semantic content.

## Browser versus terminal

Treat `ansi-inspired` as a visual language in browser mode unless the user explicitly requests a terminal executable. A browser implementation should use DOM, CSS, or Canvas equivalents for color, emphasis, cursor-like effects, and panels.

Do not claim terminal compatibility merely because the page looks like a terminal. Do not add a terminal adapter in V0.1 unless it is explicitly requested.

## Accessibility

- Expose action labels through real buttons or keyboard bindings.
- Announce important state changes through text or an appropriate live region.
- Do not make color the only distinction between safe, dangerous, selected, or completed states.
- Keep decorative glyphs out of the meaningful reading order when possible.
