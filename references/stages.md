# Stage Detection (阶段判定)

22 方法不是平等的脑暴工具 — 每一个最适合解决**特定阶段**的特定问题。读懂用户当前在哪个阶段，是路由的第一步。

## 6 个阶段 (Stages)

### 1. 空想 (Blank Page) — 状态：完全空白
**信号词**：
- "我想做点什么"
- "没方向"
- "不知道从哪开始"
- "想开始但不知道做什么"
- "I want to build something" (没具体目标)

**最优方法**：
- #17 Mashup（跨域组合最容易产生起点）
- #19 Persona 100（找到具体的人）
- #21 Time Travel（拉远视角）
- #20 Role Storming（角色换头脑）

**避免**：TRIZ（没东西可解矛盾）、Pre-mortem（没东西可验尸）

### 2. 扩张 (Expansion) — 状态：1 个点子，要 10 个
**信号词**：
- "我有一个点子，能给我 10 个变体吗"
- "怎么扩展"
- "再想想"
- "更多方向"
- "give me variants"

**最优方法**：
- #6 SCAMPER（7 个算子对 1 个东西做变换）
- #17 Mashup（与不同域组合）
- #20 Role Storming（不同角色看同一物）

**避免**：Story Spine（要单一叙事）、Defamiliarization（要打磨已有物）

### 3. 卡壳 (Stuck) — 状态：做了但推不动
**信号词**：
- "卡住了"
- "推我一把"
- "试过了都不行"
- "灵感枯竭"
- "stuck / writer's block / creative block"

**最优方法**：
- #1 Oblique Strategies（Eno 卡片，通用解卡）
- #5 Lateral Provocations（PO 跳出常规）
- #13 Defamiliarization（用陌生化重看问题）
- #22 Everything Must Go（清空-重启）

**避免**：SCAMPER（需要现有物且在扩张）、Persona 100（要的是思路不是用户）

### 4. 求变 (Pivot) — 状态：当前路线放弃，要换
**信号词**：
- "这个方向不行"
- "要换思路"
- "重做"
- "放弃 v1"
- "pivot / restart"

**最优方法**：
- #22 Everything Must Go（清空-重启）
- #17 Mashup（彻底换 DNA）
- #21 Time Travel（拉远看问题）
- #18 Anti-Goal（先看清什么不行）

**避免**：SCAMPER（还在用旧的 DNA）

### 5. 打磨 (Refinement) — 状态：方向对，要更好
**信号词**：
- "差不多了但差点意思"
- "细节没到位"
- "再 polish 一下"
- "精修"
- "almost there but"

**最优方法**：
- #13 Defamiliarization（最经典打磨工具）
- #1 Oblique Strategies（细节级卡片）
- #14 Story Spine（叙事结构精修）
- #11 Pattern Language（抽象成可复用模式）

**避免**：Mashup（要换大方向）、Persona 100（要的是细节不是用户）

### 6. 决策 (Decision) — 状态：2-3 候选选 1 个
**信号词**：
- "我在 A 和 B 之间选"
- "两个方案哪个好"
- "要不要 commit"
- "ship or not"

**最优方法**：
- #3 Pre-mortem（验尸假设失败）
- #18 Anti-Goal（先想怎么失败）
- #15 5 Whys（挖根因）

**避免**：Brainstorming 类（要收敛不是发散）、SCAMPER

## 阶段判定流程

1. 读用户原话
2. 匹配信号词
3. 如果有歧义（如"我想做 X 但写不出来"）→ 阶段 5（打磨）优先
5. 如果阶段是 1+2+3+4+5+6 的混合（如"想重新思考整个方向"）→ 优先级：**4 > 3 > 1 > 5 > 2 > 6**（Pivot > Stuck > Blank > Refine > Expand > Decide — 想换 > 卡住 > 没方向，因为有"想换"是带方向的，比单纯"卡住"信息量大）
6. 不确定时默认走 **阶段 1 (空想)**，因为最通用
7. **重要修正 (v2.0.1)**: "卡住了 想换思路" 这种组合出现时，**Stage 4 Pivot 优先级 > Stage 3 Stuck**。原 v2.0 的 "3 > 1 > 4" 顺序是错的——把"想换方向"当成"单纯卡住"是 routing 的常见误判。改后优先级: **Pivot > Stuck > Blank**

## 阶段间的跳跃保护

不允许直接从 **阶段 1 (空想)** 跳到 **阶段 5 (打磨)** — 中间必须经过 **阶段 2 (扩张)**。打磨需要现有物。

不允许直接从 **阶段 6 (决策)** 跳到 **阶段 1 (空想)** — 决策需要候选。

如果用户这么做了（如"我想做 X 怎么 polish 一下"但 X 还不存在）→ 强制回到合适的中间阶段，告诉用户。

## Stage vs Override 冲突解决 (v2.1 新增)

overrides.md 给 Override (情绪/显式/时间) 高优先级，stages.md 给 Stage 优先，两者没说哪个赢。这是 routing 引擎的实际 bug (子代理在 Problem 3 vault 案例中暴露)。

**核心规则：看动词，不看形容词。**

| 用户原话模式 | 判定 | 走 |
|---|---|---|
| "扔掉" "放弃" "没意义" "我不行" "重新来" | 真失落 (Override 2) | #22 Everything Must Go |
| "差一点" "不到位" "用不上" "是 X 不是 Y" "像图书馆" "差点意思" | 失落表达 + Refinement 意图 | 走 Stage 5 (Defamiliarization) |
| "选 A 还是 B" "ship 不 ship" "升不升" "换不换" | 终极决策 (Override 7) | #3 Pre-mortem + #18 Anti-Goal |
| "卡住了 想换思路" | Stage 3+4 混合 | Pivot 优先 (v2.0.1 修正) |
| "搞个新东西" 后面说 "但我已经在做 X" | Stage 1+5 混合 | Stage 1 优先 (空想) — X 还没成形 |

**冲突判断的 3 个启发式**：
1. **动词比形容词优先**: "扔掉" (动词) > "不好" (形容词)
2. **"不是 X 是 Y" 句式 = Refinement 意图**: 情绪是次要,方向是主
3. **判定不确定时 → 走更轻的阶段**: Refinement (Stage 5) > Pivot (Stage 4) > Reset (Override 2 → #22 EMuG)。先 polish,实在不行再扔。

**默认规则**: Stage 5 > Override 2 (除非用户明确说"扔掉" / "放弃" / "从零")。
