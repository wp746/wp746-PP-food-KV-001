# PP-food-KV-001 Pre-Flight Checklist

目标：只拦真正会导致 B 漂移/串台/失败的问题，不让门禁本身成为上下文负担。

## 1. Bootstrap Status

必须：

```text
VERSION_READ = PASS
RUNTIME_MANIFEST_READ = PASS
SKILL_READ = PASS
SOP_B_READ = PASS
HANDOFF_READ = PASS
REQUIRED_READ_SET_READ = PASS
EXECUTION_CONTRACT_TEMPLATE_READ = PASS
```

`tests/*` 不属于正常生产 pre-flight。

## 2. Runtime Capability Gate

必须静态确认：

```text
VISION_MODEL_CAN_READ_ORIGINAL = PASS
VISION_MODEL_CAN_READ_STAGE_A = PASS
VISION_MODEL_CAN_READ_STAGE_B = PASS
IMAGE_MODEL_REFERENCE_EDIT = PASS
PP_FOOD_STAGE_A_DEPENDENCY = PASS
STAGE_A_OUTPUT_TO_STAGE_B = PASS
CREDENTIAL = PASS
```

任一 UNKNOWN/MISSING → `PRODUCTION_GATE = BLOCKED`。

静态能力只证明 `DECLARED = PASS`；没有真实 A→B 证据时保持 `VERIFIED = PENDING`。

## 3. Current B Job Gate

必须：

```text
CURRENT_JOB_FACTS = CREATED
INTENT = B
CURRENT_STAGE_A_QC = PASS
STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
B_JOB_CORE = LOADED
CURRENT_CATEGORY_ONLY = TRUE
SELECTED_VISUAL_SYSTEM = RESOLVED
TYPOGRAPHY_PERSONALITY = RESOLVED
FULL_TEXT_SYSTEM_PLAN = CREATED
COPY_ALLOWLIST = CREATED
COPY_BLOCKLIST = CREATED
EXECUTION_CONTRACT = COMPACT_AND_COMPLETE
```

## 4. Copy Gate

若用户未提供完整海报文案：

- 产品名可作为 headline；
- subtitle/slogan 可生成非事实型传播文案；
- 用户说“按默认文案来”仍只授权软文案；
- 未确认电话、地址、价格、认证、奖项、工艺、产地、食材等不得编造；
- 信息不足时降低密度，不靠编造填满。

## 5. Prompt Sanity Gate

Stage B IMAGE_MODEL Prompt 必须：

```text
REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
PRODUCT_PRIORITY = 1
HEADLINE_PRIORITY = 2
CURRENT_JOB_ONLY = TRUE
PREVIOUS_JOB_SKIN = NONE
ALL_12_CATEGORY_SKINS = NONE
FULL_REPO_DUMP = FALSE
TEST_CONTENT = NONE
```

当前 Prompt 只保留当前品类、当前文案、当前空间系统和当前产品锁定。

## 6. Post-Generation Gate

至少检查：

```text
Food Fidelity >=95
Vessel Fidelity >=98
Typography Accuracy =100
Category Visual Language >=90
Full Text-System Spatiality = PASS
Product Dominance = PASS
Category Skin Contamination = FALSE
Upper-Bound Readiness >=90
Legacy Entity Contamination = 0
```

失败 → 只加载对应 QC/Retry reference → 定向重试。

## 7. READY / First Live Verification

Minimal Core + declared capability PASS：

```text
RUNTIME_STATE = READY_WAITING_FOR_START
```

用户“启动”后进入 PRODUCTION。

首次完整 A→B 尚未验证时，第一笔真实 B 业务兼任验证，不额外生成 smoke-test 海报。

## 8. Recovery

VISION / IMAGE reference-edit / Stage A dependency / Credential / A→B pass-through / output readback 失败 → 回 `SETUP_GATE`，只修具体缺失项。
