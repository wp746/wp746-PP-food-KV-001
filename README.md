# PP-food-KV-001

餐饮随手拍 → 世界级 Key Visual（KV）海报的可复用 Skill。

> 核心原则：**先锁住真实美食，再做电影级商拍，最后做 KV。**
>
> **Preserve the food first. Upgrade the photography second. Build the KV third.**

## 1. 这套 Skill 解决什么问题

用户只需要提供：

1. 一张真实随手拍美食照片；
2. **主标题（必填）**；
3. **副标题（必填）**；
4. 再提供任意一个辅助信息字段（N ≥ 1），例如店名、Slogan、核心食材、卖点、地址、电话、价格、营业信息等。

满足“**主标题 + 副标题 + N**”后，Skill 才进入正式 KV 设计。

最终目标不是普通菜单海报、促销单或简单“照片上加字”，而是：

- 高保真锁定原食物 DNA；
- 把随手拍升级成电影工作室级商拍；
- 根据菜名 / 菜系 / 风味做语义背景；
- 用空间化主标题、统一消失点、受控遮挡、Hero Food 最近景制造视觉张力；
- 建立完整但克制的信息密度；
- 输出真正具有传播记忆点的餐饮 KV。

## 2. 两阶段视觉引擎

### Stage A｜Food Fidelity + Commercial Re-photography

先执行 `PP-food-001` 的核心原则：

- Food Identity ≥ 95%
- Ingredient Geometry ≥ 95%
- Vessel / Container Identity ≥ 98%
- Plating Fidelity ≥ 95%
- Physical Relationship Fidelity ≥ 95%

这一阶段只允许显著改变：灯光、背景、环境、景深、色彩、摄影质感。

**不得因为“更高级”而重做食材、换碗、换盘、重摆盘。**

### Stage B｜KV Art Direction

只有当 Stage A 主体稳定后，才进入 KV：

- One Big Idea
- Dish Semantic Router
- Hero Food Foreground
- Spatial Typography
- Shared Vanishing Point
- Controlled Occlusion
- Information Hierarchy
- Campaign Density
- Typography QA
- KV QA

## 3. 默认信息结构

满足输入门槛后，默认优先构建：

- 主标题（必须）
- 副标题（必须）
- 1 条 Slogan / 传播句（若用户未提供，可生成原创“非官方”微文案）
- 3–4 个卖点（只允许来自用户信息或从照片可合理支持的产品特征，不编造事实）
- 店名 / 品牌名（若有）
- 地址（若有）
- 电话（若有）
- 右下角二维码区域（若真实二维码素材存在则使用；没有时只预留 QR safe zone，不伪造真实扫码内容）

默认信息密度是“完整 Campaign KV”，但后续可以按用户要求增删改查。

## 4. 核心视觉方法

### Hero Food 最近景

美食是第一主角。默认把主体放在最近景、最大、最锐利的位置；允许碗 / 盘适度出画，制造镜头逼近感。

### Spatial Typography

主标题不能只是平贴文字，而应根据餐饮语义成为：

- 门头 / 招牌
- 墙体 / 门廊
- 舞台 / 背景结构
- 纵深文字场
- 前景图形结构

### Shared Vanishing Point

标题、器皿、桌面、蒸汽、信息牌、背景建筑尽量共享一个主消失点，避免“照片一套透视，文字另一套透视”。

### Controlled Occlusion

允许蒸汽、碗沿、食材枝叶轻擦文字边缘制造层次，但不能吞字、错字或破坏识别。

### Domain Style Firewall

可以迁移数码 Campaign 的构图语法，但**禁止把食品 KV 做成科技 / HUD / 赛博 / 数码发布会风格**，除非用户明确要求。

> 迁移构图方法，不迁移行业视觉皮肤。

## 5. 仓库结构

```text
wp746-PP-food-KV-001/
├── README.md
├── SKILL.md
├── VERSION
├── references/
│   ├── information-gate.md
│   ├── food-fidelity-bridge.md
│   ├── dish-semantic-router.md
│   ├── creative-director.md
│   ├── spatial-typography-engine.md
│   ├── vanishing-point-director.md
│   ├── occlusion-engine.md
│   ├── domain-style-firewall.md
│   ├── information-density.md
│   ├── typography-system.md
│   ├── prompt-builder.md
│   ├── kv-qc.md
│   └── retry-policy.md
└── tests/
    └── test-cases.md
```

## 6. 最终验收

只有同时满足以下条件才算合格：

- Food Fidelity ≥ 95
- Container / Vessel Fidelity ≥ 98
- Typography Accuracy = 100%
- Semantic Background ≥ 85
- KV Design Quality ≥ 90
- 不存在随机文字 / 错别字 / 乱码 / 假二维码 / 食材明显重构

## 7. 适用范围

适合：

- 餐厅主菜 KV
- 菜品招牌海报
- 新品推广
- 门店朋友圈 / 小红书 / 抖音封面
- 菜单 Hero Visual
- 地方特色菜传播
- 饮品 / 甜品 / 烧烤 / 火锅 / 中餐 / 西餐等餐饮产品

不适合直接用于：

- 纯人物写真
- 非食品主视觉的品牌 Campaign
- 需要完全工业级包装复制的 FMCG 包装设计

## 8. 版本

当前版本：**V1.1.0**

V1.1.0 重点强化：

- 先商拍、后 KV 的双阶段硬流程
- 食物 DNA 高保真桥接
- 空间化标题
- 共用消失点
- 受控遮挡
- 餐饮行业风格防污染
- 默认 Campaign 信息密度
- 3–4 个卖点系统
- 二维码安全区与真实性规则

---

**一句话定义：**

> 保留真实食物，先把它拍成顶级商拍，再让标题、空间、光影和信息系统一起成为 KV。