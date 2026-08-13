# Media Fit Gate

Use this reference before designing a glyph-first game. Its purpose is to prevent a concept whose core depends on high-fidelity graphics, continuous physics, or networked simulation from being relabeled as an ASCII game.

## Questions

Answer these questions from the concept:

1. Can the primary player action be represented by cells, symbols, discrete timing, resources, or explicit state?
2. Can the important feedback be shown through glyph position, substitution, layering, color plus a non-color cue, or concise text?
3. Can a small glyph legend communicate the important objects and states?
4. Can the core loop fit within a browser character grid without pixel-level precision?
5. Can the first session reach a meaningful result without a backend, multiplayer service, or large asset pipeline?

## Classification

### FIT

Use when the answer to the first four questions is yes and no hard blocker is present. Proceed with the normal workflow.

Good candidates include grid movement, symbolic combat, resource allocation, terminal-style management, constrained observation, small narrative scenes, and low-resolution arcade loops.

### FIT WITH REDUCTION

Use when the concept has a glyph-native core but also asks for a non-glyph presentation layer. Preserve the discrete core and explicitly downgrade the unsupported layer.

Examples:

- replace cinematic camera movement with changing spatial composition;
- replace facial animation with portrait glyph states and dialogue consequences;
- replace a large world with one representative location;
- replace precise aiming with discrete lanes, cells, or timing windows.

### NOT FIT

Stop and explain the blocker when the core experience requires one or more of the following:

- pixel-accurate aiming or continuous physics;
- high-fidelity facial performance or image identity;
- complex 3D camera, depth, or animation as the main feedback;
- multiplayer real-time synchronization;
- a large natural-language parser while glyph space is only decoration;
- a backend or persistent simulation that cannot be reduced to a local slice.

Do not hide the blocker behind borders, random glyph corruption, or terminal-colored prose. Offer a different medium or ask whether the user accepts a reduced glyph-native slice.
