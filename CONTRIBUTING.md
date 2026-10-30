# Contributing to Glyph Game Builder

Thank you for helping improve glyph-first game creation.

## Scope of contributions

The project is a **workflow and reference bundle**, not a browser-game framework. Changes should improve the quality or reproducibility of games made with the skill.

Good contributions include:

- clearer medium-fit decisions and more honest `FIT WITH REDUCTION` guidance;
- stronger glyph semantics, silhouette readability, scene composition, or accessibility;
- browser and mobile rendering guidance backed by concrete observations;
- small, testable improvements to the core-loop or handoff process;
- fixes to examples, typos, internal links, or cross-reference consistency.

Avoid expanding the default skill into a full engine, mandatory backend, unrelated toolchain, or overly rigid checklist.

## Before opening a pull request

1. Open an issue first for broad or behavior-changing proposals, so the goal and scope are visible.
2. Explain the real problem and the expected effect on a glyph game.
3. Keep `SKILL.md` focused. Put detailed, optional guidance into the appropriate `references/` file.
4. Preserve the current separation of game state, rules, renderer, and browser UI.
5. If you change the skill's user-facing behavior, update both README languages where necessary.

## Validation

There is **no repository-wide executable test suite** bundled here. Do not claim tests passed without running a separate game-building exercise.

For documentation-only changes, verify:

- links to files in the repository resolve;
- `SKILL.md` YAML front matter stays valid and retains `name` and `description`;
- all referenced files exist, and the mandatory vs. optional reading sequence still makes sense;
- instructions do not contradict the scope or acceptance contract.

For functional workflow changes, ideally exercise the new guidance in a **separate disposable browser-game project** and report the actual build/run commands, input paths tested, gameplay outcomes, and any visual checks performed. A report or test fixture is not a substitute for the implementation it describes.

## Pull request description

Please include: the problem, what changed, why it fits the project, how it was checked, and limitations or unverified claims.

Do not submit private prompts, credentials, user records, or code/assets you cannot license for distribution.

## License and attribution

The repository is released under **AGPL-3.0-only** (see [LICENSE](LICENSE)). Contributions intended for inclusion must be compatible with this license and appropriately attributed. By submitting a contribution, you represent that you have the rights necessary to submit it under the project's license.

Maintainers may request revisions before merging. Submitting a contribution does not guarantee acceptance.
