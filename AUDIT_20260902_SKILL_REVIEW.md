# glyph-game-builder Skill 审计与优化建议

> 来源：Archi::Mi 对 glyph-game-builder 全量文件（SKILL.md + 6 份 references + agents/openai.yaml）及 smoke test 项目（glyph-skill-smoke / SPARK RUN）的逐文件审计，结合 Dead-Reckoning 的成功经验与两个"不好玩"项目（旧神试演场、异世界商店街）的对照。
> 日期：2026-09-02

---

## 发布判断：可以发

### 理由

1. **Smoke test 闭环。** SPARK RUN 从概念到可玩产物走完全程。10 个自动化测试全绿，桌面和 390px 移动端布局验证过，QA_REPORT 完整。证明 skill 能指导 AI 编码模型从概念到可玩产物走完全程。

2. **工作流干净。** 9 步线性流程，每步职责清晰，progressive disclosure 控制参考文件加载时机。

3. **scope 控制到位。** 明确写了做什么和不做什么。Media Fit Gate 能在开工前挡掉不适合字符介质的概念。

4. **Dead-Reckoning 是旗舰证据。** 证明了 glyph diorama 这条视觉路线和设计哲学能产出真正好玩的东西。

5. **与 novel-to-game 的关键差异是优势：**
   - 从"介质"出发而不是从"小说"出发（介质先行 = 玩具先行）
   - Acceptance Contract 足够小（快速产出可判断手感的最小原型）
   - 不混淆"正确"和"完成"（轻量验收不逼 AI 做成最容易通过测试的形态）

---

## 优化建议（发布后迭代）

以下改动不 block 发布，可作为后续版本的迭代方向。按优先级排序。

### 优先级 1：实装"玩具"思维

**三处微改，不加新文件：**

#### 1a. Step 2 和 Step 3 之间插入半步——"命名玩具"

```markdown
### 2b. Name the toy

Before defining the full loop, identify the single core interaction
that should feel satisfying without any objective, score, or narrative:

- What does the player physically do? (press key, click cell, drag, tap rhythm)
- What visibly changes in the character grid as an immediate result?
- Can you describe the toy without mentioning winning, losing, or goals?

Example: "press arrow key → @ slides across the grid → walls block, sparks
vanish on contact" is a toy. "Choose the right dialogue option to increase
trust" is not a toy — it is an outcome wrapped in a menu.

If the concept has no toy, the game will default to a menu with
consequences. Identify what the player's hands are doing and what their
eyes are tracking before proceeding.
```

#### 1b. Acceptance Contract 加一条

```markdown
- the core action produces a visible, immediate change in the character
  grid that the player can understand without reading explanatory text;
```

#### 1c. Step 7 加一句提醒

在 "Implement the complete core loop before adding secondary systems..." 后追加：

```markdown
Implement the toy interaction first. Confirm that the core action and its
grid feedback work before adding objectives, scoring, or settlement logic.
```

**总改动量 < 20 行。改的是 AI 的执行顺序，不是它的审美能力。**

### 优先级 2：loop-patterns.md 补 Survival/Sandbox 循环

当前四种（Arcade / Strategy / Narrative / Hybrid）缺少日历驱动的生存沙盒模式。建议新增：

```markdown
### Survival / Sandbox

dawn settlement → free action phase (constrained by resource budget) →
dusk settlement → cycle

Defining traits:
- External pressure advances whether the player acts or not
- Player chooses WHICH actions to take with limited action points,
  not WHETHER to act
- Multiple viable strategies exist for the same cycle
- Consequences accumulate across cycles, not within a single action
```

Dead-Reckoning、*Moonlighter*、*This War of Mine*、*Darkest Dungeon* 城镇阶段均属此类型。

### 优先级 3：Acceptance Contract 加决策质量底线

```markdown
- if the game presents choices, at least one decision point has no single
  option that dominates across all reachable game states;
```

能挡住"UI 上直接写推荐配置"或"3 选 1 只有 1 个能通关"的伪选择。

### 优先级 4：scene-composition.md 触发条件放宽

```diff
- Read `scene-composition.md` when the game presents visual places, objects,
-   vehicles, environments, layered scenes, or stateful visual beats.
+ Read `scene-composition.md` unless the game is a pure grid/board with no
+   location identity (e.g. snake, tetris, minesweeper).
```

Dead-Reckoning 证明了：有场景的字符游戏让人感觉在一个"地方"里，没场景的让人感觉在看一个"界面"。

### 优先级 5：加"对象实体性"推荐

在 glyph-spec.md 或 loop-patterns.md 加一段：

```markdown
## Object identity (recommended for strategy, narrative, and survival loops)

When objects matter to gameplay, consider giving each a unique identity
rather than treating them as fungible counters:
- unique ID, not just a type count
- origin (where/when found)
- observable properties the player can inspect
- losing a specific object closes specific future possibilities
```

### 优先级 6：情境化 HUD 推荐

在 browser-rendering.md 加一段：

```markdown
Show only the status relevant to the current decision context.
A full status panel should be available on demand ([S] STATUS), not
permanently visible. Character-grid screen space is scarce; a
permanently full HUD crowds out the game world.
```

### 优先级 7：程序化音频推荐

在 browser-rendering.md 加一段可选推荐：

```markdown
Procedural Web Audio (OscillatorNode + filtered noise) can provide
ambient atmosphere without external audio assets. Consider a
two-pillar approach: tension layer + warmth layer, crossfading
based on game state.
```

---

## 不建议改的

- ❌ 不要加 novel-to-game 那种重型 QA 契约（344 行）。轻量验收是优势。
- ❌ 不要加原著保真/来源追溯。那是另一个 skill 的职责。
- ❌ 不要加 intake 问卷。当前的 "Inspect and frame" 足够。
- ❌ 不要把 Dead-Reckoning 的具体实现代码放进 skill。放模式，不放实现。

---

## Skill 的价值定位

**glyph-game-builder 解决的核心问题：AI 编码模型收到"做一个字符游戏"时默认产出的东西很烂。**

没有 skill 时 AI 做什么：
- 用 monospace 字体渲染散文加彩色边框，叫它"终端风格游戏"
- 做一个选择题式文字冒险
- 画一个 ASCII 地图但没有可交互机制
- 堆 emoji 叫它"字符游戏"

有了 skill 后的底线：
- 有明确的核心循环（不只是点击文字）
- 字符有语义分类（不只是装饰）
- 状态和渲染分离（代码可测试）
- 有真实的胜负/结算和重开
- 在手机上能用
- 有无障碍基础

**一句话：Dead-Reckoning 证明了天花板，glyph-game-builder 抬高了地板。** Skill 是你从 DR 中提炼出的设计直觉，转化成 AI 可以遵循的可执行规则。

---

## 审阅文件清单

**glyph-game-builder 主文件：**
- `SKILL.md` (150 行)
- `references/media-fit.md`
- `references/loop-patterns.md`
- `references/glyph-spec.md`
- `references/scene-composition.md`
- `references/browser-rendering.md`
- `references/persistent-world-memory.md`
- `agents/openai.yaml`

**smoke test 项目（glyph-skill-smoke）：**
- `GAME_BRIEF.md`、`GLYPH_SPEC.md`、`QA_REPORT.md`
- `game-logic.mjs`、`main.mjs`、`index.html`、`styles.css`
- `tests/game.test.mjs` (10 assertions)

**对照项目：**
- `Dead-Reckoning/` 全量源码、设计文档、测试与 QA
- `old-god-rehearsal/` 全量源码与设计演进
- `multiverse-market-street/` 全量源码
