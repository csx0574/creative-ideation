# Creative Ideation v2.1 — Constraint + Direction = Creativity

A 4-step routing engine for blank-page problems. Not a brainstorm — a system that picks the right creative method for *your* situation.

> **Based on SHL0MS's [v1.0.0](https://github.com/NousResearch/hermes-agent/tree/main/optional-skills/creative/creative-ideation) constraint library, completely restructured into a 22-method routing engine in v2.0/v2.1.**

## What's new in v2.1 (vs v2.0.1 / v1.0.0)

- **v1.0.0** (SHL0MS, 2024): 30+ constraint prompts, no routing, no anti-slop
- **v2.0.0**: Added 4-step routing (signals → overrides → route → anti-slop), 22 method library with named originators, 6-stage detection, 7 override rules
- **v2.0.1**: Fixed Stage 3 vs Stage 4 priority — "想换思路" = Pivot > Stuck
- **v2.1.0**: Six fixes after stress-testing on 3 real problems (HTML5 game studio commercial strategy, Hermes upgrade decision, vault refinement)

### v2.1 specific fixes

1. **stages.md**: Stage vs Override conflict resolution — "看动词不看形容词" + "Stage 5 > Override 2" by default
2. **SKILL.md Step 4.5**: New forced self-audit before delivery (noun substitution test, layer 4 体检, 怪诞预算审计 non-decorative, buildability, 锚点多样性)
3. **SKILL.md Output Format**: "Methods NOT chosen" with rejection reason — routing becomes auditable
4. **anti-slop.md Layer 2.5**: Anchor diversity rule (1 user/scene + 1 mechanism/engineering + 1 anomaly/edge per idea)
5. **anti-slop.md Layer 5**: No hallucinated references — specific products/cases need ≥1 verifiable fact
6. **overrides.md Rule 8**: Default 怪倾向 for Stage 3/4/5 — Stage 6 Decision exempt
7. **methods/13-defamiliarization.md**: 5-Dimension Martian Template (action / time / space / energy / silence)

## Install

```bash
mkdir -p ~/.hermes/skills/creative-ideation
cp -R ./* ~/.hermes/skills/creative-ideation/
```

Or via `clawdhub` / `hermes skills install` if you're running Hermes Agent.

## Use

Trigger this skill when the user says: "我想做点什么", "没灵感", "推我一把", "卡住了", "I want to build something", "give me a project idea", "I'm bored", "inspire me", or any variant of "I have tools but no direction".

The skill runs a 4-step routing flow:
1. **Read signals** (stage / domain / specificity)
2. **Check overrides** (8 rules)
3. **Route to a method** (one of 22)
4. **Run anti-slop** (Layer 1-3 + Layer 2.5 diversity + Layer 5 no hallucination)
5. **Self-audit** (Step 4.5 checklist)

See `SKILL.md` for the full flow.

## The 22 Methods

Each method is a standalone file in `references/methods/` with the originator's name, year, mechanism, when-to-use, and output shape. Methods are not LLM-invented — each cites a specific human originator:

| # | Method | Originator | Year |
|---|---|---|---|
| 01 | Oblique Strategies | Brian Eno + Peter Schmidt | 1975 |
| 02 | TRIZ | Genrich Altshuller | 1946 |
| 03 | Pre-mortem | Gary Klein | 2007 |
| 04 | OuLiPo | Raymond Queneau + François Le Lionnais | 1960 |
| 05 | Lateral Provocations (PO) | Edward de Bono | 1970 |
| 06 | SCAMPER | Bob Eberle / Alex Osborn | 1971 |
| 07 | Biomimicry | Janine Benyus | 1997 |
| 08 | First Principles | Aristotle / Elon Musk (modern) | ancient |
| 09 | Jobs-to-be-Done | Clayton Christensen | 2016 |
| 10 | Pataphysics | Alfred Jarry | 1893 |
| 11 | Pattern Language | Christopher Alexander | 1977 |
| 12 | Affinity Diagrams | Jiro Kawakita | 1960s |
| 13 | Defamiliarization | Viktor Shklovsky | 1917 |
| 14 | Story Spine | Kenn Adams / Pixar | 2003 |
| 15 | 5 Whys | Sakichi Toyoda | 1930s |
| 16 | Crazy 8s | Google Ventures | 2010s |
| 17 | Mashup / Combinatorial Creativity | Arthur Koestler | 1964 |
| 18 | Anti-Goal | Charlie Munger / Ray Dalio | modern |
| 19 | 100 Personas | (practitioner method) | — |
| 20 | Role Storming | Rick Griggs | 1980s |
| 21 | Time Travel Ideation | Anthony Dunne + Fiona Raby | 1990s |
| 22 | Everything Must Go | Rob Walker + Joshua Glenn | 2009 |

## Why routing matters

v1.0.0's 30 constraints are useful, but the same constraint library gets served to a user who's "blank page" and to a user who's "stuck on a 1-year project" — no differentiation.

v2.1's routing engine forces Stage → Method mapping. Examples:
- "想换思路" → Stage 4 Pivot → #22 Everything Must Go (not the default #1 Oblique Strategies)
- "选 A 还是 B" + "ship or not" → Override 7 终极决策 → #3 Pre-mortem + #18 Anti-Goal (gives verdict, not ideas)
- "差不多但差点意思" → Stage 5 Refinement → #13 Defamiliarization with 5-dimension Martian template (catches "attention blank spots")

When routing works (e.g. Decision → Pre-mortem), v2.1 produces 3-5x more useful output than v1's constraint library. When routing is roughly equivalent (e.g. Refinement → Defamiliarization), v2.1 still wins on anti-slop enforcement (forced 1+1+1 anchor diversity, non-decorative 怪诞 budget, no hallucinated references).

## Honest limitations (v2.1)

After 4 real-problem stress tests (v6.3 RPG visual rework, HTML5 commercial strategy, Hermes upgrade decision, vault refinement):

- **Trade-off: output is longer**. Routing trace + 5-dimension Martian + 3 ideas × multi-anchor + self-audit checklist = ~2-3x longer than v1's "3 ideas with a constraint header". Main公 trade-off is real: **可审计性 + 深度 ↔ 简洁性 + token cost**.
- **Override Rule 8 (default 怪倾向) needs Stage 6 exemption** — Decision stages shouldn't force 怪诞 ideas (already implemented, but worth noting).
- **Layer 5 (no hallucinated references) is hard to fully execute** in fast generation. Sub-agent admitted to one slip: "30 秒内丢 60% 记忆" was stated as fact when it's uncertain. The rule activated self-audit awareness but execution still depends on agent discipline.
- **Routing has a few ambiguous cases** (Stage 1 vs Stage 2, Stage 2 vs Stage 5). The v2.1 "看动词" rule resolved Override 2 vs Stage 5, but the other boundary cases still rely on agent judgment.

## Provenance

- v1.0.0 by SHL0MS — constraint approach inspired by [wttdotm.com/prompts.html](https://wttdotm.com/prompts.html)
- v2.0.0 by csx0574 — 4-step routing engine, 22 method library, 6-stage detection, 7 override rules, 4-layer anti-slop
- v2.0.1 by csx0574 — Stage 3 vs Stage 4 priority fix
- v2.1.0 by csx0574 — Six routing/anti-slop fixes after stress testing

## License

MIT (inherited from SHL0MS v1.0.0)
