# PP-food-KV-001 Runtime Manifest

本文件是 Stage B 的 **P0 唯一运行真相源**。其他文件只负责解释、展开和举例，不得削弱以下规则。

## P0. Global Intent Router

```text
1. Explicit A → Stage A only
2. Explicit B → Stage A → Stage A QC → Stage A PASS → Stage B → Stage B QC
3. No A/B + obvious KV business info → B, but still Stage A first
4. Otherwise → A
```

明显 KV 商业信息包括：产品/菜名、店铺/品牌、主标题、副标题、地址、电话、价格、核心食材、卖点、新品/活动等。

```text
EXPLICIT_A_OVERRIDES_AUTO_B = TRUE
B_CAN_SKIP_STAGE_A = FALSE
DEFAULT_ASPECT_RATIO = 9:16
DEFAULT_KV_MODE = TRUE_UPPER_BOUND
```

## P1. Stage A Bridge

B 的唯一合法产品参考：

```text
STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
```

Stage A 至少满足：

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating Topology >=95
Physical Relationship >=95
```

Stage A 漂移 → 返回 Stage A 修正。禁止用 KV 排版掩盖产品漂移；禁止 Stage B 回退原始随手拍或上一任务图片。

## P2. Current Job Isolation

每个新任务创建独立 `CURRENT_JOB_FACTS`。

当前任务只允许使用：当前用户图的可见事实、当前用户明确提供的信息、当前任务已验证的 Stage A / Stage B 中间产物。

除非用户明确要求沿用：

```text
LEGACY_SEMANTIC_IMPORT = OFF
LEGACY_BRAND_IMPORT = OFF
LEGACY_FOOD_ENTITY_IMPORT = OFF
LEGACY_COPY_IMPORT = OFF
LEGACY_CATEGORY_SKIN_IMPORT = OFF
```

历史案例只能迁移方法，不能迁移事实或视觉皮肤。

## P3. Copy Truth / Information Gate

硬事实只能来自用户明确提供或当前图像能够可靠确认的内容。

正式执行 B 前默认检查：

```text
HEADLINE = required
SUBTITLE = required
AUXILIARY_INFORMATION_COUNT >= 1
```

如果缺失：**只询问最少缺失项**，不要未经授权自动把整套文案补完。

只有用户明确表达“按默认文案来 / 文案你来安排 / 剩下文字你来写”等，才允许：

```text
DEFAULT_COPY_AUTHORIZED = TRUE
```

此时可用产品名作为 headline，并生成非事实型 subtitle / slogan / 感官型卖点。

即使 `DEFAULT_COPY_AUTHORIZED = TRUE`，仍严禁自行编造：电话、地址、价格、营业时间、活动、认证、奖项、店史、原产地、官方背书、未确认食材、未确认口味、未确认制作工艺、医疗/健康功效等。

信息不足时降低密度，不靠编造填满版面。

每个 B 合同必须有：

```text
COPY_ALLOWLIST
COPY_BLOCKLIST
```

## P4. Category Re-Route Every Job

每个新食品重新输出：

```text
food_category
cuisine_family
brand_positioning
visual_mood
category_confidence
selected_visual_system
```

主系统从当前 12 类视觉系统中选择一个，最多加一个弱辅助系统。

```text
Category 70%
Brand Positioning 30%
```

品类路由只改变视觉语言，绝不能改变 Food DNA。

## P5. Method, Never Previous Skin

允许跨品类迁移：Hero Product、透视方法、空间字体方法、前中后景、受控遮挡、统一光影、信息层级、负空间、One Big Idea。

禁止自动继承上一任务：字体人格、标题材质、空间介质、门头/牌匾/橱窗/丝带/灯箱/圆章/拱门、配色、道具、卖点模块、背景皮肤。

如果只换产品海报仍几乎成立：

```text
CATEGORY_SKIN_CONTAMINATION = TRUE
RESULT = FAIL
```

## P6. Product Hero Priority

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / QR / UTILITY INFO
```

```text
PRODUCT_PRIORITY = 1
HEADLINE_PRIORITY = 2
```

标题可以强，但产品必须更强。禁止为了标题缩小、后退、遮挡或重做产品。

## P7. True Upper-Bound

```text
TRUE_UPPER_BOUND =
locked product truth
× category-native visual language
× spatial typography
× one big idea
× campaign finish
```

真正上限发生在：category-native background、typography personality/materiality、headline/subtitle spatial medium、full text-system depth、perspective/lighting/material integration、One Big Idea、Campaign Finish。

真正上限**不发生在**：重做食物、加减食材、换器皿、重摆盘、重画包装。

冲突时：

```text
REDUCE_DESIGN_AGGRESSION = TRUE
REDUCE_FOOD_FIDELITY = NEVER
```

## P8. Full Spatial Typography System

不能只有主标题立体、其他文字平贴。

必须整体设计：
- Headline：第二视觉锚点，使用当前品类字体人格和空间介质；
- Subtitle：明显从属，使用同品类合理介质，不默认同平面/同横排；
- Slogan / Selling Points：更低响度，仍属于同一品类视觉语法；
- Brand / Utility：准确、清楚、不抢产品。

所有文字必须共享一致透视/空间逻辑。关键汉字的受控遮挡不能破坏识别。

## P9. Typography / Business Accuracy

```text
TYPOGRAPHY_ACCURACY = 100%
```

用户提供的产品名、品牌、主副标题、地址、电话、价格、活动文字只要错一个字/数字/漏字/乱码 → FAIL。

无真实 QR 目标时只预留 safe zone，不把随机 AI 矩阵当正式二维码。

## P10. Final QC

```text
Food Fidelity >=95
Vessel Fidelity >=98
Typography Accuracy =100
Category Visual Language >=90
Typography-Category Match >=13/15
Spatial Language Match >=13/15
Full Text-System Spatiality >=9/10
KV Design Quality >=90
Product Dominance = PASS
CATEGORY_SKIN_CONTAMINATION = FALSE
Upper-Bound Readiness >=90
LEGACY_ENTITY_CONTAMINATION = 0
```

任意硬门槛不满足 → 不得标记 True Upper-Bound Ready。

## P11. Targeted Retry

不随机整张重抽。按失败类型：

```text
Food Drift → return to Stage A
Product Demotion → Product Hero Retry
Flat Headline / Subtitle → Spatial Typography Retry
Wrong Category Skin → Category Router Retry
Previous-Skin Contamination → rebuild current category system
Typography Error → Typography Accuracy Retry
Too Dense / Too Sparse → Information Density Retry
Weak Big Idea → Upper-Bound Creative Retry
```

最多 3 次定向重试。Food/文字硬门槛始终无法可靠满足 → 不假装 PASS。

## P12. Capability Evidence + Runtime Profile

静态能力与真实验证必须分开：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS / BLOCKED
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING / BLOCKED
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

工具 schema、宿主说明、连接存在只能证明 `DECLARED = PASS`。

完整双 Skill `VERIFIED = PASS` 必须有真实 A→B 端到端证据，或者存在与当前非秘密配置 fingerprint 匹配、scope = `FULL_A_TO_B` 的 verified Runtime Profile。

如果没有匹配 profile：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

允许 READY，但禁止声称“完整 A→B 已 smoke tested”。第一笔真实 B 任务兼任验证，不额外生成测试海报。

若首次任务只有 A，只能建立 `STAGE_A` scope evidence；不能把完整 B 链路标成 verified。

Verified profile 保存在宿主私有持久状态；fingerprint 不变时跨会话复用。Fingerprint 不得包含 API Key、Token、完整私有 URL 或用户凭据。

配置 identity 变化或任何真实链路失败 → profile 失效。

## P13. Runtime Context Discipline｜防过载/防串台

正常生产采用 Minimal Core，禁止把“为了安全”变成“全部都读”。

```text
FULL_REPO_DUMP = FORBIDDEN
TESTS_IN_NORMAL_RUNTIME = FORBIDDEN
ALL_12_CATEGORY_SKINS_ACTIVE = FORBIDDEN
PREVIOUS_JOB_SKIN_IMPORT = OFF
```

当前 B 任务只允许激活：

```text
1 primary selected_visual_system
+ optional 1 weak auxiliary system
+ current typography rules
+ current layout/information rules if needed
```

IMAGE_MODEL 只接收：

```text
CURRENT_JOB_STAGE_A_PASS_IMAGE
+ compact current B Execution Contract
+ compact current B Prompt
```

不得把 SOP、tests、全部 references、历史案例和旧任务摘要直接拼进 IMAGE_MODEL Prompt。

## P14. Fail Closed

以下任一无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

- Runtime Minimal Core；
- Pre-flight；
- `RUNTIME_CAPABILITIES_DECLARED != PASS`；
- Stage A dependency；
- 当前 Stage A PASS reference；
- VISION_MODEL / IMAGE_MODEL / Credential / 图片传递；
- Category Route；
- Copy Allowlist / Blocklist；
- 当前 B Execution Contract；
- 未解决规则冲突。

`RUNTIME_CAPABILITIES_VERIFIED = PENDING` 本身不代表配置缺失；它表示第一笔真实业务必须在最终交付前完成 live verification。

## P15. Repository Security Boundary

仓库不保存具体供应商名、私有聚合平台名、实际 API Base URL、API Key、Token、私有模型凭据或 Runtime Profile 的真实值。只保留通用能力要求；真实值由宿主 Secret / Environment / Connection / 私有持久状态提供。

## P16. Runtime State

```text
SETUP_GATE
→ READY_WAITING_FOR_START
→ user says 启动
→ PRODUCTION
```

READY 时必须准确报告：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

连接失效、fingerprint 不匹配、版本变化或上下文压缩后无法证明 P0 规则时，重新 Bootstrap / Pre-flight。
