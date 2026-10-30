# Glyph Game Builder｜字符游戏构建 Skill

**让编程 Agent 用 ASCII、Unicode 和 ANSI 风格字符，制作真正可玩的浏览器游戏。**

[English](README.md) · [Skill 主文件](SKILL.md) · [贡献指南](CONTRIBUTING.md) · [开源协议](LICENSE)

Glyph Game Builder 是一个可复用的 **Agent Skill**。它帮助 AI 把游戏构想落实为具有真实交互、状态变化、完整核心循环和可验证结果的字符游戏，而不是给文字菜单加一个终端风格边框。

**本仓库是 Skill，不是游戏引擎，也不附带现成可玩的游戏。** 它提供的是设计、实现与验收方法；实际游戏代码由运行 Skill 的编程 Agent 在目标项目中生成。

## 核心能力

- **介质适配判断（Media Fit Gate）**：先判断构想适不适合字符游戏，结果分为 `FIT`、`FIT WITH REDUCTION`、`NOT FIT`，不为了做字符而强行牺牲玩法。
- **真实的核心循环**：明确玩家动作、即时反馈、状态转换、目标与结算，以及重新开始的路径。
- **有意义的字符**：将字符区分为语义（`semantic`）、氛围（`atmospheric`）、装饰（`decorative`）三类。影响玩法的信息必须与真实状态关联，不只靠颜色传达。
- **字符场景构图**：对空间、飞船、地貌、建筑等可辨认场景，重视轮廓、空间关系、动态表现和隐藏标签后的识别能力。
- **浏览器优先**：关注键盘与触控操作、字符网格、移动端适配、无障碍，以及状态逻辑的测试可行性。
- **真实验收**：不把“看起来完成”当作测试通过；明确说明已经验证和尚未验证的部分。

## 适合与不适合

适合：字符网格街机游戏、小型策略或资源管理游戏、以字符场景为主要视觉表达且拥有真实玩法循环的交互游戏。

默认不适合：纯文字冒险、以装饰性终端界面包装的散文、多用户在线世界、依赖复杂后端的游戏、以图片或 3D 为主要视觉介质的游戏。

## 如何安装与使用

1. Clone 或下载整个仓库。
2. 将**完整文件夹**（包括 `SKILL.md`、`references/`、`agents/`、`assets/`）放入你所使用的 Agent Skills 兼容宿主支持的技能目录，或者按宿主文档注册该目录。
3. 在另外的游戏项目里启动编程 Agent，并要求它使用 `glyph-game-builder`。

示例指令：

```text
使用 glyph-game-builder Skill，制作一个以废弃空间站探索为主题的
纯前端单人字符游戏。先判断字符介质是否合适，再完成一个真正可玩的
核心循环。以 ASCII/Unicode 字符为主要视觉表达，按玩法需要支持
键盘与触控，交付 GAME_BRIEF.md、GLYPH_SPEC.md、可运行的游戏代码
和 QA_REPORT.md。需要实际验证交互和状态转换，不要只给设计方案。
```

不同宿主的 Skill 加载方式可能不同。`agents/openai.yaml` 属于特定宿主使用的界面元数据；可移植的核心是 `SKILL.md` 和 `references/`。

## 工作流程

```text
理解游戏构想与项目
      ↓
介质适配检查
      ↓
选择主要玩法循环
      ↓
定义 Glyph Spec
      ↓
按需设计字符场景构图
      ↓
拆分状态、规则与渲染
      ↓
实现完整的可玩切片
      ↓
验证机制、交互、画面与适配
      ↓
交付游戏、规格与 QA 报告
```

详细九步流程和验收要求请阅读 [SKILL.md](SKILL.md)。参考资料采取按需加载的方式，并非每次都必须全部阅读。

## 仓库组成

- `SKILL.md`：主工作流、适用范围、验收要求。
- `references/media-fit.md`：字符介质适配判断。
- `references/loop-patterns.md`：街机、策略、叙事和混合游戏循环。
- `references/glyph-spec.md`：字符语义、坐标和图层约束。
- `references/scene-composition.md`：字符场景与画面构图。
- `references/glyph-surface-rendering.md`：按需使用的材质、光照和遮挡方法。
- `references/browser-rendering.md`：浏览器字符渲染、操作和无障碍。
- `references/persistent-world-memory.md`：仅在明确需要持久世界时使用。
- `agents/openai.yaml` 与 `assets/icon.svg`：宿主元数据与图标。

跨项目历史审查报告已归档在本仓库之外；这些报告不是 Skill 安装或运行必需的文件。

## Skill 运行后应该交付什么

一个新游戏或重要改版应当包含 `GAME_BRIEF.md`、`GLYPH_SPEC.md`、可运行的纯前端游戏，以及 `QA_REPORT.md`。这些是 **Skill 要求 Agent 在目标项目中创建的交付物**，并非本仓库已经附带的示例游戏。本仓库不提供独立游戏 Demo 或自动化测试运行器。

## 贡献与授权

欢迎改进字符美术、玩法设计、浏览器兼容性、无障碍与验收规范。提交修改前请阅读 [CONTRIBUTING.md](CONTRIBUTING.md)，安全问题按 [SECURITY.md](SECURITY.md) 处理。

**Copyright © 2026 elyseeJuly.**

本仓库采用 **GNU Affero General Public License v3.0 only（`AGPL-3.0-only`）**，完整协议见 [LICENSE](LICENSE)。修改、分发受保护的作品以及通过网络提供修改版服务时，应履行协议对应的开源义务。**该协议不禁止商业使用。**

本协议覆盖本仓库获得授权的内容；**仅仅让 Agent 遵循本 Skill 制作游戏，不代表那个独立制作的游戏自动适用 AGPL**。具体应根据游戏实际使用和改编的受版权保护材料判断。

如果需要以与 AGPL-3.0-only 不兼容的方式复用 Skill 原文，应向相关版权持有人另行取得许可。
