# Persistent World and Memory

Load this reference only when the user explicitly requests cross-session memory, a persistent world, permanent progression, or save migration. Its purpose is to prevent an apparently intelligent “remembering world” from becoming untestable hidden state.

## Minimum model

Represent memory as explicit data with:

- stable event or memory IDs;
- source and timestamp or turn reference;
- conditions for activation;
- effects on state or content;
- one-shot, cooldown, or repeat behavior;
- observable later feedback;
- save version and migration behavior when the schema changes.

Use the same transition path for loaded and newly created state. Do not let the renderer silently mutate memory.

## Verification

Test at least one complete chain:

```text
action in session A
→ saved memory
→ new session or revisit
→ condition matches
→ event/effect fires
→ player can observe the remembered consequence
```

If that chain cannot be tested, describe the feature as planned rather than implemented. Keep persistent-world work outside the default V0.1 flow and do not add it merely because the narrative mentions history or consequences.
