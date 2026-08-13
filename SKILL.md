---
name: glyph-game-builder
description: Create playable browser games whose primary visual medium is ASCII, Unicode, or ANSI-inspired glyphs. Use when a coding agent must turn a game concept into a glyph-based game with a complete core loop, state-driven rendering, keyboard or touch input, and mechanical verification. Do not use for ordinary text adventures, MUDs, multiplayer worlds, image-first or 3D-first games, or backend game systems.
---

# Glyph Game Builder

Turn a game concept into a small, playable, glyph-first browser game. Keep the Skill focused on decisions and workflow; load detailed domain guidance only when the current phase requires it.

## Default scope

- Prefer a browser, pure frontend, single-player implementation.
- Use ASCII, Unicode, or ANSI-inspired glyphs as the primary visual medium.
- Build one complete vertical slice with one dominant core loop.
- Support the input model that fits the loop: keyboard, buttons, touch, or a combination.
- Do not add images, 3D assets, multiplayer networking, a backend, a general-purpose game engine, a full natural-language parser, or a persistent world unless the user explicitly changes scope.

## Workflow

### 1. Inspect and frame

Read the concept and the current repository before changing files. State the intended platform, player action, objective, failure or settlement condition, and the smallest playable session. Preserve existing project conventions when they already fit the scope.

Do not invent a large mechanic set to compensate for an underspecified concept. Ask only for information that blocks the core loop; otherwise record a narrow implementation assumption.

### 2. Run the Media Fit Gate

Read [media-fit.md](references/media-fit.md). Classify the concept as `FIT`, `FIT WITH REDUCTION`, or `NOT FIT` before designing the implementation.

- For `FIT`, continue.
- For `FIT WITH REDUCTION`, state what will be preserved and what will be downgraded before continuing.
- For `NOT FIT`, explain the blocker and stop glyph-game implementation unless the user accepts a revised glyph-native slice.

Do not call a prose-only interface a glyph game merely because it uses a monospace font or terminal decoration.

### 3. Define the core loop

Read only the relevant section of [loop-patterns.md](references/loop-patterns.md). Select one dominant loop: arcade, strategy, narrative, or a justified hybrid.

Specify:

```text
initial state → player action → feedback → state transition → objective evaluation → settlement/failure/victory → restart
```

Do not impose a fixed number of choices or a fixed session duration. Match the action vocabulary and completion condition to the selected loop.

### 4. Define the Glyph Spec

Read [glyph-spec.md](references/glyph-spec.md). Create a compact Glyph Spec before implementing the renderer.

Every important glyph must be classified as `semantic`, `atmospheric`, or `decorative`. Bind semantic glyphs to game state and provide a legend, fallback, or non-color cue where needed. Atmospheric and decorative glyphs must not carry information required to complete the game.

### 5. Model state before rendering

Separate the game into:

```text
state → action/rules → transition → glyph renderer → browser UI
```

Keep rules and state transitions testable without the DOM when practical. Make each core action produce an observable consequence. Mark any mechanics added by the agent as inferred or newly introduced when the concept is an adaptation of source material.

### 6. Build the smallest playable slice

Implement the complete core loop before adding secondary systems, large content sets, persistent progression, or visual effects. Keep the primary playfield character-based. Provide the input method required by the chosen loop and a visible route to settlement, failure, victory, or restart.

If the game is browser-based and uses Unicode, ANSI-inspired styling, responsive cells, or mobile layout, read [browser-rendering.md](references/browser-rendering.md) before finalizing the renderer.

### 7. Verify mechanically and visually

Run the repository's existing checks first. Add only small project-local tests needed to verify:

- the project starts or builds;
- the core action changes state;
- the main result node is reachable;
- restart returns to a valid initial state;
- seeded behavior is reproducible when randomness affects the core loop;
- the glyph layout does not obviously overflow at the target viewport;
- required information is not conveyed by color alone.

Use an available browser or equivalent runtime check when possible. Record unverified visual or device-specific claims instead of implying success.

### 8. Deliver the handoff

For a new or substantially changed game, provide:

- `GAME_BRIEF.md` with the core loop and session contract;
- `GLYPH_SPEC.md` with the actual glyph mapping used by the game;
- the runnable pure-frontend game;
- `QA_REPORT.md` with commands, tested paths, known failures, and unverified items.

Do not add a Skill README, marketing copy, a large demo, or unrelated project documentation.

## Persistent world and memory

Keep the default session self-contained. Do not infer a persistent world from words such as “history”, “remember”, or “consequence”. Read [persistent-world-memory.md](references/persistent-world-memory.md) only when the user explicitly requests cross-session memory, a persistent world, permanent progression, or save migration.

## Acceptance contract

Accept a V0.1 result only when one session can experience the game's complete dominant loop:

- at least one meaningful player action is available;
- the action causes observable feedback and a meaningful state change;
- the objective can be evaluated;
- the player can reach settlement, failure, victory, or an equivalent score/checkpoint result;
- the player can restart or begin a new session;
- the character medium carries spatial, object, or state meaning rather than only decoration;
- no required control is dead or unreachable;
- the implementation stays within the agreed scope.

Do not require every game to have three choices, a fixed number of endings, a fixed session length, a map, resources, or persistent saves.

## Progressive disclosure map

- Always use this file for scope, gate, workflow, and acceptance.
- Read `media-fit.md` during the fit gate.
- Read the relevant part of `loop-patterns.md` after selecting the dominant loop.
- Read `glyph-spec.md` before defining character semantics or the renderer.
- Read `browser-rendering.md` only for browser character-cell, Unicode, ANSI-inspired, responsive, or accessibility concerns.
- Read `persistent-world-memory.md` only after explicit persistent-world scope is accepted.

Do not load every reference by default. Do not create bundled scripts unless repeated blind testing demonstrates a deterministic check that cannot be kept as a project-local test.
