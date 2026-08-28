# PP-food-KV-001 Required Read Set

本文件强制区分“冷启动必读”与“当前任务按需读”，防止选择性漏读，也避免每次把整仓库塞入上下文。

## ALWAYS_LOAD｜冷启动必须完整读取

```text
references/food-fidelity-bridge.md
references/information-gate.md
references/category-router.md
references/category-style-firewall.md
references/category-qc.md
references/product-hero-priority.md
references/typography-personality-map.md
references/typography-system.md
references/spatial-typography-engine.md
references/upper-bound-standard.md
references/kv-qc.md
references/retry-policy.md
tests/runtime-handoff-tests.md
tests/test-cases.md
```

不得以摘要或“已经知道大概意思”代替正文。

## READ-PROOF CHECKPOINTS

读完 ALWAYS_LOAD 后必须能回答：

1. `food-fidelity-bridge.md`：为什么 Stage B 只能使用当前任务 Stage A PASS 图？
2. `information-gate.md`：哪些商业硬事实不能编造？产品名如何充当 headline？信息不足时应该降低密度还是补事实？
3. `category-router.md`：如何按置信度和 Category/Brand 权重路由？
4. `category-style-firewall.md`：什么叫“只迁移方法，不迁移上一品类皮肤”？哪些元素属于皮肤污染？
5. `category-qc.md`：如何判断 Category Visual Language 和跨品类串台？
6. `product-hero-priority.md`：视觉优先级完整顺序是什么？
7. `typography-personality-map.md`：字体人格为什么必须由当前品类/品牌决定，而不能默认金色毛笔？
8. `typography-system.md` + `spatial-typography-engine.md`：为什么主标题、副标题、Slogan、辅助信息必须形成完整空间文字系统？
9. `upper-bound-standard.md`：True Upper-Bound 的公式、硬失败条件和 >=90 门槛是什么？
10. `kv-qc.md`：Food / Typography / KV Design 的硬门槛是什么？
11. `retry-policy.md`：为什么必须定向重试且有重试上限？
12. 两份 tests：B 必经 A、9:16、Execution Contract、Fail Closed、Previous-Skin Contamination 的回归要求是什么？

任何一项无法准确回答 → 重读对应文件。

## CONDITIONAL_LOAD｜当前任务按需读取

### 每个 B 任务必选一个 Category Visual System

识别当前品类后，必须读取：

```text
references/category-visual-systems.md
```

只把当前 `selected_visual_system` 及必要的一个弱辅助系统带入当前任务 Contract；不要把 12 套视觉皮肤一起混进 Prompt。

### Brand Positioning

需要品牌语气修正时读取：

```text
references/brand-positioning-map.md
```

Category 仍占主导，不得让品牌定位把食品跨到另一品类皮肤。

### Layout / Information Density

需要版式与信息密度决策时读取：

```text
references/layout-bias-map.md
references/information-density.md
```

### Creative Direction / Prompt Compilation

需要 One Big Idea、空间导演或最终 Prompt 结构时读取：

```text
references/creative-director.md
references/prompt-builder.md
references/vanishing-point-director.md
references/occlusion-engine.md
```

### QR

只有用户提供真实 QR 或真实目标需求时读取：

```text
references/qr-system.md
```

### Domain / Dish Semantics

品类或风格边界仍有歧义时读取：

```text
references/domain-style-firewall.md
references/dish-semantic-router.md
```

## Production Rule

冷启动 ALWAYS_LOAD 完成后，每个 B 新任务至少刷新：

```text
RUNTIME_MANIFEST.md
food-fidelity-bridge.md
当前 selected category visual system
当前任务需要的 typography/category 条目
EXECUTION_CONTRACT_TEMPLATE.md
```

上下文压缩后如果无法证明 ALWAYS_LOAD 的 P0 检查点仍在活跃上下文，重新执行 BOOTSTRAP。