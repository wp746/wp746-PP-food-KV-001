---
name: PP-food-KV-001
description: Use when a real food photo should become a category-native professional KV/campaign poster while preserving the exact product and routing typography, background, materials and layout to the current food category.
version: 1.6.0
---

# PP-food-KV-001 V1.6.0

## Core Principle

> **Preserve the food → complete Stage A → identify the category → build a category-native KV → push that category to its true upper-bound without redesigning the product.**

默认：

```text
DEFAULT_ASPECT_RATIO = 9:16
DEFAULT_KV_MODE = TRUE_UPPER_BOUND
```

真正上限版的“上限”发生在背景、空间、主副标题、字体材质、透视、光影、One Big Idea 和 Campaign 完成度；**不发生在重做食物本体。**

---

# 0. Runtime Gate

首次加载或运行状态未知时读取 `HANDOFF.md`，进入 `SETUP_GATE`。仓库只保存通用能力约定；**不得写入具体供应商名、模型服务 URL、API Key 或聚合平台配置。** 凭据由宿主 Secret / Environment / Connection 管理。

进入 `PRODUCTION` 后，不重复询问配置，除非连接失效。

---

# 1. A / B Intent Router｜用户入口规则

优先级：

```text
1. 用户明确说 A → 只执行 PP-food-001 Stage A 商拍
2. 用户明确说 B → 进入 B，但必须先完整执行 Stage A
3. 未说 A/B，但出现明显 KV 商业信息 → 自动判定 B
4. 其他情况 → 默认 A
```

商业信息包括：产品/菜品名、店铺/品牌、主标题、副标题、地址、电话、价格、核心食材、卖点、新品/活动信息等。

**显式 A 优先于自动 B。**

任何 B 都必须：

```text
原始图
→ Stage A
→ Stage A Fidelity QC
→ Stage A PASS 图
→ Stage B
```

Stage B 的参考图必须是当前任务的 Stage A PASS 图，不得回退原始随手拍。

---

# 2. Current Job Isolation｜当前任务隔离

每一单建立独立 `CURRENT_JOB_FACTS`。

当前任务只允许使用：
- 当前上传图片可见事实；
- 当前用户明确提供的商业信息；
- 当前任务已经验证的 Stage A / Stage B 中间产物。

上一任务的品牌、产品名、食材、口味、地址、电话、Slogan、标题皮肤、场景皮肤、配色和道具默认全部失效，除非用户明确要求沿用。

```text
LEGACY_SEMANTIC_IMPORT = OFF
LEGACY_BRAND_IMPORT = OFF
LEGACY_FOOD_ENTITY_IMPORT = OFF
LEGACY_COPY_IMPORT = OFF
LEGACY_CATEGORY_SKIN_IMPORT = OFF
```

历史案例只能迁移**设计方法**，不能迁移当前任务事实或视觉皮肤。

---

# 3. Runtime Roles

## VISION_MODEL
负责：
- 读取原图与 Stage A / Stage B 结果；
- Food DNA / Fidelity Manifest；
- food_category / cuisine_family / brand_positioning / visual_mood；
- Category Router；
- Product Dominance QC；
- Typography / Spatial Medium QC；
- Category QC；
- Previous-Skin Contamination QC；
- 最终 KV QC。

## IMAGE_MODEL
负责：
- Stage A：原图 → 高保真商业摄影；
- Stage B：Stage A PASS 图 → KV；
- 执行 Product Hero、品类原生视觉语言、空间字体、材质、透视与信息层级。

图片模型能参考图出图，不代表可以跳过视觉分析或 QC。

---

# 4. Stage A Fidelity Gate｜B 必经 A

Stage B 之前必须满足：

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating Topology >=95
Physical Relationship >=95
```

必须锁定：
- 食物/产品身份；
- 主要食材与几何；
- 器皿/包装；
- 摆盘拓扑；
- 酱汁/红油/汤体/奶油/冰块等可见状态；
- 主要数量与排列关系；
- 手持、餐具、托盘等物理关系。

如果 Stage A 漂移，禁止用 Stage B 排版掩盖；必须先回 Stage A 修正。

读取 `references/food-fidelity-bridge.md`。

---

# 5. KV Information + Copy Truth

B 一旦触发，不要求用户理解内部信息门槛。

优先使用用户明确提供的：
- 产品名 / 菜名；
- 店铺 / 品牌；
- 主标题 / 副标题；
- 地址 / 电话 / 价格；
- 核心食材 / 卖点；
- 新品 / 活动信息。

若用户未给主标题但给了产品名，默认可使用**产品名本身作为主标题**。

副标题 / Slogan 可以创作，但只能：
- 基于用户已给事实；或
- 使用不冒充产品事实的情绪/传播文案。

禁止编造：电话、地址、价格、认证、奖项、品牌历史、原产地、官方背书、具体食材、具体口味、制作工艺等未经用户或图像证据支持的硬事实。

“剩下的你自己安排”只授权视觉设计和安全文案，不授权编造产品事实。

读取 `references/information-gate.md`。

---

# 6. Category Router｜先识别品类再设计

Stage B 前输出：

```text
food_category
cuisine_family
brand_positioning
visual_mood
category_confidence
selected_visual_system
```

主视觉系统从以下选择一个：

```text
CN_HOME_STYLE_SYSTEM
SPICY_HOT_SYSTEM
CLAYPOT_SOUP_SYSTEM
NOODLE_RICE_NOODLE_SYSTEM
BBQ_NIGHTMARKET_SYSTEM
SEAFOOD_PREMIUM_SYSTEM
DESSERT_CAKE_SYSTEM
COFFEE_TEA_SYSTEM
WESTERN_DINING_SYSTEM
JAPANESE_KOREAN_SYSTEM
BAKERY_BREAKFAST_SYSTEM
RETAIL_PACKAGED_SYSTEM
```

默认：

```text
Category 70%
Brand Positioning 30%
```

最多一个主系统 + 一个弱辅助系统。Category routing 只改变视觉语言，绝不能改变 Food DNA。

读取：
- `references/category-router.md`
- `references/category-visual-systems.md`
- `references/brand-positioning-map.md`

---

# 7. Category-Native Design Firewall｜只迁移方法，不迁移皮肤

每个新任务必须重新决定：
- typography personality；
- headline spatial medium；
- subtitle spatial medium；
- layout bias；
- color system；
- material system；
- background / prop language；
- information density；
- negative style rules。

允许跨品类迁移的方法：Hero Product、透视、空间字、前中后景、受控遮挡、统一光影、信息层级、负空间、One Big Idea。

禁止自动继承上一任务的：金字、毛笔、门头、牌匾、橱窗、丝带、灯箱、圆章、拱门、配色、道具、卖点卡和背景模板。

Anti-template Test：如果把当前食品替换成完全不同品类，海报仍几乎成立 → FAIL。

读取：
- `references/category-style-firewall.md`
- `references/domain-style-firewall.md`
- `references/typography-personality-map.md`
- `references/layout-bias-map.md`

---

# 8. Product Hero Priority

统一视觉优先级：

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / QR / UTILITY INFO
```

> **标题可以强，但产品必须更强。**

禁止：
- 为标题放大而缩小产品；
- 产品退到远景/角落；
- 产品成为标题背景；
- 空间字遮挡关键食欲区 / 包装识别区；
- 第一视觉记忆只有标题。

Stage B Prompt 必须包含同等强度约束：

> **以 Stage A 商拍图中的产品为 Hero Product。严格保持 Food/Packaging DNA。标题可以有厚度、透视、材质和空间张力，但不得缩小、后退、遮挡或重做产品。调用当前食品品类自己的字体、空间、色彩、材质、背景和信息密度系统。**

读取 `references/product-hero-priority.md`。

---

# 9. TRUE UPPER_BOUND｜所有品类默认真正上限版

除非用户明确说“标准版 / 普通版 / 保守版 / 简单一点”，默认：

```text
KV_MODE = TRUE_UPPER_BOUND
```

真正上限 = **Food Fidelity 锁死 + 当前品类自己的视觉语言推到上限**。

上限主要发生在：
- category-native background；
- category-native typography；
- headline materiality；
- subtitle spatial hierarchy；
- full text-system depth；
- perspective / depth；
- One Big Idea；
- campaign lighting；
- campaign finish。

如果上限设计与产品忠实度冲突，降低背景/标题激进度，绝不能降低 Food Fidelity。

读取 `references/upper-bound-standard.md`。

---

# 10. Full Spatial Typography System｜主副标题和辅助字共同进入空间

不能只把主标题做成立体字，然后副标题、Slogan、卖点全部平贴。

## Headline
- 第二视觉锚点；
- 字体人格属于当前品类；
- 有该品类合理的材质、厚度、透视、投影、悬挂或附着关系；
- 不靠“放大 + 描边”冒充上限。

## Subtitle
- 明显从属主标题；
- 不默认同一平面 / 同一横排 / 同一响度；
- 使用该品类合理介质：吊牌、包装纸带、玻璃小字、菜单条、墙面小字、丝带、标签、窗面字等；
- 可读且参与空间层级。

## Slogan / Selling Points
- 视觉响度继续下降；
- 介质与品类一致；
- 不强制圆章、四宫格或卡片。

## Brand / Utility
- 100% 准确；
- 服务品牌识别；
- 不抢产品与主标题。

空间字体必须共享一个主消失点或一致透视场；关键汉字受控遮挡默认不超过约 8–12%。

读取：
- `references/spatial-typography-engine.md`
- `references/typography-system.md`
- `references/typography-personality-map.md`
- `references/vanishing-point-director.md`
- `references/occlusion-engine.md`

---

# 11. Category-Specific Upper-Bound Examples

这些只是路由示意，不能变成固定模板：

- 中式家常：厚中文展示字 / 牌匾或门头空间 / 暖材质 / 烟火感；
- 面食粉类：纵向节奏 / 拉伸与上升动线 / 主食力量；
- 烧烤夜市：悬挂招牌 / 灯箱 / 炭火烟气；
- 海鲜宴席：refined Song / 现代黑体 / 克制金属与留白；
- 蛋糕甜点：editorial serif / 奶油曲面 / 玻璃 / 丝带；
- 咖啡茶饮：现代无衬线 / 玻璃字 / 窗面字 / Lifestyle 留白；
- 西餐：high-contrast serif / 石材 / 银器 / Fine Dining；
- 日韩：极简窄体 / 木格 / 纸面 / 几何秩序；
- 烘焙早餐：warm serif / friendly sans / subtle handwritten / 晨光 / 橱窗 / 包装纸 / 吊牌；
- 包装食品：Hero Packshot / 品牌展示体 / 展台或货架，包装 DNA 100% 锁定。

具体规则以 `references/category-visual-systems.md` 为准。

---

# 12. Information Density + Typography Accuracy

密度必须按品类变化，不强迫所有品类使用相同卖点模块。

用户提供的主标题、副标题、品牌、地址、电话、价格、活动文字必须 **100% 准确**。发现错字、漏字、乱码或数字错误 → FAIL。

有真实 QR 则锁定；无真实目标只预留 safe zone，不把随机 AI 矩阵当二维码。

读取：
- `references/information-density.md`
- `references/qr-system.md`

---

# 13. Final QC

必须通过：

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

Mandatory FAIL：
- Food DNA 漂移；
- 标题成为第一主角；
- 主标题有空间感但副标题/辅助字平贴；
- 当前品类使用上一任务视觉皮肤；
- 商业事实被编造；
- 把所有品类做成同一 3D 金字 / 同一深木 / 同一圆章模板。

读取：
- `references/category-qc.md`
- `references/kv-qc.md`
- `references/upper-bound-standard.md`

---

# 14. Targeted Retry

失败按类型修正，不随机整张重抽：

```text
Food Drift → 返回 Stage A
Product Demotion → Product Hero Retry
Flat Headline / Subtitle → Spatial Typography Retry
Wrong Category Skin → Category Router Retry
Previous-Skin Contamination → rebuild current category system
Typography Error → Typography Accuracy Retry
Too Dense / Too Sparse → Information Density Retry
Weak Campaign Idea → Upper-Bound Creative Retry
```

最多 3 次定向重试；若 Food / Typography 无法可靠达到硬门槛，不得假装 PASS。

读取 `references/retry-policy.md`。

---

# 15. Production Workflow

```text
User image + natural language
→ A/B Intent Router
→ Stage A (always required for B)
→ Stage A QC
→ CURRENT_JOB_FACTS isolation
→ Category Router
→ One Big Idea
→ category-native background + full spatial typography system
→ IMAGE_MODEL(Stage A PASS image + Stage B hard lock)
→ Product / Typography / Category / Upper-Bound QC
→ targeted retry if needed
→ deliver
```

用户只需说 A、B 或用大白话描述需求；不要暴露内部 JSON、Prompt、路由名或评分表。

---

# Final Rule

> **默认 A。出现明确 B 或 KV 商业信息时进入 B，但 B 必须先完成 A。所有输出默认 9:16；所有品类默认使用该品类自己的真正上限版。产品事实和 Food DNA 永远高于设计张力。**
