# PP FOOD｜执行B：高保真商拍 → 品类原生 KV Canonical SOP

> 快捷指令：`执行B` / `B`
>
> 角色：Stage B / Category-Native KV Engine
>
> 核心流程：**先锁食物 → 先商拍 → 再 KV。**

## 0. Authority

本文件是 **B 任务的操作 SOP**，用于跨智能体复现当前稳定生产方式。

执行时必须同时遵守：

```text
RUNTIME_MANIFEST.md                 # P0 单一事实源
SKILL.md                            # Stage B 角色与硬门槛
REQUIRED_READ_SET.md                # 必读/条件加载
PRE_FLIGHT_CHECKLIST.md             # 生产门禁
EXECUTION_CONTRACT_TEMPLATE.md      # 当前任务合同
references/*                        # 品类/字体/空间/QC 方法
```

Stage A 必须真实调用 `PP-food-001`，并以该仓库的 `SOP-A.md` 作为 A 操作 SOP。

如本 SOP 与 `RUNTIME_MANIFEST.md` 冲突，以 `RUNTIME_MANIFEST.md` 为准并 Fail Closed。

---

# 1. 用户触发协议

用户上传图片并说：

```text
执行B
```

默认含义：

```text
当前用户原图
→ VISION_MODEL
→ PP-food-001 Stage A
→ Stage A QC PASS
→ 当前任务 Stage A PASS 图
→ KV 信息门槛
→ Category Router
→ Stage B KV
→ QC
→ 定向重试
```

默认禁止：

```text
原始随手拍 → 一步激进 KV
```

Stage B 不得使用上一任务图片，不得绕回原始随手拍替代当前 Stage A PASS 图。

---

# 2. KV 文案门槛

用户说 B 后先检查当前任务文案。

默认正式 KV 需要：

```text
HEADLINE = 主标题
SUBTITLE = 副标题
AUXILIARY_INFORMATION_COUNT >= 1
```

辅助信息可为：

- 品牌/店名；
- slogan；
- 核心卖点；
- 核心食材；
- 价格；
- 净含量；
- 地址；
- 电话；
- 活动/营业信息；
- 其他真实商业信息。

## 信息不足时

只问最少缺失项，不重复问已经给过的信息。

例如：

- 只有产品名 + 店名 → 提醒补主标题/副标题；
- 已有标题、副标题但无 N → 只补 1 项辅助信息。

## 用户说“按默认文案来”

允许系统自动生成 **软文案**：

- 传播型副标题；
- 感官型 slogan；
- 非事实型卖点。

允许依据：

```text
用户产品名
当前品类语义
当前图可见特征
合理感官属性
```

例如：现烤出炉、麦香浓郁、清甜多汁、冰爽解暑、茶香回甘、外韧内软、果香满溢。

禁止自动生成未经用户/图片支持的硬事实：

```text
非遗 / 百年 / 0添加 / 有机 / 进口 / 获奖 / 官方认证
每日现杀 / 指定产地 / 医疗健康功效 / 未提供的价格地址电话
```

每个 B 任务建立：

```text
COPY_ALLOWLIST
COPY_BLOCKLIST
```

用户硬信息必须原样保真。

---

# 3. Stage A Bridge｜B 必经 A

Stage A 完整遵循 `PP-food-001/SOP-A.md`。

核心门槛至少：

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating Topology >=95
Physical Relationship >=95
Stage A QC = PASS
```

Stage A PASS 图成为：

> **当前任务 Stage B 的唯一主要产品真相。**

Stage B 不得为了排版重新做食物、重新设计包装、换器皿或改源表面状态。

---

# 4. Stage B Current Job Contract

进入 KV 前至少整理：

```text
CURRENT_JOB_STAGE_A_PASS_IMAGE
HEADLINE
SUBTITLE
BRAND_OR_STORE
SLOGAN
SELLING_POINTS
PRICE
ADDRESS
PHONE
CAMPAIGN_INFO
FOOD_CATEGORY
CUISINE_FAMILY
BRAND_POSITIONING
VISUAL_MOOD
ROUTING_CONFIDENCE
SELECTED_VISUAL_SYSTEM
COPY_ALLOWLIST
COPY_BLOCKLIST
UPPER_BOUND_MODE
```

默认：

```text
DEFAULT_KV_MODE = TRUE_UPPER_BOUND
```

用户说“上限版 / 真正上限 / 顶级版 / 世界级 / 再加强视觉张力”时明确保持 `TRUE_UPPER_BOUND = ON`。

---

# 5. Category Router｜每个任务重新路由

默认主视觉系统：

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

原则：

```text
Category System ≈ 70%
Brand Positioning ≈ 30%
```

最多：

```text
1 个主系统 + 1 个弱辅助系统
```

当前任务必须重新路由，禁止继承上一张具体字体、牌匾、拱门、丝带、灯箱、圆章、配色、背景或卖点模板。

---

# 6. Category Style Firewall

跨品类可以共享的是 **方法**：

- Hero Product；
- 透视；
- 空间字体；
- 前中后景；
- Controlled Occlusion；
- Master Vanishing Point；
- One Big Idea；
- 层级与负空间。

不能共享上一品类的 **视觉皮肤**。

典型禁止：

- 蛋糕 → 中式饭馆大金字/木门头/锅气；
- 咖啡/水果冰 → 家常菜四圆章/红金饭馆皮肤；
- 西餐 → 川湘红金大毛笔字；
- 高档海鲜 → 粗糙夜市招牌；
- 烘焙 → 自动套家常菜门头模板；
- 包装食品 → 改包装为堂食产品或重画包装 DNA。

Anti-template Test：

> 把当前产品换成完全不同品类后，如果字体、布局、材质、背景和信息结构几乎不用改，则 FAIL。

---

# 7. Product Hero Priority｜产品永远第一主角

视觉优先级：

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / QR / UTILITY INFO
```

禁止：

- 为了标题缩小产品；
- 把产品推到远景/角落；
- 把产品变成标题背景；
- 空间字大面积遮挡食欲区/包装识别区；
- 第一眼只看到文字，之后才发现产品。

硬规则：

> **标题可以强，但产品必须更强。**

---

# 8. One Big Idea

每张 KV 只允许一个主创意。

先回答：

> **这张图最应该被记住的一个视觉概念是什么？**

例：

- 面食：热汤入魂 / 蒸汽纵深；
- 烘焙：现烤出炉 / 麦香 Hero Stage；
- 甜点：轻盈茶香 / 奶油+玻璃装置；
- 水果冰：夏日爆汁 / 果冻透明空间；
- 包装罐头：阳光果香装进一罐 / Hero Packshot + 果园光感。

禁止 5 个互相竞争的创意同时上场。

---

# 9. Spatial Typography｜标题必须参与空间

标题不是后期平贴字幕。

根据当前品类，它可以成为：

```text
门头 / 招牌 / 墙体 / 屏风 / 走廊 / 悬挂牌
玻璃装置 / 奶油浮雕 / 丝带结构 / 木牌
橱窗字 / 包装展示墙 / 亚克力拱门 / 投影字
```

主标题、副标题、Slogan 不默认三行平行等权。

必须建立：

- 尺度差；
- 前后关系；
- 方向差；
- 高低错位；
- 材质差；
- 透视；
- 受光关系；
- 必要的受控遮挡。

---

# 10. Typography Restraint

字体可以有：

- 厚度；
- 浮雕；
- 金属/木材/奶油/玻璃/亚克力/丝带；
- 透视；
- 阴影；
- 环境反射；
- 空间张力。

但：

> **Typography builds the world around the product; it does not replace the product.**

若第一视觉记忆是标题而不是产品 → Typography Restraint Retry。

---

# 11. Master Vanishing Point

使用强空间结构时，尽量统一：

- 产品台面；
- 器皿椭圆；
- 标题结构；
- 展台/背景建筑；
- 信息牌；
- 道具；
- 蒸汽；
- 光线方向。

避免标题像后贴上去。

---

# 12. Controlled Occlusion

允许轻度遮挡制造真实纵深：

- 蒸汽轻擦标题；
- 产品位于标题前方；
- 叶片/水果轻触字边；
- 碗沿轻压空间字下缘；
- 丝带穿越标题层级。

关键文字默认遮挡预算约：

```text
8–12%
```

不得遮住关键识别笔画；不得遮挡核心食欲区/包装识别区。

---

# 13. 品类上限语言

## 中式家常热菜
厚中文展示字、门头/牌匾、锅气、木石铁、暖光；食物最近景。

## 川湘鲜麻热辣
厚透视字、红/绿风味色、热气、爆发纵深。

## 砂锅/汤煲
围锅舞台、半拱、陶/铜、琥珀光、汤汽层次。

## 面/米线/粉
上升动线、蒸汽纵深、主食力量，面条动线与标题呼应。

## 烧烤/夜市
悬挂招牌、灯箱、炭火、烟气、夜色高反差。

## 海鲜/高档中餐
精致宋体/现代黑体、金属/屏风、玉白/深蓝灰/克制金、高级留白。

## 蛋糕/甜点
Editorial/Fashion Serif、奶油浮雕、玻璃/亚克力、丝带、柔性空间装置；蛋糕仍最大锚点。

## 咖啡/茶饮/水果冰
Modern Sans、果冻/透明玻璃字、窗面字、阳光、冰块、水果、Lifestyle 留白。

## 西餐
High Contrast Serif + Clean Sans、石材、银器、亚麻、菜单式精致层级。

## 日韩
Minimal Sans / Narrow Grotesk、木格、纸面、招帘、几何秩序。

## 烘焙/早餐
Warm Serif / Friendly Sans、木牌、牛皮纸、麦金、晨光、烘焙空间；禁止退化成中式家常菜门头模板。

## 包装食品
Hero Packshot、品牌展示体、展台/货架/包装结构协同；包装本体最大、最清楚。

---

# 14. Information Density

默认：

```text
中高密度：家常 / 川湘 / 包装商品
中密度：汤煲 / 面食 / BBQ / 烘焙
低到中密度：高档海鲜 / 甜点 / 咖啡 / 西餐 / 日料
```

可包含：

- 主标题；
- 副标题；
- 1 条 slogan；
- 2–4 条适用品类卖点；
- 品牌/店名；
- 地址/电话/价格；
- QR 功能区。

禁止机械给每个品类放“四个圆形卖点章”。

---

# 15. Copy / Typography Accuracy

用户提供的以下硬信息必须 100% 准确：

```text
品牌名 / 店名 / 主标题 / 副标题
地址 / 电话 / 价格 / 净含量 / 活动信息
```

若 IMAGE_MODEL 文字不稳定：

- 定向重试文字区；或
- 使用外部排版/后期叠字。

不得为了视觉好看主动改写硬信息。

---

# 16. QR

- 用户提供真实 QR → 原样锁定；
- 用户提供真实目标 URL → 图像模型外生成 QR 后叠加；
- 无目标 → 只预留 `QR SAFE ZONE`。

禁止把 AI 随机矩阵作为正式二维码。

---

# 17. Stage B IMAGE_MODEL Prompt 编译

Agent 先读规则，再把当前任务编译成短而明确的 `EXECUTION_CONTRACT`。

## P1｜Stage A Product Lock

```text
以当前任务 Stage A PASS 商拍图中的真实产品为 Hero Product 和产品真相。
严格保持其产品身份、结构、器皿/包装、主要食材、源表面状态和关键颜色。
不得为了 KV 排版重新设计产品。
```

## P2｜Product Hero Priority

```text
产品必须始终是第一视觉主角，标题第二。
不得为了放大标题而缩小、后退、遮挡产品。
```

## P3｜Category Route

只注入当前 `SELECTED_VISUAL_SYSTEM` 和最多一个弱辅助系统，包括：

- typography personality；
- spatial medium；
- layout bias；
- materials；
- color system；
- environment；
- negative style rules。

## P4｜One Big Idea

只写一个核心创意。

## P5｜Spatial Typography

明确标题如何成为当前品类原生空间结构，而不是 flat overlay。

## P6｜Copy Hierarchy

```text
headline > subtitle > slogan > selling points > utility info
```

## P7｜Commercial Finish

- campaign lighting；
- coherent depth；
- consistent perspective；
- material realism；
- premium composition；
- controlled negative space。

## P8｜Negative Constraints

至少：

```text
no product demotion
no product redesign
no previous-category skin contamination
no flat flyer layout
no unsupported hard facts
no fake QR
no packaging redesign
no excessive typography dominance
```

---

# 18. True Upper-Bound

真正上限不是：字更大、金色更多、元素更多、更复杂。

必须同时做到：

1. Food/Package DNA 不漂移；
2. Product Hero 第一；
3. 当前品类语言高度明确；
4. 主标题有品类专属材质/厚度/空间行为；
5. 副标题与 Slogan 有节奏和空间层级；
6. One Big Idea 足够强；
7. 前中后景明确；
8. 光影、透视、材质统一；
9. 信息完整但不过载；
10. 缩略图下仍有强产品记忆点。

> **Upper-bound does not mean louder. It means more resolved, more specific, more dimensional and more memorable.**

---

# 19. KV QC

生成后 VISION_MODEL 至少检查：

```text
Food Fidelity = PASS / >= required threshold
Vessel / Package Fidelity = PASS
Typography Accuracy = 100%
Category Visual Language >=85
KV Design Quality >=90
Product Dominance = PASS
Upper-Bound Readiness >=90
Output Aspect Ratio = exact runtime target
No Critical Failure
```

必须回答：

- Stage A 产品是否被 Stage B 改掉？
- 第一眼是否先看到产品？
- 标题是否过强？
- 当前字体/材料/背景是否真属于当前品类？
- 是否继承了上一任务皮肤？
- 文案硬信息是否准确？
- 是否存在 unsupported hard fact？

---

# 20. Targeted Retry｜禁止随机重抽

按失败类型只修失败项：

```text
Food/Product drift          → PRODUCT_LOCK_RETRY / return Stage A if required
Typography too flat         → SPATIAL_TYPOGRAPHY_RETRY
Typography overpowering     → TYPOGRAPHY_RESTRAINT_RETRY
Wrong category skin         → CATEGORY_ROUTE_RETRY
Previous-skin contamination → STYLE_FIREWALL_RETRY
Copy error                  → COPY_ACCURACY_RETRY
Information too sparse      → INFORMATION_DENSITY_RETRY
Information overloaded      → INFORMATION_CURATION_RETRY
Weak campaign tension       → TRUE_UPPER_BOUND_RETRY
Packaging drift             → PACKAGING_FIDELITY_RETRY
```

不得无限随机重抽。

---

# 21. 执行B结束条件

只有当前任务真实经过：

```text
Stage A PASS
→ B Contract PASS
→ Stage B Generation
→ Product / Copy / Category / Upper-Bound QC PASS
```

才允许交付。

最终心法：

> **Preserve the exact current product. Build the world around it. Route every new food category again. Make the typography spatial and memorable, but keep the product first.**