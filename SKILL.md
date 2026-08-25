---
name: PP-food-KV-001
description: Use when a user provides a real food photo and wants a premium Chinese restaurant Key Visual, campaign poster, hero food poster, menu hero image, or promotional KV while preserving the original food identity and using provided headline/subheadline/business information.
---

# PP-food-KV-001

## Overview

把真实餐饮随手拍变成高保真、高视觉张力、可传播的餐饮 Key Visual。

**核心顺序不可颠倒：**

> **先锁食物 → 再做电影级商拍 → 最后做 KV。**

KV 创意不能以牺牲食物 DNA 为代价。

---

## 1. Entry Gate｜信息门槛

进入正式 KV 设计前必须满足：

```text
headline = required
subtitle = required
auxiliary_information_count >= 1
```

辅助字段可以是：Slogan、店名、品牌名、核心食材、卖点、地址、电话、预订电话、营业时间、价格、菜系、活动信息等。

如果不足，只询问**最少缺失信息**；禁止编造电话、地址、价格、营业时间、品牌历史、认证或促销活动。

详见 `references/information-gate.md`。

---

## 2. Stage A｜Food Fidelity First

在任何 KV 构图之前，先按 `PP-food-001` 的原则建立 Food Fidelity Manifest。

硬目标：

- Food Identity ≥ 95%
- Ingredient Geometry ≥ 95%
- Vessel / Container Identity ≥ 98%
- Plating Fidelity ≥ 95%
- Physical Relationship Fidelity ≥ 95%

必须锁定：

- 食物类别
- 主辅食材
- 食材形状 / 切法 / 大小关系
- 配料数量与空间关系
- 汤汁 / 酱汁 / 油脂基础状态
- 原器皿材质、颜色、形状
- 原装盘拓扑

只允许显著升级：

- 灯光
- 背景
- 环境
- 景深
- 摄影构图
- 商业调色
- 材质可见度

**Stage A 的结果应该先单独成立为“同一份食物的电影级商拍”。**

如果 Food DNA 未锁住，不得进入 Stage B。

详见 `references/food-fidelity-bridge.md`。

---

## 3. Stage B｜KV Art Direction

Food Fidelity PASS 后，开始 KV。

先确定：

1. 菜名 / 菜系 / 风味语义
2. One Big Idea
3. Hero Food 最近景策略
4. 主消失点
5. Spatial Typography 类型
6. 遮挡关系
7. 信息密度
8. 字体层级
9. 语义背景
10. QA

---

## 4. Food Remains Hero

视觉优先级：

```text
1. FOOD HERO
2. HEADLINE
3. CREATIVE SPACE
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS INFORMATION
```

默认让美食成为最近、最大、最锐利的对象。

可以让碗 / 盘适度出画，但不能重做食物本身。

---

## 5. One Big Idea

每张 KV 只建立一个核心视觉创意。

不要同时堆叠：国潮 + 赛博 + 水墨 + 杂志 + 电影 + 复古。

创意必须来自：

- 菜品语义
- 食材特征
- 风味
- 地域
- 用户文案
- 原照片构图机会

例：青椒酸菜鱼 → “鲜麻入席”“鲜麻风暴中心”“青椒香气穿过门头空间”。

---

## 6. Spatial Typography

主标题不是平贴信息，而是第二主视觉和空间构件。

允许模式：

- TITLE_AS_SIGNAGE
- TITLE_AS_ARCHITECTURE
- TITLE_AS_STAGE
- TITLE_AS_DEPTH_FIELD
- TITLE_AS_FOREGROUND_GRAPHIC

主标题可以成为餐厅门头、牌匾、门廊、墙体、舞台、纵深字场，但必须保持中文可读性。

详见 `references/spatial-typography-engine.md`。

---

## 7. Shared Vanishing Point

优先建立一个 `MASTER_VANISHING_POINT`。

标题结构、桌面纹理、器皿、背景建筑、信息牌、蒸汽方向和光影尽量服从同一纵深逻辑。

详见 `references/vanishing-point-director.md`。

---

## 8. Controlled Occlusion

通过轻微遮挡制造空间，而不是通过遮挡制造乱码。

允许：蒸汽、碗沿、筷子、青花椒枝等轻擦标题边缘。

建议单字遮挡预算 ≤ 8–12%，且不得遮挡关键识别笔画。

详见 `references/occlusion-engine.md`。

---

## 9. Domain Style Firewall

可以借鉴其他行业的 Campaign **构图语法**：

- 巨型字体
- 透视
- Hero Product
- 前中后景
- 遮挡
- 负空间
- 信息层级

但禁止默认继承：

- HUD
- 科技走廊
- 赛博霓虹
- 科技网格
- 数码参数卡
- 发布会视觉

除非用户明确要求。

**迁移构图方法，不迁移行业视觉皮肤。**

详见 `references/domain-style-firewall.md`。

---

## 10. Campaign Information Density

满足信息门槛后，默认输出不是“极简两行字”。

优先建立：

- Headline
- Subtitle
- 1 条原创传播句 / Slogan（非官方声明）
- 3–4 个卖点
- 已有店名 / 地址 / 电话
- QR safe zone / 真实二维码
- 少量装饰信息

但信息层级必须清楚，不能做成密集宣传单。

卖点只能来自用户信息或照片 / 菜名可合理支持的感官属性；禁止编造认证、历史、来源、每日现杀等硬事实。

详见 `references/information-density.md`。

---

## 11. Typography Accuracy

以下用户提供文字必须 100% 准确：

- 主标题
- 副标题
- 店名
- 地址
- 电话
- 价格
- 活动文字

任何错字、乱码、漏字、数字错误均判 FAIL。

字体视觉层级：

```text
T1 Headline          100%
T2 Subtitle          35–50%
T3 Slogan/Selling    15–25%
T4 Utility Info       8–15%
```

详见 `references/typography-system.md`。

---

## 12. QR Rule

如果用户提供真实二维码：保留并使用真实二维码。

如果没有真实二维码：

- 可以预留右下角 QR safe zone；
- 可以在设计预览中使用明确的占位块；
- 不得把随机生成的不可控二维码当成正式扫码信息交付。

---

## 13. Prompt Build

最终提示词必须分层：

1. Source Truth / Food Locks
2. Commercial Re-photography
3. Dish Semantics
4. One Big Idea
5. Hero Food Composition
6. Spatial Typography
7. Vanishing Point
8. Occlusion
9. Information Density
10. Lighting / Color
11. Text Accuracy
12. Negative Rules

详见 `references/prompt-builder.md`。

---

## 14. Final QA

必须执行三重检查：

### Food Fidelity QC
食物是否仍是原图那一份。

### Typography QC
所有关键文字是否逐字准确。

### KV QC
是否存在视觉概念、空间张力、清晰层级和餐饮语义。

交付阈值：

```text
Food Fidelity >= 95
Vessel Fidelity >= 98
Typography Accuracy = 100
Semantic Relevance >= 85
KV Design Quality >= 90
```

失败按错误类型定向重试，不要随机重抽。

详见 `references/kv-qc.md` 与 `references/retry-policy.md`。

---

## Core Command

> **PRESERVE THE FOOD. UPGRADE THE PHOTOGRAPHY. THEN BUILD THE KV.**
>
> **MAKE THE HEADLINE PART OF THE SPACE, NOT A LABEL ON TOP OF THE IMAGE.**
>
> **TRANSFER CAMPAIGN COMPOSITION GRAMMAR, NOT NON-FOOD INDUSTRY SKIN.**