# Glyph Game Builder

**A reusable Agent Skill for building playable, glyph-first browser games.**

[简体中文](README.zh-CN.md) · [Skill instructions](SKILL.md) · [Contributing](CONTRIBUTING.md) · [License](LICENSE)

Glyph Game Builder helps a coding agent turn a game concept into a **small but complete, testable browser game** where ASCII, Unicode, or ANSI-inspired characters are the primary visual language—not a decorative wrapper around paragraphs or menus.

**This repository contains an Agent Skill, not a game engine or a ready-to-play game.** It provides a repeatable design, implementation, and verification workflow. The coding agent and the target project provide the actual runtime and code.

## What makes it different

- **Media Fit Gate:** Decide whether the concept genuinely works as a glyph-based game: `FIT`, `FIT WITH REDUCTION`, or `NOT FIT`.
- **One dominant gameplay loop:** Define inputs, observable feedback, state changes, an objective, a settlement condition, and a restart path before increasing scope.
- **Glyphs with meaning:** Distinguish `semantic`, `atmospheric`, and `decorative` glyphs. Tie gameplay-critical visuals to real state and provide non-color cues.
- **Scene composition where appropriate:** Prioritize silhouettes, spatial readability, state-bound motion, and label-blind recognition for ships, environments, and other recognizable subjects.
- **Browser-first verification:** Check keyboard/touch access, readable character grids, responsive layout, reduced-motion behavior when applicable, and testable state transitions.
- **Honest handoff:** Report what was tested and what remains unverified.

## Good fits

A character-grid arcade game, a small tactical or resource-management game, or a glyph-native interactive scene with a genuinely playable loop.

Not a good fit by default: a prose-only text adventure, decorative terminal UI, MUD, multiplayer backend, image-first or 3D-first game, or a concept whose essential interaction cannot be conveyed through the glyph medium.

## Installation and use

1. Clone or download this repository.
2. Place the **whole directory** (including `SKILL.md`, `references/`, `agents/`, and `assets/`) where your chosen Agent Skills-compatible host discovers skills, or register that directory using the host's documented skills mechanism.
3. Start your coding agent in a separate game project and explicitly ask it to use `glyph-game-builder`.

For example:

```text
Use the glyph-game-builder skill to make a small, single-player browser game
about navigating a damaged orbital station. Build one complete playable loop.
Use ASCII/Unicode glyphs as the primary visual medium, support keyboard and
touch where appropriate, and deliver GAME_BRIEF.md, GLYPH_SPEC.md, runnable
frontend files, and QA_REPORT.md. Verify the game rather than only describing it.
```

**Host support varies.** The included `agents/openai.yaml` is host-specific metadata; `SKILL.md` and `references/` are the portable core. This repository does not automatically install itself or claim to work identically in every agent runtime.

## Workflow at a glance

```text
Inspect concept and project
      ↓
Media Fit Gate
      ↓
Choose one core loop
      ↓
Define Glyph Spec
      ↓
Compose scenes if needed
      ↓
Model state and transitions
      ↓
Implement a playable vertical slice
      ↓
Test rules, controls, layout, and visuals
      ↓
Deliver game + specifications + QA report
```

The detailed nine-step workflow and acceptance contract are in [SKILL.md](SKILL.md). The reference guides are **loaded only when relevant**, rather than all at once.

## Repository layout

```text
glyph-game-builder/
├── SKILL.md                      # Main skill and acceptance contract
├── agents/openai.yaml            # Host-specific interface metadata
├── assets/icon.svg               # Skill icon
├── references/
│   ├── media-fit.md              # Medium suitability check
│   ├── loop-patterns.md          # Gameplay loop patterns
│   ├── glyph-spec.md             # Glyph semantics and mappings
│   ├── scene-composition.md      # Glyph diorama and visual composition
│   ├── glyph-surface-rendering.md# Optional material/light/occlusion guidance
│   ├── browser-rendering.md      # Browser, input, layout, accessibility
│   └── persistent-world-memory.md# Optional persistence guidance
├── README.zh-CN.md
├── CONTRIBUTING.md
├── SECURITY.md
└── LICENSE
```

The repository also preserves historical audit notes. Those are background records, not required installation dependencies or included game demos.

## Expected output from a game-building task

The skill asks the coding agent to produce:

1. `GAME_BRIEF.md` — platform, core loop, and playable-session contract.
2. `GLYPH_SPEC.md` — the game's actual character/state mapping.
3. A runnable browser-based, glyph-first game.
4. `QA_REPORT.md` — commands, paths tested, known failures, and unverified items.

These are **expected outputs of an agent run**, not bundled example files in this repository. No standalone game, automated test runner, or demo is shipped here.

## Contributing and responsible use

Improvements to game design guidance, glyph readability, accessibility, and verification methodology are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) before proposing changes. Report suspected vulnerabilities through the process in [SECURITY.md](SECURITY.md).

## License

**Copyright © 2026 elyseeJuly.**

This repository is licensed under the **GNU Affero General Public License v3.0 only (`AGPL-3.0-only`)**; see [LICENSE](LICENSE). Modified, distributed, and network-served versions of covered software are subject to the applicable requirements of that license. Commercial use is **not prohibited**.

The license covers this repository's licensed materials. It does **not automatically impose AGPL on independently created games** merely because an agent followed this skill; the rights and licensing of a particular game depend on the material actually incorporated into that game.

If you want to reuse the skill's text in a way incompatible with AGPL-3.0-only, seek separate permission from the relevant copyright holders.
