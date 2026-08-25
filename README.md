# PP-food-KV-001

餐饮随手拍 → 世界级 Key Visual（KV）海报的可复用 Skill。

> **核心顺序：先锁住真实美食 → 升级成电影级商拍 → 再做 KV。**
>
> **Preserve the food first. Upgrade the photography second. Build the KV third.**

当前版本：**V1.1.0**

---

## 1｜输入门槛：主标题 + 副标题 + N

用户提供一张真实美食照片后，正式进入 KV 设计前必须满足：

- **主标题：必填**
- **副标题：必填**
- **辅助信息 N：至少 1 项**

辅助信息可以是：店名、品牌名、Slogan、核心食材、菜品卖点、地址、电话、预订电话、价格、营业信息、菜系等。

如果不足，Skill 只询问最少缺失项，不重复追问已经提供的内容，也不编造商业事实。

---

## 2｜双阶段视觉引擎

### Stage A｜Food Fidelity + Commercial Re-photography

先继承 `PP-food-001` 的高保真逻辑：

- Food Identity ≥ 95%
- Ingredient Geometry ≥ 95%
- Vessel / Container Identity ≥ 98%
- Plating Fidelity ≥ 95%
- Physical Relationship Fidelity ≥ 95%

这一阶段的目标是：

> **先让原始随手拍成为“同一份菜”的电影工作室级商拍图。**

允许大幅升级灯光、背景、环境、景深、调色和材质表现；禁止为了更好看而换食材、换器皿、重摆盘或增加高级配料。

### Stage B｜KV Art Direction

只有 Stage A 的 Food DNA 通过质检后，才进入 KV：

- 菜品语义识别
- One Big Idea
- Hero Food 最近景
- 空间化主标题
- 共用消失点
- 受控遮挡
- Campaign 信息密度
- 中文字体层级
- 二维码功能层
- 三重 QA

---

## 3｜KV 不是“照片上加字”

真正的餐饮 KV 要同时具备：

- Food Hero
- 强视觉概念
- 空间化主标题
- 前 / 中 / 后景纵深
- 统一透视与光影
- 清晰信息层级
- 菜品语义相关背景
- 传播级完成度

### 主标题空间化

标题不只是叠字，可以根据菜品和场景成为：

- 门头 / 招牌
- 墙体 / 门廊
- 舞台 / 空间框架
- 纵深文字场
- 前景图形结构

### Hero Food 最近景

美食永远是第一主角：最近、最大、最锐利。允许器皿适度出画制造镜头逼近感，但 Food DNA 不能改变。

### Shared Vanishing Point

碗 / 盘、桌面、标题空间、背景建筑、菜单牌、蒸汽和光线尽量服从同一主消失点，避免“标题像后贴上去”。

### Controlled Occlusion

允许蒸汽、碗沿、筷子或食材枝叶轻擦标题边缘制造层次，但不得吞掉关键笔画。建议单字遮挡预算 ≤ 8–12%。

---

## 4｜餐饮行业风格防污染

本 Skill 可以学习其他优秀 Campaign 的**构图语法**：

- 巨型文字
- 一点透视 / 斜切透视
- Hero Product
- 前中后景
- 遮挡
- 负空间
- 信息层级
- 统一光影

但不会默认复制其他行业的视觉皮肤。

除非用户明确要求，否则禁止：

- HUD
- 科技参数卡
- 赛博霓虹
- 科技走廊
- 未来网格
- 数码发布会视觉

> **迁移构图方法，不迁移行业视觉皮肤。**

---

## 5｜默认 Campaign 信息密度

满足“主标题 + 副标题 + N”后，默认优先构建：

1. 主标题
2. 副标题
3. 1 条原创传播句 / Slogan
4. 3–4 个卖点
5. 店名 / 品牌名（若有）
6. 地址（若有）
7. 电话（若有）
8. 二维码功能区
9. 少量地域 / Campaign 装饰信息

这是一套默认完整信息结构，**不是死模板**。用户后续可以要求增加、删除、修改或移动任意信息模块，而不需要重做 Food Hero。

### 卖点真实性

3–4 个卖点优先来自用户输入、菜名语义或照片明确支持的感官特征，例如：

- 鲜麻开胃
- 鱼片嫩滑
- 酸菜提鲜
- 热汤入味

禁止无依据编造：非遗、百年老店、每日现杀、有机认证、祖传秘方、奖项等硬事实。

---

## 6｜二维码规则

二维码必须作为真实功能层处理：

1. 用户提供真实二维码 → 原样使用；
2. 用户提供明确扫码目标，且运行环境支持二维码生成 → 在图像模型外生成真实二维码，再叠加；
3. 没有明确扫码目标 → 只预留 QR safe zone；
4. 禁止让图像模型随机画一个二维码并作为正式可扫码信息交付。

默认倾向右下角，但会根据 Food Hero、地址电话和负空间动态调整。

---

## 7｜文字准确率

以下用户提供的信息必须 **100% 准确**：

- 主标题
- 副标题
- 店名
- 地址
- 电话
- 价格
- 活动信息

任何错字、漏字、乱码或电话号码错误都直接判定 FAIL。

视觉层级建议：

```text
T1 主标题             100%
T2 副标题             35–50%
T3 Slogan / 卖点      15–25%
T4 地址 / 电话等       8–15%
```

---

## 8｜最终验收

只有同时满足以下条件才允许作为 Hero KV 交付：

```text
Food Fidelity >= 95
Vessel Fidelity >= 98
Typography Accuracy = 100
Semantic Relevance >= 85
KV Design Quality >= 90
```

KV Design Quality 会检查：

- 创意概念
- 视觉层级
- 构图
- 空间字体
- 商拍质感
- 菜品语义相关性
- 色彩
- 细节完成度

失败时按“食物漂移 / KV 太平 / 文字错误 / 行业风格污染 / 信息过稀 / 信息过密”等具体错误定向重试。

---

## 9｜仓库结构

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
│   ├── qr-system.md
│   ├── prompt-builder.md
│   ├── kv-qc.md
│   └── retry-policy.md
└── tests/
    └── test-cases.md
```

---

## 10｜一句话定义

> **保留真实食物，先把它拍成顶级商拍，再让标题、空间、光影和信息系统一起成为 KV。**

核心命令：

> **PRESERVE THE FOOD. UPGRADE THE PHOTOGRAPHY. THEN BUILD THE KV.**
>
> **MAKE THE HEADLINE PART OF THE SPACE, NOT A LABEL ON TOP OF THE IMAGE.**