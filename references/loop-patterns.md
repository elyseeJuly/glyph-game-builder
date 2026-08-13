# Core Loop Patterns

Use only the section matching the chosen dominant loop. This reference prevents every glyph game from becoming a choice-based narrative and prevents visual style from replacing a playable loop.

## Arcade

```text
start → input or movement → collision/timing/collection → score, damage, or progress → fail/checkpoint → restart
```

Use discrete cells, lanes, ticks, or low-resolution timing when continuous precision would make glyphs inadequate. Make the action-feedback relationship immediately visible.

## Strategy

```text
setup → allocation/order/plan → resolution → resource or board change → objective evaluation → settlement or failure → restart
```

Expose the important state before the decision. Ensure that an action changes a resource, position, threat, relationship, or objective rather than only advancing text.

## Narrative

```text
encounter → player action or choice → consequence → information or relationship change → ending/settlement → restart
```

Use glyph layout, portraits, spatial relations, status marks, or controlled corruption as part of the narrative feedback. Do not reduce the game to prose with decorative borders.

## Hybrid

Choose one dominant loop and name the secondary loop. Keep the first playable session focused on the dominant loop. Do not introduce a second full subsystem merely because the concept contains multiple genres.

## Session contract

Every loop must identify:

- initial state;
- meaningful player action;
- observable feedback;
- state transition;
- objective evaluation;
- settlement, failure, victory, score, or checkpoint;
- restart or new-session path.

Do not require a fixed number of choices, endings, resources, or minutes. Use the smallest action vocabulary that expresses the selected loop.
