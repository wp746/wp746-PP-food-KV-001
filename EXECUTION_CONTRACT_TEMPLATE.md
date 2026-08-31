# PP-food-KV-001 Compact Execution Contract

每个 B 任务在调用 Stage B IMAGE_MODEL 前，只编译**当前任务专属、短、无串台**的合同。

## Contract

```text
JOB_MODE = B
REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
OUTPUT = 9:16
KV_MODE = TRUE_UPPER_BOUND | USER_REQUESTED_LOWER_MODE

1) PRODUCT_LOCK
- product identity:
- major ingredients / materials:
- geometry / count / arrangement:
- vessel / packaging:
- plating / physical relationships:

2) CURRENT_CATEGORY
- food_category:
- cuisine_family:
- brand_positioning:
- visual_mood:
- selected_visual_system:
- optional weak auxiliary system:

3) COPY_TRUTH
- headline:
- subtitle:
- brand/store:
- slogan / selling points:
- price/address/phone/campaign facts:
- COPY_ALLOWLIST:
- COPY_BLOCKLIST:

4) SPATIAL_TEXT_SYSTEM
- headline personality / material / medium:
- subtitle subordinate medium:
- slogan / selling-point medium:
- brand / utility placement:
- shared perspective / vanishing logic:
- occlusion limit:

5) ONE_BIG_IDEA + CATEGORY_WORLD
- one campaign concept:
- background / materials / color:
- information density:
- negative style rules:

6) HARD_NEGATIVES
- no raw user photo as Stage B reference after A exists
- no previous-job image/facts/skin
- no product / package / vessel / plating redesign
- no major ingredient add/remove/replace
- no unsupported business facts
- no headline dominance over product
- no flat PPT subtitle/slogan system
- no cross-category skin contamination
- no random full regeneration after targeted failure
```

## Compilation Rule

Stage B IMAGE_MODEL Prompt 只编译为 6 个短块：

```text
A. Stage A Product Lock
B. Current Category Route
C. Current Copy Truth
D. Product Hero + Spatial Typography
E. One Big Idea + Category-Native World
F. Hard Negatives
```

禁止加入：
- tests 原文；
- 全 12 品类视觉系统；
- 上一任务案例；
- 仓库结构说明；
- Runtime Profile 说明；
- 重复多次的同义约束。

## Copy Rules

- 用户给产品名但没给 headline → 产品名可直接作为 headline。
- 用户没给 subtitle → 可生成非事实型传播副标题。
- 用户说“按默认文案来” → 只授权感官/传播软文案。
- 未确认电话、地址、价格、认证、奖项、历史、工艺、产地、食材等硬事实不得生成。
- 信息少 → 降低信息密度。

## Anti-Drift Rule

如果合同出现上一任务品牌/产品/地址/口味/字体皮肤/背景皮肤，且用户未明确要求沿用：

```text
CONTRACT_CONTAMINATION = TRUE
PRODUCTION_GATE = BLOCKED
```

## QC Targets

```text
Food Fidelity >=95
Vessel Fidelity >=98
Typography Accuracy =100
Category Visual Language >=90
Product Dominance = PASS
Full Text-System Spatiality = PASS
Category Skin Contamination = FALSE
Upper-Bound Readiness >=90
```

## Failure Mapping

```text
Food drift → return Stage A
Product demotion → Product Hero Retry
Flat text system → Spatial Typography Retry
Wrong category skin → Category Router Retry
Previous-job contamination → rebuild current contract
Typography error → Typography Accuracy Retry
Unsupported copy → remove unsupported copy
Weak Big Idea → Upper-Bound Creative Retry
```

最多 3 次定向重试；硬门槛无法满足时不假装 PASS。
