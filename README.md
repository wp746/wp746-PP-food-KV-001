# PP-food-KV-001

Stage B 跨品类美食 KV / Campaign Skill。当前版本：**1.6.0**。

## 默认入口规则

```text
A = 只出 Stage A 商拍
B = 先 Stage A，再 Stage B KV
未说 A/B 且无明显商业信息 = 默认 A
未说 A/B 但给出产品名、店铺、标题、地址、价格、核心食材、卖点、新品等商业信息 = 自动 B
DEFAULT_ASPECT_RATIO = 9:16
DEFAULT_KV_MODE = TRUE_UPPER_BOUND
```

显式 A 优先于自动 B。任何 B 都不得跳过 Stage A。

## 核心方法

> **先锁产品，再识别品类，再用该品类自己的视觉语言做到真正上限。**

真正上限不重做食物本体；它发生在背景、空间、字体、主副标题层级、材质、透视、光影、One Big Idea 和 Campaign 完成度。

## 当前任务隔离

每个新任务只使用当前图片、当前用户信息和当前链路产物。上一任务的品牌、菜名、食材、口味、标题皮肤、场景皮肤、配色和道具默认失效，除非用户明确要求沿用。

## 品类原生设计

Stage B 必须先路由食品品类，再决定：
- typography personality；
- headline / subtitle spatial medium；
- layout；
- color / material；
- background / props；
- information density。

只迁移 Hero Product、透视、空间字、前中后景、遮挡、信息层级、负空间、One Big Idea 等**方法**，不迁移上一品类的具体视觉皮肤。

## Product Hero

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / UTILITY INFO
```

标题可以强，但产品必须更强。

## Full Spatial Typography

主标题、副标题、Slogan 和辅助信息必须共同形成与当前品类匹配的空间文字系统。不能只把主标题做立体字，其他信息全部平贴。

例如烘焙类可以使用 warm serif / friendly sans、橱窗字、包装纸字、吊牌、晨光投影；咖啡饮品则偏现代无衬线、玻璃/窗面/投影字和 Lifestyle 留白。具体以 `references/category-visual-systems.md` 和 `references/typography-personality-map.md` 为准。

## 双 Skill 标准链路

```text
原图
→ PP-food-001 Stage A
→ Stage A Fidelity QC
→ Stage A PASS 图
→ PP-food-KV-001 Stage B
→ Category / Product Hero / Typography / KV QC
→ 定向重试或交付
```

Stage B 必须使用当前任务 Stage A PASS 图作为参考图。

## 最终硬门槛

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

## 运行环境

首次安装读取 `HANDOFF.md`。仓库只保存通用能力约定；不要把具体供应商、模型服务 URL、API Key 或聚合平台配置写进 Skill。凭据由宿主 Secret / Environment / Connection 管理。

详细规则以 `SKILL.md` 和 `references/` 为准。
