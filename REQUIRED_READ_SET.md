# PP-food-KV-001 Required Read Set

目标：**冷启动只加载不会偏向某个食品品类的核心规则；真正拿到当前图后，再强制加载当前品类/字体/空间规则。**

## COLD_START_ALWAYS_LOAD｜冷启动核心必读

```text
references/food-fidelity-bridge.md
references/information-gate.md
references/category-router.md
references/category-style-firewall.md
references/product-hero-priority.md
references/upper-bound-standard.md
references/kv-qc.md
references/retry-policy.md
tests/runtime-handoff-tests.md
tests/test-cases.md
```

不得用摘要或“已经知道”代替正文。

## COLD-START READ-PROOF

必须能回答：

1. `food-fidelity-bridge.md`：为什么 Stage B 只能使用当前任务 Stage A PASS 图？
2. `information-gate.md`：硬事实哪些不能编造？产品名如何充当 headline？信息不足时如何处理？
3. `category-router.md`：置信度如何影响 specific / family / conservative route？
4. `category-style-firewall.md`：什么叫“只迁移方法，不迁移上一品类皮肤”？
5. `product-hero-priority.md`：完整视觉优先级是什么？
6. `upper-bound-standard.md`：True Upper-Bound 的定义、Product Lock 和 >=90 门槛是什么？
7. `kv-qc.md`：Food / Typography / Design 的硬门槛是什么？
8. `retry-policy.md`：为什么必须定向重试且不能无限重抽？
9. 两份 tests：B 必经 A、9:16、Execution Contract、Fail Closed、Previous-Skin/Entity Contamination 的回归要求是什么？

答不准任何一项 → 重读对应文件。

## B_JOB_ALWAYS_LOAD｜每个 B 任务必读

拿到当前任务 Stage A PASS 图并完成初步 Category Route 后，每个 B 任务必须读取：

```text
references/category-qc.md
references/typography-personality-map.md
references/typography-system.md
references/spatial-typography-engine.md
references/category-visual-systems.md
```

规则：
- `category-visual-systems.md` 只把当前 `selected_visual_system` 和最多一个弱辅助系统带入 Contract；
- Typography 文件只提取当前品类需要的字体人格、主副标题空间介质和层级规则；
- 不把其他品类的具体视觉皮肤注入当前 Stage B Prompt。

### B-Job Proof

调用 Stage B IMAGE_MODEL 前必须确认：

```text
SELECTED_VISUAL_SYSTEM = RESOLVED
CATEGORY_QC_RULE = LOADED
TYPOGRAPHY_PERSONALITY = RESOLVED
HEADLINE_SPATIAL_MEDIUM = RESOLVED
SUBTITLE_SPATIAL_MEDIUM = RESOLVED
FULL_TEXT_SYSTEM_PLAN = CREATED
```

## CONDITIONAL_LOAD｜按当前任务加载

### Brand Positioning

```text
references/brand-positioning-map.md
```

Category 仍占主导，Brand Positioning 不得把食品跨到另一品类皮肤。

### Layout / Information Density

```text
references/layout-bias-map.md
references/information-density.md
```

### Creative / Prompt / Perspective

需要 One Big Idea、Prompt 编译、空间导演或遮挡时读取：

```text
references/creative-director.md
references/prompt-builder.md
references/vanishing-point-director.md
references/occlusion-engine.md
```

### QR

只有用户提供真实 QR 或真实目标时读取：

```text
references/qr-system.md
```

### Domain / Dish Semantics

品类仍有歧义时读取：

```text
references/domain-style-firewall.md
references/dish-semantic-router.md
```

## Production Refresh

每个 B 新任务至少刷新：

```text
RUNTIME_MANIFEST.md
food-fidelity-bridge.md
B_JOB_ALWAYS_LOAD
当前任务需要的 CONDITIONAL_LOAD
EXECUTION_CONTRACT_TEMPLATE.md
```

上下文压缩后若无法证明 Cold-Start Core 仍在活跃上下文，重新执行 BOOTSTRAP。