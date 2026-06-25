# Override Rules (覆盖规则)

22 方法的默认路由可以被打断。覆盖规则 = 紧急通道，在某些信号出现时跳过默认路由直接到指定方法。

## 1. 显式偏好覆盖

用户说了具体的方法名或方法家族 → 直接用。

| 用户说 | 强制方法 |
|---|---|
| "TRIZ" / "矛盾" / "工程 trade-off" | #2 TRIZ |
| "Eno" / "侧向卡片" / "oblique" | #1 Oblique Strategies |
| "第一性" / "first principles" / "从头想" | #8 First Principles |
| "约束" / "Oulipo" / "限制" | #4 OuLiPo |
| "JTBD" / "用户雇佣" / "job to be done" | #9 Jobs-to-be-Done |
| "陌生人化" / "defamiliarize" / "陌生化" | #13 Defamiliarization |
| "故事骨架" / "Pixar pitch" / "story spine" | #14 Story Spine |
| "5 个为什么" / "5 whys" / "根因" | #15 5 Whys |
| "角色" / "如果我是 X" / "换角色" | #20 Role Storming |
| "时间穿越" / "未来人" / "speculative" | #21 Time Travel |

## 2. 情绪覆盖

用户表现出特定情绪 → 切换到对应方法。

| 信号 | 强制方法 |
|---|---|
| 焦虑 / 急躁 ("快"、"没时间"、"就要 1 个") | #16 Crazy 8s（设 8 分钟硬时限） |
| 完美主义 ("还不够好"、"再想想"、"再 polish") | #13 Defamiliarization |
| 失落 ("放弃了"、"没意义"、"我不行") | #22 Everything Must Go（清空-重启，给许可） |
| 愤怒 ("讨厌这个"、"太烂了"、"砸了") | #1 Oblique Strategies（用卡片降温） |
| 自满 ("差不多了"、"差不多能 ship") | #3 Pre-mortem（验尸找盲点） |

## 3. 高套路领域覆盖

话题属于"高套路黑名单"（见 anti-slop.md）→ 强制启用：
- 拒绝前 5 个（不是前 3）
- #5 Lateral Provocations 必用
- #10 Pataphysics 备用

## 4. 怪诞覆盖

用户说 "怪一点的" / "反常识" / "weird" / "unexpected" / "出圈" →
- 跳过 #6 SCAMPER（仍偏常规）
- 必用 #5 Lateral Provocations
- 备用 #10 Pataphysics
- 至少 1 个 idea 必须违反一个 best practice

## 5. 协作覆盖

用户在团队/客户场景 → 加 #19 Persona 100 的子集："如果这 5 个同事/客户来想会怎样"

## 6. 时间预算覆盖

用户给了明确时间：
- 5 分钟内 → #16 Crazy 8s（最便宜）
- 30 分钟内 → #6 SCAMPER（结构化但快）
- 1 小时+ → 可用 2-3 个方法叠加
- 多日 → 可用 #3 Pre-mortem 等深度方法

## 7. 终极决策覆盖

用户在 "ship 还是不 ship"、"换工作还是留下" 等重大决定 →
- 跳过所有发散方法
- 必用 #3 Pre-mortem + #18 Anti-Goal
- 不给 idea，给 verdict

## 8. 默认怪倾向覆盖 (v2.1 新增)

如果用户没说"怪"，但 routing 处于以下阶段，**默认强制 1/3 idea 必须有怪诞预算**：

- **Stage 3 Stuck** → 强制 1/3 idea 必须有怪诞预算（卡住场景常需 lateral move）
- **Stage 4 Pivot** → 强制 1/3 idea 必须违反 best practice（Pivot 本就是反常规）
- **Stage 5 Refinement** → 强制 1/3 idea 必须"反 best practice"（Defamiliarization 自带）

例外:
- Stage 1 Blank Page → 不强制（用户刚起步，先要方向）
- Stage 2 Expansion → 不强制（要的是 variants 数量）
- Stage 6 Decision → 不强制（决策类不需要怪诞）

怪诞预算审计规则见 anti-slop.md Layer 3 (v2.1 警告：装饰性怪诞不算怪诞)。

## 9. 推送触发安全检查 (v2.2 新增, 链式调 gh-push-safety-check)

如果用户原话含"推送"/"GitHub"/"开源"/"公开"/"PR"/"merge"等动词，**routing 流在 Step 4.5 之后追加 Step 4.6**：

- 自动调 `gh-push-safety-check` skill（`~/.hermes/skills/gh-push-safety-check/`）
- 默认 `--strict` 模式（WARN 也算 FAIL）
- 输出格式：在 Routing 表的"Method chosen"后加一行 `Safety pre-check: REQUIRED → invoke gh-push-safety-check`
- Safety 检查不通过 → idea 仍输出，但顶部加红色警告 ⚠️ `BLOCK PUSH: <count> critical findings`
- Safety 检查通过 → 输出末尾加 ✅ `Safe to push`

**触发词清单**:
- "推" + "GitHub"/"github"/"仓库"/"repo" → 触发
- "git push" / "gh repo create" / "gh pr create" → 触发
- "开源" / "公开" / "publish" / "release" → 触发
- "PR" / "merge" / "拉取请求" / "合并" → 触发
- "发" + "链接"/"URL"/"仓库地址" → 触发

**不触发**:
- 单纯 "推" = 推算法/推理/思考（不涉及代码） → 不触发
- "推到" + 主公/客户/团队（指通知/汇报） → 不触发
- 想法阶段、纯文档项目 → 不触发

**与其他 override 关系**:
- 推送触发是 routing 流后置步骤，**不影响 method 选择**
- 推送触发 + Override 7 (终极决策) 同时出现 → 决策给 verdict + safety-check 双流程

## 覆盖优先级

当多个覆盖冲突时：
1. 显式偏好 > 情绪 > 话题 > 怪诞 > 协作 > 时间 > 默认
2. 用户明示 > 推断
3. 显式说"用 X 方法" > 显式说"用 X 家族" > 隐含信号

## 覆盖 ≠ 跳过 anti-slop

任何覆盖方法生成 idea 后，仍要跑 anti-slop.md 的 Layer 1-3。覆盖决定**用什么方法**，不决定**是否过滤**。
