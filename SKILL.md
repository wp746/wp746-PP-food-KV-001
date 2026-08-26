---
name: PP-food-KV-001
description: Use when a user provides a real food photo and wants a professional restaurant, dessert, beverage, western-dining, bakery, packaged-food, or other food-category KV/campaign poster built from that exact product.
---

# PP-food-KV-001 V1.5

## Core Principle

> **Preserve the food → upgrade the photography → identify the food category → build a category-native KV → push that category to its true upper-bound without demoting or redesigning the product.**

The skill must never turn every food into the same poster language.

默认原则：

```text
DEFAULT_ASPECT_RATIO = 9:16
DEFAULT_KV_MODE = TRUE_UPPER_BOUND
```

除非用户明确要求“标准版 / 普通版 / 保守版 / 简单一点”，所有食品品类默认按**该品类自己的真正上限版**执行。

真正上限版不是修改食物本体；真正上限发生在：背景、空间、字体、主副标题层级、材质、光影、One Big Idea 与 Campaign 完成度。

---

# 0. FIRST-RUN SETUP GATE｜安装后先做交接

首次安装、首次加载，或当前运行环境是否就绪未知时，禁止直接进入生产。

必须先读取根目录 `HANDOFF.md`，进入：

```text
RUNTIME_STATE = SETUP_GATE
```

只确认缺失配置：

1. `VISION_MODEL`：识图、Food DNA、品类路由、信息判断与 QC；
2. `IMAGE_MODEL`：必须支持 reference image / image editing / image-to-image；
3. API Base URL；
4. API Credential 已配置到 Secret / Environment / Connection；
5. IMAGE_MODEL 能接收上传参考图；
6. Stage A 输出能继续作为 Stage B 输入；
7. VISION_MODEL 能读取用户原图与生成结果。

如果宿主默认模型没有视觉能力，不得猜测图片内容，必须显式调用 VISION_MODEL。

配置完成后：

```text
SETUP_GATE
→ READY_WAITING_FOR_START
→ 用户回复“启动”
→ PRODUCTION
```

---

# 1. Dependency｜依赖

本 Skill 是 **Stage B / KV Engine**。

标准链路：

```text
用户原始随手拍
→ PP-food-001 Stage A 高保真电影级商拍
→ Stage A 输出图
→ PP-food-KV-001 Stage B Category-Native KV
→ VISION_MODEL QC
```

Stage B 必须使用 Stage A 输出图作为参考图，不得重新回到原始随手拍激进生成。

---

# 2. Runtime Model Roles

## VISION_MODEL

负责：
- 读取用户上传图片；
- Food DNA / Fidelity Manifest；
- food_category / cuisine_family / brand_positioning / visual_mood；
- Category Visual Language Router；
- KV 信息门槛；
- Food Fidelity QC；
- Product Dominance QC；
- Typography / Spatial Medium QC；
- Category QC；
- Previous-Skin Contamination QC；
- 最终生成结果复检。

## IMAGE_MODEL

负责：
- Stage A：原始参考图 → 同一产品高保真电影级商拍；
- Stage B：Stage A 输出图 → 最终 KV；
- 按 Prompt 执行 Product Hero、品类原生视觉语言、空间字体与信息层级。

图片模型能参考图出图，不代表可以跳过前置视觉分析与后置 QC。

---

# 3. CURRENT JOB ISOLATION｜当前任务隔离

每一单都建立独立 `CURRENT_JOB_FACTS`。

当前任务只允许使用：

1. 当前用户上传图片的可见事实；
2. 当前用户明确提供的产品名、品牌名、标题、副标题和商业信息；
3. 当前任务 Stage A / Stage B 已验证的中间产物。

上一任务的品牌名、产品名、食材名、口味、卖点、地址、电话、Slogan、场景皮肤、字体皮肤默认全部失效。

除非用户明确说“沿用上一张 / 继续上一品牌 / 还是刚才那个产品”，否则：

```text
LEGACY_SEMANTIC_IMPORT = OFF
LEGACY_BRAND_IMPORT = OFF
LEGACY_FOOD_ENTITY_IMPORT = OFF
LEGACY_COPY_IMPORT = OFF
LEGACY_CATEGORY_SKIN_IMPORT = OFF
```

历史经验可以迁移**方法**，不能迁移当前任务的事实或视觉皮肤。

---

# 4. Entry Gate｜KV 信息门槛

正式 KV 必须满足：

```text
headline = required
subtitle = required
auxiliary_information_count >= 1
```

辅助信息可以来自真实的：品牌/店名、Slogan、核心食材、风味卖点、地址、电话、价格、营业信息、菜系、活动等。

禁止编造电话、地址、价格、品牌历史、认证、奖项、非遗、官方背书等硬事实。

“剩下的你自己安排”只授权视觉导演，不授权编造产品事实。

---

# 5. Stage A｜Food Fidelity First

进入任何 KV 设计前，必须先锁住产品真相。

目标：
- Food Identity >=95%
- Ingredient Geometry >=95%
- Vessel/Container Identity >=98%
- Plating Topology >=95%
- Physical Relationship Fidelity >=95%

不可牺牲层：

1. Food / Product Identity
2. Major Ingredient Identity
3. Ingredient Geometry
4. Vessel / Packaging Identity
5. Plating Topology
6. Physical Relationships
7. Sauce / Oil / Broth State
8. Visible Count / Arrangement Relationships

允许升级：灯光、背景、环境、景深、调色、摄影品质、材质表现。

禁止为了“真正上限”：换食材、加减食材、重摆盘、改变器皿/包装、重做产品造型。

Stage A IMAGE_MODEL Prompt 必须包含同等强度约束：

> **以用户上传参考图为唯一产品真相。严格锁定食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑、酱汁/红油/汤体状态和物理关系。不得为了更高级重做、替换、增减或重新摆放主体。创意主要发生在灯光、环境、背景、景深、调色和摄影品质层。**

Stage A 输出必须通过 Fidelity QC 才能进入 Stage B。

---

# 6. Stage B｜Category Visual Language Routing

VISION_MODEL 在 Stage B 前输出：

```text
food_category
cuisine_family
brand_positioning
visual_mood
category_confidence
selected_visual_system
```

从 `references/category-visual-systems.md` 选择一个主系统：

- CN_HOME_STYLE_SYSTEM
- SPICY_HOT_SYSTEM
- CLAYPOT_SOUP_SYSTEM
- NOODLE_RICE_NOODLE_SYSTEM
- BBQ_NIGHTMARKET_SYSTEM
- SEAFOOD_PREMIUM_SYSTEM
- DESSERT_CAKE_SYSTEM
- COFFEE_TEA_SYSTEM
- WESTERN_DINING_SYSTEM
- JAPANESE_KOREAN_SYSTEM
- BAKERY_BREAKFAST_SYSTEM
- RETAIL_PACKAGED_SYSTEM

默认：

```text
Category 70%
Brand Positioning 30%
```

最多一个主系统 + 一个弱辅助系统；禁止三套以上视觉皮肤混搭。

Category routing 只能改变视觉语言，绝不能改变 Food DNA。

读取：
- `references/category-router.md`
- `references/category-visual-systems.md`
- `references/category-style-firewall.md`
- `references/typography-personality-map.md`
- `references/layout-bias-map.md`
- `references/brand-positioning-map.md`

---

# 7. Category-Native Design Gate｜品类原生设计硬门槛

每个品类必须重新决定自己的：

- typography personality
- spatial headline language
- subtitle spatial medium
- layout bias
- color system
- material system
- environment / prop language
- information density
- negative style rules

只迁移方法，不迁移上一品类皮肤。

允许跨品类迁移：Hero Product、透视、空间字这一方法、前中后景、遮挡、统一光影、信息层级、负空间、One Big Idea。

禁止自动继承：字体皮肤、标题材质、门头、牌匾、橱窗、丝带、灯箱、圆章、配色、道具、卖点模块。

如果上一张成功 KV 只是“换产品”就能套到当前品类，直接判模板化失败。

---

# 8. Global Product Hero Priority

产品永远是第一视觉主角：

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / QR / UTILITY INFO
```

禁止：
- 为标题更大而缩小产品；
- 把产品推到远景或角落；
- 把产品当标题背景；
- 空间字遮挡关键食欲区 / 包装识别区；
- 第一视觉记忆只剩标题。

> **Typography builds the world around the product; it does not replace the product.**

读取 `references/product-hero-priority.md`。

---

# 9. TRUE UPPER-BOUND｜默认真正上限版

除非用户明确要求降档，所有美食品类默认：

```text
KV_MODE = TRUE_UPPER_BOUND
```

真正上限定义：

> **Food Fidelity 锁死 + 当前品类自己的视觉语言推到上限。**

不是：统一 3D 金字、统一深木、统一拱门、统一圆章、统一大标题。

上限主要推高：
- category-native background
- category-native spatial medium
- category-native typography
- headline materiality
- subtitle spatial hierarchy
- full text-system depth
- One Big Idea
- perspective / depth
- campaign lighting
- campaign finish

如果上限设计与产品忠实度冲突，降低背景/标题激进度，绝不能降低 Food Fidelity。

读取 `references/upper-bound-standard.md`。

---

# 10. Spatial Typography System｜主副标题必须共同进入空间

不能只把主标题做成立体字，然后把副标题、Slogan、卖点平贴。

完整文字系统必须根据当前品类同时设计：

## Headline
- 第二视觉锚点；
- 字体人格属于当前品类；
- 有合理的材质、厚度、透视、投影、悬挂或附着关系；
- 不靠“放大 + 描边”冒充上限。

## Subtitle
- 明显从属主标题；
- 不默认同平面、同横排、同响度；
- 使用当前品类原生介质，例如：吊牌、包装纸带、玻璃小字、菜单条、墙面小字、丝带、标签等；
- 可读且参与空间层级。

## Slogan / Selling Points
- 视觉响度继续下降；
- 介质与品类一致；
- 不强制圆章、不强制四宫格、不强制卡片。

## Brand / Utility
- 准确清晰；
- 服从品牌；
- 不抢产品和主标题。

烘焙示例：warm serif / clean sans / subtle handwritten accent + 晨光 / 橱窗立体字 / 包装纸字 / 烘焙吊牌 / 玻璃门店字；禁止中餐重黑金江湖毛笔门头。

读取 `references/typography-personality-map.md`。

---

# 11. Shared Perspective + Controlled Occlusion

空间字体必须建立统一主消失点或一致透视场。

标题、产品、桌面/展台、器皿、背景结构、蒸汽/冰气、道具与光影应处于同一空间逻辑。

允许轻微遮挡制造层次；关键汉字默认遮挡不超过约 8–12%，不得吞掉识别笔画。

---

# 12. Information Density + Truth

信息密度必须跟品类走：

- 中式家常 / 川湘 / 包装食品：中高；
- 汤煲 / 面食 / BBQ / 烘焙：中等；
- 高档海鲜 / 蛋糕 / 咖啡 / 西餐 / 日料：低到中等。

视觉可以激进，事实必须保守。

只有当前图与用户信息支持的文字才能进入正式 KV。

---

# 13. Category Style Firewall

禁止跨品类复制具体皮肤。

Mandatory examples：
- 蛋糕/甜点 → 中式饭馆大金字门头：FAIL
- 烘焙/早餐 → 重黑金江湖毛笔门头 / 爆炒火焰 / 密集餐馆圆章：FAIL
- 咖啡 → 家常菜四宫格卖点模板：FAIL
- 西餐 → 川湘红金毛笔门头：FAIL
- 高档海鲜 → 夜市粗糙招牌：FAIL
- 包装食品 → 重画包装 Logo/文字/结构：FAIL

上一任务皮肤无依据继承到当前任务：

```text
CATEGORY_SKIN_CONTAMINATION = TRUE
→ FAIL
```

读取 `references/category-style-firewall.md`。

---

# 14. Typography & Business Data Accuracy

用户提供的信息必须 100% 准确：
- 主标题
- 副标题
- 品牌 / 店名
- 地址
- 电话
- 价格
- 活动文字

禁止错字、漏字、随机汉字、擅自改写品牌。

QR：有真实二维码则锁定；无真实目标只预留 safe zone；禁止把 AI 随机矩阵当正式二维码。

---

# 15. Production Workflow

在 `PRODUCTION`：

```text
1. User uploads image + natural-language info
2. VISION_MODEL reads source image
3. Build CURRENT_JOB_FACTS and block legacy entities/skins
4. Check KV information gate
5. PP-food-001 builds Stage A fidelity route
6. IMAGE_MODEL receives original image + Stage A hard-lock prompt
7. Stage A cinematic commercial image
8. VISION_MODEL runs Fidelity QC
9. Resolve category / positioning / visual system
10. Build category-native One Big Idea
11. Build headline + subtitle + auxiliary full spatial text system
12. IMAGE_MODEL receives Stage A image + Stage B hero/category/typography prompt
13. Generate 9:16 KV
14. VISION_MODEL runs Food Fidelity + Product Dominance + Typography + Category + Contamination + Upper-Bound QC
15. Targeted retry if required
16. Deliver
```

---

# 16. Targeted Retry

不要随机整张重抽。

- Food DNA 漂移 → Stage A Reference Lock Retry
- 产品沦为背景 → Product Hero Retry
- 主标题太平 → Headline Spatial Retry
- 副标题/辅助文字平贴 → Full Text-System Spatial Retry
- 字体人格错配 → Typography Category Retry
- 品类串台 → Category Router Retry
- 上一品类皮肤污染 → Category Skin Isolation Retry
- 信息过稀/过密 → Information Density Retry
- 文字错误 → Typography Accuracy Retry
- 缺乏 Campaign 张力 → Upper-Bound Creative Retry

如果真正上限连续不稳定：先降低标题/背景/特效自由度，绝不能放松产品锁定。

---

# 17. Final QA

必须通过：

- Food Fidelity QC
- Product Dominance QC
- Typography Accuracy QC
- Spatial KV QC
- Category Visual Language QC
- Previous-Skin Contamination QC
- True Upper-Bound QC

阈值：

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
```

以下任一情况不允许标记 True Upper-Bound Ready：
- 为了上限改变 Food DNA / Packaging DNA；
- 只有主标题有设计，副标题/辅助文字仍平贴；
- 字体/背景/材质与品类不匹配；
- 上一品类成功皮肤无依据继承；
- 换成另一完全不同品类后海报仍几乎成立；
- 标题成为第一主角，产品退为摆设。

读取：
- `references/category-qc.md`
- `references/kv-qc.md`
- `references/upper-bound-standard.md`
- `tests/test-cases.md`

---

# Final Command

> **If runtime readiness is unknown: read HANDOFF.md first. Configure VISION_MODEL + IMAGE_MODEL + API connection, wait for “启动”, then produce.**
>
> **Lock the product truth first. Route the category from scratch. Transfer the upper-bound method, never the previous category skin. Build the entire text system in category-native space. Keep the product first.**
