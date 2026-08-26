# PP-food-KV-001

高保真、跨品类餐饮 Key Visual 生成 Skill（V1.4.0）。

## 一句话定义

**先配置运行环境，再等待用户说“启动”；生产时先锁住原食物并完成电影级商拍，再识别品类，最后调用该品类自己的 KV 视觉语言。**

## 首次安装：现在自带“交接文档”

根目录新增：`HANDOFF.md`。

新的智能体安装本 Skill 后，应先读取 `HANDOFF.md`，而不是马上出图。它必须提醒用户完成以下配置：

- **VISION_MODEL**：用于识图、Food DNA、品类路由和生成后 QC；
- **IMAGE_MODEL**：用于参考图编辑、Stage A 商拍和 Stage B KV；
- **API_BASE_URL**：聚合平台/模型服务 URL；
- **API Key/Credential**：建议放在 Secret / Environment / Connection 中；
- IMAGE_MODEL 支持 reference image / image editing；
- Stage A 输出能继续作为 Stage B 输入；
- VISION_MODEL 能读取用户上传图和生成结果。

如果宿主默认模型不识图，智能体**不得猜图**，必须调用用户配置的视觉模型。

配置完成后，它应该明确告诉用户：

> **PP Food 双 Skill 运行环境已准备就绪。回复“启动”进入生产模式。**

用户只需要回复：

> **启动**

之后即可像普通聊天一样生产，不需要理解 Prompt、Food DNA、Category Router、空间字体或内部评分。

## 推荐运行参数

可以映射成宿主平台自己的 Secret/Connection，也可以使用：

```text
PP_FOOD_API_BASE_URL
PP_FOOD_API_KEY
PP_FOOD_VISION_MODEL
PP_FOOD_IMAGE_MODEL
```

API Key 不建议长期明文写在普通对话里。

## 双 Skill 标准生产链路

推荐同时安装 `PP-food-001`。

```text
用户原始随手拍
→ VISION_MODEL 识图
→ PP-food-001 Stage A：Food DNA 锁定 + 电影级商拍
→ IMAGE_MODEL 输出 Stage A 图
→ VISION_MODEL Fidelity QC
→ PP-food-KV-001 Stage B：品类路由 + KV
→ IMAGE_MODEL 输出 KV
→ VISION_MODEL Product / Category / KV QC
→ 定向重试或交付
```

**Stage A 输出必须继续传给 Stage B。** 这是跨智能体稳定复现的重要条件。

## 为什么需要视觉模型 + 图片模型

### VISION_MODEL
负责“看懂和判断”：
- 食物是什么；
- Food DNA 是什么；
- 属于哪个品类；
- 应走哪套视觉系统；
- 信息门槛是否满足；
- 出图以后产品有没有漂移、标题有没有压过产品、品类有没有串台。

### IMAGE_MODEL
负责“真正编辑和出图”：
- 根据参考图锁定主体；
- Stage A 商拍；
- Stage B KV；
- 执行空间字体、光影和品类视觉设计。

因此，“图片模型能根据参考图出图”并不等于可以省略视觉理解/QC 层。

## KV 信息门槛

正式 KV 设计默认要求：

```text
主标题 = 必填
副标题 = 必填
其他信息 N >= 1
```

N 可以是店名、品牌名、Slogan、核心食材、卖点、地址、电话、价格、营业信息、菜系等真实信息。

信息不足时，只追问最少缺失项。

## Stage A：先把产品拍对

先执行 `PP-food-001` 风格的高保真商拍：

- Food Identity ≥95%
- Ingredient Geometry ≥95%
- Vessel / Container Identity ≥98%
- Plating Fidelity ≥95%
- Physical Relationship Fidelity ≥95%

IMAGE_MODEL 的 Prompt 前部必须明确：

> **以用户上传参考图为唯一产品真相。严格锁定原始食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑和物理关系。不得为了更高级重做、替换、增减或重新摆放主体。只升级灯光、环境、背景、景深、调色和商业摄影品质。**

## Stage B：再做真正 KV

Stage B 使用 Stage A 输出作为产品真相，再执行：

- Category Visual Language Router
- One Big Idea
- Product Hero Priority
- Spatial Typography
- Shared Perspective
- Controlled Occlusion
- Information Hierarchy
- Category Style Firewall
- Upper-Bound Standard

Stage B 的 IMAGE_MODEL Prompt 必须明确：

> **以 Stage A 商拍图中的产品为 Hero Product。产品必须始终是第一视觉主角。标题可以有厚度、透视、材质和空间张力，但不得把产品缩小、后退、遮挡或降为背景/摆设。调用当前食品品类自己的字体、空间、色彩、材质和信息密度系统。**

## 12 大品类视觉系统

| Visual System | 适用品类 | 核心视觉语言 |
|---|---|---|
| CN_HOME_STYLE_SYSTEM | 中式家常热菜 | 烟火、锅气、门头、厚中文标题 |
| SPICY_HOT_SYSTEM | 川湘鲜麻热辣 | 强动势、红/绿风味色、厚透视字 |
| CLAYPOT_SOUP_SYSTEM | 砂锅、煲、汤锅 | 蒸汽、围炉、陶/铜、暖琥珀 |
| NOODLE_RICE_NOODLE_SYSTEM | 面、米线、粉 | 上升动线、热汤、主食力量 |
| BBQ_NIGHTMARKET_SYSTEM | 烧烤、炸物、夜市 | 炭火、夜牌、烟雾、悬挂招牌 |
| SEAFOOD_PREMIUM_SYSTEM | 海鲜、高档中餐 | 鲜、精致、宴席、克制金属感 |
| DESSERT_CAKE_SYSTEM | 蛋糕、甜点、西点 | 轻盈、editorial、奶油/玻璃/丝带 |
| COFFEE_TEA_SYSTEM | 咖啡、茶饮、饮品 | Lifestyle、留白、现代无衬线、玻璃/透明字 |
| WESTERN_DINING_SYSTEM | 牛排、意面、西餐 | Fine Dining、精致 serif、石材/银器 |
| JAPANESE_KOREAN_SYSTEM | 日料、韩料 | 东亚现代、几何秩序、原木/纸/石 |
| BAKERY_BREAKFAST_SYSTEM | 面包、早餐、烘焙 | 晨光、纸张、麦金、温暖 editorial |
| RETAIL_PACKAGED_SYSTEM | 零食、礼盒、包装食品 | Packshot、品牌识别、货架/展台、转化信息 |

## Product Hero 是最高硬规则

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

## 上限模式

用户说“上限版 / 真正上限 / 顶级版 / 世界级 / 再加强视觉张力”时，自动进入 `UPPER_BOUND_MODE`。

上限不是把字做得更大，而是：
- 产品继续第一；
- 品类视觉语言更具体；
- 主标题拥有该品类专属材质、厚度、透视和空间行为；
- 副标题 / Slogan 有节奏和层次；
- One Big Idea 清晰；
- 前中后景、光影和材质达到 Campaign 级；
- Food/Packaging DNA 不漂移。

## 验收目标

```text
Food Fidelity >= 95
Vessel Fidelity >= 98
Typography Accuracy = 100
Category Visual Language >= 85
KV Design Quality >= 90
Product Dominance = PASS
Upper-Bound Readiness >= 90  # 用户要求上限版时
```

## 主要文件

- `SKILL.md`
- `HANDOFF.md`
- `references/category-router.md`
- `references/category-visual-systems.md`
- `references/category-style-firewall.md`
- `references/typography-personality-map.md`
- `references/layout-bias-map.md`
- `references/brand-positioning-map.md`
- `references/category-qc.md`
- `references/product-hero-priority.md`
- `references/upper-bound-standard.md`
- `tests/test-cases.md`

## 最终使用体验

安装 → 智能体主动提醒配置 VISION_MODEL / IMAGE_MODEL / URL / Credential → 自检 → 告诉用户“准备就绪” → 用户回复 **“启动”** → 后续完全自然语言生产。
