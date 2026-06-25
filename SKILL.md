---
name: ideation
title: Creative Ideation — Constraint + Direction = Creativity
description: "Route any blank-page problem to the right creative method."
version: 2.1.0
author: SHL0MS
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [Creative, Ideation, Projects, Brainstorming, Inspiration]
    category: creative
    requires_toolsets: []
---

# Creative Ideation

A 4-step routing engine for blank-page problems. Not a brainstorm — a system that picks the right creative method for *your* situation.

## When to use

Use when the user says: "我想做点什么", "没灵感", "推我一把", "卡住了", "I want to build something", "give me a project idea", "I'm bored", "inspire me", or any variant of "I have tools but no direction". Works for code, art, hardware, writing, tools, products, strategies.

## The 4-Step Routing Flow

**Constraint + direction = creativity** (the original v1 rule, still true — but v2 makes it routable).

### Step 1: Read three signals

Before generating anything, read:

1. **Stage** (which of 6 stages is the user in?). See `references/stages.md`.
   - 1. Blank Page (没方向) → 3. Stuck (卡住) → 5. Refinement (打磨)
   - Or 2. Expansion (扩张) / 4. Pivot (求变) / 6. Decision (决策)
2. **Domain**: software / writing / visual / system / personal / research / business / hardware / other
3. **Specificity**: 完全空白 (no direction) / 知道方向 (vague) / 有具体项目 (specific) / 有具体痛点 (concrete problem)

One sentence each. Quick read.

### Step 2: Check for overrides

Before default routing, check `references/overrides.md` for:
- Did the user name a specific method (TRIZ, Eno, first principles, ...)?
- Did the user say "怪一点的" / "反常识" / "weird" / "出圈"?
- Is the topic in the **high-slop blacklist** (AI startup, productivity, side hustle, learning, fitness, dating, pets, parenting, finance)?
- Did the user show specific emotion (焦虑, 完美主义, 失落, 愤怒, 自满)?

If yes, route directly to the forced method. Don't run default routing.

### Step 3: Route to a method

Default mapping (see `references/stages.md` for full table):

| Stage | First pick | Backup | Why |
|---|---|---|---|
| 1. Blank Page | #17 Mashup | #19 Persona 100, #21 Time Travel, #20 Role Storming | Need a starting point from nothing |
| 2. Expansion | #6 SCAMPER | #17 Mashup, #20 Role Storming | Need 10 variants of one thing |
| 3. Stuck | #1 Oblique Strategies | #5 Lateral Provocations, #13 Defamiliarization, #22 Everything Must Go | Need a way out, not a way in |
| 4. Pivot | #22 Everything Must Go | #17 Mashup, #21 Time Travel, #18 Anti-Goal | Need a fresh start, not refinement |
| 5. Refinement | #13 Defamiliarization | #1 Oblique Strategies, #14 Story Spine, #11 Pattern Language | Need details and texture |
| 6. Decision | #3 Pre-mortem | #18 Anti-Goal, #15 5 Whys | Need verdict, not ideas |

**Load exactly one method file from `references/methods/01-22` based on the pick.** Each method file is self-contained (originator, mechanism, when-to-use, output shape, famous examples). Don't load multiple at once — that's the routing failure mode.

### Step 4: Run anti-slop

**Every output must pass `references/anti-slop.md` Layer 1-3 before delivery to the user.** This is non-negotiable. The single biggest failure mode of LLM creativity is producing slop — outputs that pass the "noun substitution test" (swap the nouns, the idea doesn't change). Anti-slop catches that.

- Layer 1: Reject first 3 (or first 5 in high-slop domains)
- Layer 2: Force concrete anchors (names, places, mechanisms, numbers)
- Layer 3: 怪诞预算 — at least one element that needs explaining

If output fails anti-slop, **throw it out and rerun the method with stricter slop filter**. Do not deliver slop with a "BTW I notice this is generic" disclaimer — that wastes the user's time.

### Step 4.5: Self-Audit (生成后必跑, v2.1 新增)

After generating 3-5 ideas, run this checklist **before showing to the user**. If any item fails, discard all output and rerun the method with a stricter slop filter.

- [ ] **换主语测试 (Noun Substitution Test)**: Replace the user's project name / company / tool with another high-frequency word. Does the idea still "work"? If yes → slop, throw it out.
- [ ] **Layer 4 Slop 体检**: Run anti-slop.md Layer 4's 5-item checklist.
- [ ] **怪诞预算审计**: At least 1 idea has a "needs explanation" element that is **non-decorative** (improves core value, not just flavor). Decorative 怪诞 (纪念碑, random emoji, ambient audio) doesn't count.
- [ ] **可 buildability**: At least 1 idea can be built tonight (with a specific PoC step). If no idea is tonight-buildable, the output is too high-level.
- [ ] **锚点多样性 (v2.1)**: Each idea's ≥3 anchors should include at least 1 "user/scene" anchor (specific person/place/scene/time/emotion), 1 "mechanism/engineering" anchor (specific tech/number/interface), 1 "anomaly/edge" anchor (violates best practice / unusual assumption). Prevents LLM from outputting all "engineering details" anchors.

If any item fails → **discard output, rerun method with stricter filter**, do NOT deliver substandard output.

## The Rule

Every prompt is interpreted as broadly as possible. "Does this include X?" → Yes. The methods provide direction and mild constraint. Without either, there is no creativity.

## Quick Mode (when stage detection is overkill)

If the user gives a *concrete* constraint ("我想做一个 X 工具" / "我想写一篇关于 Y 的文章"), you can skip Stage 1 signal-reading and go straight to the v1 constraint library below. This is the v1 fast path — still works, just no routing.

## Constraint Library (Quick Mode)

### For Developers

**Solve your own itch:**
Build the tool you wished existed this week. Under 50 lines. Ship it today.

**Automate the annoying thing:**
What's the most tedious part of your workflow? Script it away. Two hours to fix a problem that costs you five minutes a day.

**The CLI tool that should exist:**
Think of a command you've wished you could type. `git undo-that-thing-i-just-did`. `docker why-is-this-broken`. `npm explain-yourself`. Now build it.

**Nothing new except glue:**
Make something entirely from existing APIs, libraries, and datasets. The only original contribution is how you connect them.

**Frankenstein week:**
Take something that does X and make it do Y. A git repo that plays music. A Dockerfile that generates poetry. A cron job that sends compliments.

**Subtract:**
How much can you remove from a codebase before it breaks? Strip a tool to its minimum viable function. Delete until only the essence remains.

**High concept, low effort:**
A deep idea, lazily executed. The concept should be brilliant. The implementation should take an afternoon. If it takes longer, you're overthinking it.

### For Makers & Artists

**Blatantly copy something:**
Pick something you admire — a tool, an artwork, an interface. Recreate it from scratch. The learning is in the gap between your version and theirs.

**One million of something:**
One million is both a lot and not that much. One million pixels is a 1MB photo. One million API calls is a Tuesday. One million of anything becomes interesting at scale.

**Make something that dies:**
A website that loses a feature every day. A chatbot that forgets. A countdown to nothing. An exercise in rot, killing, or letting go.

**Do a lot of math:**
Generative geometry, shader golf, mathematical art, computational origami. Time to re-learn what an arcsin is.

### For Anyone

**Text is the universal interface:**
Build something where text is the only interface. No buttons, no graphics, just words in and words out. Text can go in and out of almost anything.

**Start at the punchline:**
Think of something that would be a funny sentence. Work backwards to make it real. "I taught my thermostat to gaslight me" → now build it.

**Hostile UI:**
Make something intentionally painful to use. A password field that requires 47 conditions. A form where every label lies. A CLI that judges your commands.

**Take two:**
Remember an old project. Do it again from scratch. No looking at the original. See what changed about how you think.

See `references/full-prompt-library.md` for 30+ additional constraints across communication, scale, philosophy, transformation, and more.

## Matching Constraints to Users (Quick Mode only)

| User says | Pick from |
|---|---|
| "I want to build something" (no direction) | Random — any constraint |
| "I'm learning [language]" | Blatantly copy something, Automate the annoying thing |
| "I want something weird" | Hostile UI, Frankenstein week, Start at the punchline |
| "I want something useful" | Solve your own itch, The CLI that should exist, Automate the annoying thing |
| "I want something beautiful" | Do a lot of math, One million of something |
| "I'm burned out" | High concept low effort, Make something that dies |
| "Weekend project" | Nothing new except glue, Start at the punchline |
| "I want a challenge" | One million of something, Subtract, Take two |

For everything else, use the 4-step routing flow. Don't try to be exhaustive in the matching table — it can't cover the long tail.

## Output Format

For routing mode (4-step flow):
```
## Routing
- **Stage**: [#1-6 + 1-sentence justification]
- **Domain**: [software/writing/visual/...]
- **Specificity**: [blank/vague/specific/concrete-problem]
- **Override check**: [any of the 7 override rules triggered?]
- **Method chosen**: [#N Name] (from methods/0N-name.md)
- **Methods NOT chosen** (v2.1): [list 1-2 backup methods considered + 1-sentence rejection reason each — e.g. "#3 Pre-mortem rejected because not a Decision stage" — gives user a way to verify routing]

## Method: [Name] (originator)
[1-2 sentence mechanism summary]

### Output

[Method-specific output — see methods/0N-name.md for shape]
[Each idea passes anti-slop Layer 1-3]
[Self-audit: Step 4.5 checklist results]
```

For quick mode (constraint library):
```
## Constraint: [Name]
> [The constraint, one sentence]

### Ideas

1. **[One-line pitch]**
   [2-3 sentences: what you'd build and why it's interesting]
   ⏱ [weekend / week / month] • 🔧 [stack]

2. **[One-line pitch]**
   [2-3 sentences]
   ⏱ ... • 🔧 ...

3. **[One-line pitch]**
   [2-3 sentences]
   ⏱ ... • 🔧 ...
```

## Example (routing mode)

User: "我做 v6.3 idle RPG 卡住了，AI 生成的素材太丑，想换思路但不知道换什么"

```
## Routing
- **Stage**: #3 Stuck (clearly 卡住) + #4 Pivot (换思路)
- **Domain**: visual/game design
- **Specificity**: concrete problem (v6.3 素材太丑)
- **Override check**: 
  - User 没说方法名
  - 没要求 "怪"
  - 不在高 slop 领域
  - 没显示极端情绪
  - → No overrides
- **Method chosen**: #22 Everything Must Go (matches "PIVOT + STUCK" combo)
  Backup: #13 Defamiliarization

## Method: Everything Must Go (Rob Walker & Joshua Glenn, 2009)
把 v1 放进抽屉。从"v1 不存在"重新做一次，保留教训。

### Output

**Lessons from v6.3 (用 #15 5 Whys 跑一遍):**
- 为什么 v6.3 素材"丑"？LPC 24px 风格与暗黑写实调性冲突
- 为什么用 LPC？早期为了"快"妥协
- 为什么当时妥协？没找到低成本高质量替代
- 为什么没找到？因为搜索路径错了（用错关键词）
- **根因**：v1 的 DNA 是"快速原型"，但现在用户要"暗黑写实" — DNA 错位

**v2 (5-min sketch) — 假设 v1 不存在:**

1. **Wesnoth + Diablo II 资产 + 重新动画**: 用 Battle for Wesnoth 的 CC0 资产(540 帧)做基础，重画阴影 + 描边做"暗调"。零生成成本,质量中上。**违反 best practice**: 用别人的资产,但开源+CC0+改大,合法且有出处。
   ⏱ 周末 • 🔧 6.3 现有代码不动,只换 assets/

2. **手绘 5 主角 + 5 怪物, 出场顺序动态切换**: 不做完整 sprite sheet。每场战斗前 AI 生成一次(用 minimax-image-01 + inpaint)。每张图 8K 训练出来的暗调。**怪诞预算**: 主角每次战斗"变脸",叙事上解释为"被地下城记忆污染"。
   ⏱ 2 周 • 🔧 AI 资产 + 离线缓存

3. **抽象派 2D + 黑色氛围**: 不做"写实"了,做"抽象暗黑" — 参考 Hyper Light Drifter。96 帧动态粒子+纯黑背景+高对比血红色强调。**反 best practice**: 玩家认不出角色脸 → 但这是"地下城身份丢失"的叙事钩子,服务于剧情。
   ⏱ 1 周 • 🔧 现有 6.3 删一半,只留战斗循环

[每个 idea 都过 anti-slop Layer 1-3: 有具体工具/时间/反 best practice 元素,无 "AI 重新定义 X" slop]

**Merged direction**: 选 #2 路线 (手绘 5 主角 + AI 重生),保留 v1 的战斗循环代码,把 v1 的 LPC 资产全部归档不删。
```

## File Map

```
creative-ideation/
├── SKILL.md                              # This file (主入口)
├── references/
│   ├── anti-slop.md                      # Layer 1-3 slop filter
│   ├── stages.md                         # Stage 1-6 detection rules
│   ├── overrides.md                      # 7 override rules
│   ├── full-prompt-library.md            # v1 quick mode 30+ constraints
│   └── methods/                          # 22 method files (load on demand)
│       ├── 01-oblique-strategies.md
│       ├── 02-triz.md
│       ├── 03-premortem.md
│       ├── 04-oulipo.md
│       ├── 05-lateral-provocations.md
│       ├── 06-scamper.md
│       ├── 07-biomimicry.md
│       ├── 08-first-principles.md
│       ├── 09-jobs-to-be-done.md
│       ├── 10-pataphysics.md
│       ├── 11-pattern-language.md
│       ├── 12-affinity-diagrams.md
│       ├── 13-defamiliarization.md
│       ├── 14-story-spine.md
│       ├── 15-5-whys.md
│       ├── 16-crazy-eights.md
│       ├── 17-mashup.md
│       ├── 18-anti-goal.md
│       ├── 19-persona-100.md
│       ├── 20-role-storming.md
│       ├── 21-time-travel.md
│       └── 22-everything-must-go.md
```

## Anti-Slop Reminder (read it, internalize it)

**Every output goes through anti-slop.md Layer 1-3 before delivery.** The single biggest failure mode of LLM creativity is producing slop — outputs that pass the noun substitution test. If your output could have "Wei, 32, Shanghai" replaced with "小李, 28, 北京" and not lose any meaning, it's slop. Force specific anchors. Force 怪诞预算. Reject first 3 (or 5 in high-slop domains).

## Attribution

v1 (1.0.0) by SHL0MS — constraint approach inspired by [wttdotm.com/prompts.html](https://wttdotm.com/prompts.html). Adapted and expanded for software development and general-purpose ideation.

v2.0 (2.0.0) adds 4-step routing engine, 22 method library (each with named originator and provenance), 6-stage detection, 7 override rules, and 4-layer anti-slop system. The 22 methods are not LLM-invented — each cites a specific human originator: Brian Eno (Oblique Strategies, 1975), Genrich Altshuller (TRIZ, 1946), Gary Klein (Pre-mortem, 2007), Raymond Queneau (OuLiPo, 1960), Edward de Bono (Lateral Thinking, 1970), Bob Eberle/Alex Osborn (SCAMPER, 1971), Janine Benyus (Biomimicry, 1997), Aristotle/Elon Musk (First Principles), Clayton Christensen (JTBD, 2016), Alfred Jarry (Pataphysics, 1893), Christopher Alexander (Pattern Language, 1977), Jiro Kawakita (Affinity Diagrams, 1960s), Viktor Shklovsky (Defamiliarization, 1917), Kenn Adams/Pixar (Story Spine, 2003), Sakichi Toyoda (5 Whys, 1930s), Google Ventures (Crazy 8s, 2010s), Arthur Koestler (Mashup, 1964), Charlie Munger (Anti-Goal), Rob Walker/Joshua Glenn (Everything Must Go, 2009), Rick Griggs (Role Storming, 1980s), Anthony Dunne/Fiona Raby (Time Travel/Speculative Design, 1990s).

v2.0.1 (2.0.1) fixes Stage 3 vs Stage 4 priority — "想换思路" = Pivot > Stuck (was Stuck > Pivot). Found by sub-agent during v6.3 idle RPG stress test.

v2.1 (2.1.0) — iteration on v2.0.1, validated against 3 real problems (HTML5 commercial strategy, Hermes upgrade decision, ThirdSpace vault refinement). Six fixes:
1. **stages.md**: Stage vs Override conflict resolution — "看动词不看形容词" + "Stage 5 > Override 2" by default. Fixes routing ambiguity exposed in Problem 3 (vault refinement).
2. **SKILL.md Step 4.5**: New forced self-audit before delivery — noun substitution test, layer 4 体检, 怪诞预算审计 (non-decorative), buildability, 锚点多样性.
3. **SKILL.md Output Format**: "Methods NOT chosen" with rejection reason — routing becomes auditable, not black-box.
4. **anti-slop.md Layer 2.5**: Anchor diversity rule (1 user/scene + 1 mechanism/engineering + 1 anomaly/edge per idea). Prevents LLM over-output of "engineering details" anchors.
5. **anti-slop.md Layer 5**: No hallucinated references. Specific products/companies/cases need at least 1 verifiable fact. Statistics must use hedging. Fixes Bug #2 (引用《大多数》手游"丑出了梗流量涨" as evidence without basis).
6. **overrides.md Rule 8**: Default 怪倾向 for Stage 3/4/5 — Stage 6 Decision exempt.
7. **methods/13-defamiliarization.md**: 5-Dimension Martian Template (action / time / space / energy / silence) — silence dimension captures "attention blank spots" (the gold mine for capture opportunities).
