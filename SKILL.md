---
name: PP-food-KV-001
description: Use when a user provides a real food photo and wants a professional restaurant, dessert, beverage, western-dining, bakery, packaged-food, or other food-category KV/campaign poster built from that exact product.
---

# PP-food-KV-001 V1.4

## Core Principle

> **Preserve the food → upgrade the photography → identify the food category → build a category-native KV → push that category to its true upper-bound without demoting the product.**

The skill must never turn every food into the same poster language.

---

# 0. FIRST-RUN SETUP GATE｜安装后先做交接

首次安装、首次加载，或当前运行环境是否就绪未知时，**禁止直接进入生产**。

必须先读取根目录 `HANDOFF.md`，进入：

```text
RUNTIME_STATE = SETUP_GATE
```

只向用户确认缺失配置：

1. `VISION_MODEL`：负责识图、Food DNA、品类路由、信息判断和生成后 QC；
2. `IMAGE_MODEL`：必须支持 reference image / image editing / image-to-image，用于 Stage A 商拍与 Stage B KV；
3. `API_BASE_URL`：聚合平台或模型服务地址；
4. API Key/Credential 已配置到 Secret / Environment / Connection；
5. IMAGE_MODEL 能接收上传参考图；
6. Stage A 输出能继续作为 Stage B 输入；
7. VISION_MODEL 能读取用户原图与生成结果。

如果宿主默认模型没有视觉能力，**不得自行猜测上传图片内容**。必须显式调用配置好的 `VISION_MODEL`。

推荐环境变量：

```text
PP_FOOD_API_BASE_URL
PP_FOOD_API_KEY
PP_FOOD_VISION_MODEL
PP_FOOD_IMAGE_MODEL
```

如果平台有自己的 Secret/Connection 系统，可以映射，不强制变量名。

配置完成后必须告诉用户：

> **PP Food 双 Skill 运行环境已准备就绪。回复“启动”进入生产模式。**

状态：

```text
SETUP_GATE
→ READY_WAITING_FOR_START
→ 用户回复“启动”
→ PRODUCTION
```

进入 `PRODUCTION` 后，用户只需自然语言交流；不要重复询问模型配置，除非连接失效。

---

# 1. Dependency｜依赖

本 Skill 是 **Stage B / KV Engine**。

推荐同时安装 `PP-food-001`，标准链路：

```text
用户原始随手拍
→ PP-food-001：Stage A 高保真电影级商拍
→ Stage A 输出图
→ PP-food-KV-001：Stage B KV
→ VISION_MODEL QC
```

如果 `PP-food-001` 未安装，应提醒用户安装/挂载。若用户明确要求降级单独运行，可以继续，但应说明高保真稳定性会下降。

---

# 2. Runtime Model Roles

## VISION_MODEL

负责：
- 读取用户上传图片；
- Food DNA / Fidelity Manifest；
- `food_category` / `cuisine_family` / `scene_type` / `brand_positioning`；
- Category Visual Language Router；
- KV 信息门槛判断；
- Food Fidelity QC；
- Product Dominance QC；
- Category QC；
- 生成结果的视觉复检。

## IMAGE_MODEL

负责：
- Stage A：接收原始参考图，生成同一产品的高保真电影级商拍；
- Stage B：接收 Stage A 输出图，生成最终 KV；
- 按 Prompt 约束执行空间字体、品类视觉语言和产品 Hero 规则。

**图片模型能参考图出图，不代表可以跳过前置视觉分析与后置 QC。**

---

# 3. Entry Gate｜KV 信息门槛

正式 KV 设计必须满足：

```text
headline = required
subtitle = required
auxiliary_information_count >= 1
```

N 可包括：
- 店名 / 品牌名
- Slogan
- 核心食材
- 风味卖点
- 地址
- 电话
- 价格
- 营业信息
- 菜系
- 活动信息
- 其他真实商业信息

不足时只询问**最少缺失项**。

禁止编造：
- 电话
- 地址
- 价格
- 品牌历史
- 认证
- 奖项
- 非遗
- 每日现杀
- 官方背书

---

# 4. Stage A｜Food Fidelity First

在任何 KV 空间设计之前，必须先执行 `PP-food-001` 式高保真商拍。

目标：
- Food Identity >=95%
- Ingredient Geometry >=95%
- Vessel/Container Identity >=98%
- Plating Topology >=95%
- Physical Relationship Fidelity >=95%

Stage A 先让原始随手拍成为：

> **同一份真实产品的电影工作室级商业摄影图——世界级美食英雄定妆照。**

允许升级：灯光、背景、环境、景深、调色、材质表现。

Stage A 背景必须同时满足 PP-food-001 的两份硬规则：

- `PP-food-001/references/semantic-background-rules.md`：环境语义属于这道菜；
- `PP-food-001/references/hero-shot-mandate.md`：环境是高级材质舞台（食材DNA第一原则 + 四层景深 + 核心作料围铺虚化 + 食欲感渲染 + 英雄定妆照调性），禁止平背景与真实场所结构。

这直接服务 Stage B：英雄位构图 + 上方干净负空间是 KV 排版的空间基础。

禁止为了高级感：换食材、换器皿、重摆盘、改变包装、增加不存在的高级配料。

## Stage A IMAGE_MODEL Prompt Hard Lock

调用 IMAGE_MODEL 时，提示词前部必须包含同等强度约束：

> **以用户上传参考图为唯一产品真相。严格锁定原始食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑和物理关系。不得为了“更高级”重做、替换、增减或重新摆放主体。主要创意只发生在灯光、环境、背景、景深、调色和摄影品质层。**

Stage A 输出必须成为 Stage B 的参考图输入。

---

# 5. Stage B｜Category Visual Language Routing

VISION_MODEL 在 Stage B 前判断：

```text
food_category
cuisine_family
brand_positioning
visual_mood
routing_confidence
```

再从 `references/category-visual-systems.md` 选择一个主系统：

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

Category system 是主导，Brand Positioning 是二级修饰。默认建议：

```text
Category 70%
Brand Positioning 30%
```

最多一个主系统 + 一个弱辅助系统。禁止三套以上视觉皮肤混搭。

---

# 6. Category-Native Design Rule

每个品类必须拥有自己的：
- typography personality
- spatial headline language
- layout bias
- color system
- material system
- environment / prop language
- information density
- negative style rules

禁止把“金色毛笔字”当全品类默认。

例如：
- 家常中餐 → 锅气、暖材质、厚中文展示字、门头/牌匾空间；
- 蛋糕甜点 → editorial serif、奶油/玻璃/丝带柔性装置；
- 咖啡饮品 → modern grotesk、玻璃/窗面/透明轻空间字、Lifestyle 留白；
- 西餐 → refined serif、石材/银器/亚麻、Fine Dining 克制空间；
- 烘焙 → warm serif、晨光、木/纸/麦金、橱窗/包装纸空间；
- 包装食品 → Hero Packshot、品牌识别、展台/货架、包装 DNA 锁定。

读取：
- `references/category-router.md`
- `references/category-visual-systems.md`
- `references/category-style-firewall.md`
- `references/typography-personality-map.md`
- `references/layout-bias-map.md`
- `references/brand-positioning-map.md`

---

# 7. Global Product Hero Priority

这条规则覆盖所有品类和版式偏好：

> **产品永远是第一视觉主角。**

统一优先级：

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / QR / UTILITY INFO
```

禁止：
- 为了标题更大而缩小产品；
- 把产品推成远景或边角摆设；
- 把产品当标题背景；
- 让空间字遮挡关键食欲区 / 包装识别区；
- 第一视觉记忆只剩标题。

> **Typography builds the world around the product; it does not replace the product.**

读取 `references/product-hero-priority.md`。

---

# 8. Stage B IMAGE_MODEL Hero Lock

Stage B 发送给 IMAGE_MODEL 的提示词中，必须明确包含同等强度约束：

> **以 Stage A 商拍图中的产品为 Hero Product。产品必须始终是第一视觉主角。标题可以有厚度、透视、材质和空间张力，但不得把产品缩小、后退、遮挡或降为背景/摆设。调用当前食品品类自己的字体、空间、色彩、材质和信息密度系统。**

---

# 9. Spatial Typography + Restraint

标题不能只是平贴，但也不能喧宾夺主。

可根据品类成为：
- 门头 / 牌匾 / 墙体 / 舞台；
- 屏风 / 走廊 / 悬挂招牌；
- 奶油浮雕 / 丝带 / 玻璃/亚克力装置；
- 橱窗字 / 窗面字 / 桌面投影字；
- 包装展示墙 / 展台字。

主标题、副标题、Slogan 不默认三行平排。应通过：
- 尺度差；
- 前后层次；
- 高低错位；
- 方向变化；
- 透视；
- 受控遮挡；
- 材质差；

建立节奏。

但文字视觉权重永远不得越过 Product Hero。

---

# 10. Shared Perspective + Controlled Occlusion

使用空间字体时，建立一个主消失点或一致透视场。

标题、产品、桌面/展台、器皿、背景结构、蒸汽/冰气、道具与光影应在同一空间逻辑内。

允许轻微遮挡制造层次，但关键汉字默认遮挡不超过约 8–12%，不得吞掉识别笔画。

---

# 11. Information Density

如果用户没要求极简，默认可使用：
- headline
- subtitle
- 1 条 slogan / campaign line
- 3–4 个精炼卖点（只在品类适合时）
- 店名
- 地址 / 电话（若提供）
- QR 功能区（有真实 QR/目标时）

密度按品类变化：
- 中式家常 / 川湘 / 包装食品：中高；
- 汤煲 / 面食 / BBQ / 烘焙：中等；
- 高档海鲜 / 蛋糕 / 咖啡 / 西餐 / 日料：低到中等。

不要强迫所有品类使用四个圆形卖点章。

---

# 12. Category Style Firewall

可以跨品类共享：
- Hero Product
- 透视
- 空间字
- 前中后景
- 遮挡
- 负空间
- 统一光影
- 视觉层级

不能共享行业/品类视觉皮肤。

禁止：
- 蛋糕 → 中式饭馆大金字门头；
- 咖啡 → 家常菜四圆章模板；
- 西餐 → 川湘红金大毛笔字；
- 高档海鲜 → 夜市粗糙招牌；
- 家常热菜 → 冷感科技发布会；
- 包装食品 → 重画包装 Logo/文字/结构。

---

# 13. True Upper-Bound Standard

当用户说：
- 上限版
- 真正上限
- 顶级版
- 世界级
- 最高标准
- 再加强视觉张力

自动进入 `UPPER_BOUND_MODE`。

上限不是更吵，而是：
- Product Hero 仍第一；
- 品类语言更具体；
- 标题拥有该品类专属材质、厚度、透视或空间行为；
- 副标题/Slogan 有明确节奏；
- One Big Idea 清晰；
- 前中后景深度明确；
- 光影与材质达到 Campaign 级；
- 信息完整但不过载；
- Food/Packaging DNA 不漂移。

读取 `references/upper-bound-standard.md`。

---

# 14. Typography & Business Data Accuracy

用户提供的信息必须 **100% 准确**：
- 主标题
- 副标题
- 店名 / 品牌
- 地址
- 电话
- 价格
- 活动文字

禁止错字、漏字、随机汉字、电话错误、地址错误、擅自改写品牌。

---

# 15. QR Rule

- 用户提供真实 QR → 原样锁定；
- 用户提供明确扫码 URL 且运行环境支持 → 在图像模型外生成真实 QR 再叠加；
- 无 QR/目标 → 只预留 QR Safe Zone；
- 禁止把 AI 随机矩阵当正式可扫码二维码。

---

# 16. Production Workflow

在 `PRODUCTION` 状态：

```text
1. User uploads image + natural-language info
2. VISION_MODEL reads source image
3. Check KV information gate
4. PP-food-001 builds Stage A fidelity route
5. IMAGE_MODEL receives original image + Stage A hard-lock prompt
6. Stage A cinematic commercial image
7. VISION_MODEL runs Fidelity QC
8. Resolve category / positioning / visual system
9. Build One Big Idea + spatial typography + information hierarchy
10. IMAGE_MODEL receives Stage A image + Stage B hero/category prompt
11. Generate KV
12. VISION_MODEL runs Product Dominance + Category + KV QC
13. Targeted retry if required
14. Deliver
```

用户不需要知道内部 JSON、Visual System、Prompt 或评分表。

---

# 17. Targeted Retry

不要随机整张重抽。

- Food DNA 漂移 → Stage A Reference Lock Retry
- 产品沦为背景 → Product Hero Retry
- 标题太平 → Spatial Typography Retry
- 标题太抢 → Typography Restraint Retry
- 品类串台 → Category Router Retry
- 信息过稀/过密 → Information Density Retry
- 文字错误 → Typography Accuracy Retry
- 缺乏 Campaign 张力 → Upper-Bound Creative Retry

---

# 18. Final QA

必须通过：
- Food Fidelity QC
- Product Dominance QC
- Typography Accuracy QC
- Spatial KV QC
- Category Visual Language QC
- Upper-Bound QC（如果用户要求）

阈值：

```text
Food Fidelity >=95
Vessel Fidelity >=98
Typography Accuracy =100
Category Visual Language >=85
KV Design Quality >=90
Product Dominance = PASS
Upper-Bound Readiness >=90  # when requested
```

如果换成完全不同品类而海报几乎无需变化 → 模板化失败。

如果去掉产品以后标题仍像完整主视觉、产品只是摆设 → Product Hero 失败。

---

# Final Command

> **If runtime readiness is unknown: read HANDOFF.md first. Configure VISION_MODEL + IMAGE_MODEL + API connection, wait for “启动”, then produce.**
>
> **Preserve the food. Upgrade the photography. Build the category-native KV. Keep the product first.**
