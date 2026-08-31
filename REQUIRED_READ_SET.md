# PP-food-KV-001 Required Read Set

目标：**每个 B 任务只激活当前品类、当前字体和当前信息结构。禁止把 12 品类皮肤同时放进运行上下文。**

## B_JOB_CORE｜每个 B 任务必读

拿到当前任务 Stage A PASS 图并初步路由后，只固定加载：

```text
references/food-fidelity-bridge.md
references/information-gate.md
references/category-router.md
references/category-style-firewall.md
references/product-hero-priority.md
references/upper-bound-standard.md
```

这 6 个文件只负责：A→B 桥、文案事实边界、当前品类路由、防串台、产品优先级和上限边界。

## CURRENT_CATEGORY_LOAD｜只加载当前品类条目

从以下文件提取**当前 selected_visual_system 对应条目**，不要把完整 12 品类文本全部激活：

```text
references/category-visual-systems.md
references/typography-personality-map.md
references/typography-system.md
references/spatial-typography-engine.md
```

只允许：

```text
1 primary visual system
+ optional 1 weak auxiliary system
```

其他品类皮肤在当前任务中视为 INACTIVE。

## CONDITIONAL_LOAD｜有需要才读

### Brand Positioning
`references/brand-positioning-map.md`

### Layout / Information Density
`references/layout-bias-map.md`
`references/information-density.md`

### One Big Idea / Prompt / Perspective / Occlusion
只在当前 KV 确实需要时，从以下中选择必要文件：

```text
references/creative-director.md
references/prompt-builder.md
references/vanishing-point-director.md
references/occlusion-engine.md
```

### QR
只有真实 QR / 真实扫码目标时：
`references/qr-system.md`

### Category Ambiguity
仅当品类仍不确定时：

```text
references/domain-style-firewall.md
references/dish-semantic-router.md
```

## POST_GENERATION_CORE｜生成后按需

```text
references/category-qc.md
references/kv-qc.md
references/retry-policy.md
```

QC/Retry 文件不要提前作为视觉皮肤内容灌入 IMAGE_MODEL Prompt。

## Anti-Overload Rules

```text
LOAD_ALL_12_CATEGORY_SYSTEMS = FORBIDDEN
LOAD_ALL_TYPOGRAPHY_EXAMPLES = FORBIDDEN
LOAD_ALL_CONDITIONAL_REFERENCES = FORBIDDEN
TESTS_DURING_NORMAL_PRODUCTION = FORBIDDEN
PREVIOUS_JOB_SKIN_IMPORT = OFF
```

如果一个 reference 很长，只抽取当前类别/当前规则条目。

## B-Job Proof

调用 Stage B IMAGE_MODEL 前只需确认：

```text
CURRENT_STAGE_A_PASS_IMAGE = READY
SELECTED_VISUAL_SYSTEM = RESOLVED
TYPOGRAPHY_PERSONALITY = RESOLVED
HEADLINE_SPATIAL_MEDIUM = RESOLVED
SUBTITLE_SPATIAL_MEDIUM = RESOLVED
FULL_TEXT_SYSTEM_PLAN = CREATED
COPY_ALLOWLIST = CREATED
COPY_BLOCKLIST = CREATED
EXECUTION_CONTRACT = COMPACT_AND_CURRENT_JOB_ONLY
```

缺项 → B BLOCKED。

## Production Refresh

每个新 B 任务重新路由、重新选择当前 category/typography refs。上一任务加载过的品类文件不会自动延续为当前视觉皮肤。
