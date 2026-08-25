# PP-food-KV-001

高保真、跨品类餐饮 Key Visual 生成 Skill（V1.3.1）。

## 一句话定义

**先锁住原食物，再把它拍成电影级商拍，然后识别品类，最后调用这个品类自己的 KV 视觉语言。**

这版继续坚持：**不把所有美食都做成同一套海报，也不允许为了文字张力把主产品变成背景。**

## 强制工作流

1. 信息门槛：主标题 + 副标题 + N≥1
2. Food DNA 锁定（继承 `PP-food-001` 思路）
3. 先完成同一份食物的电影级商拍底图
4. 识别 `food_category / cuisine_family / brand_positioning / visual_mood`
5. 调用对应品类视觉系统
6. One Big Idea + Spatial Typography + Layout + Color + Material + Information Density
7. Food QC + Product Dominance QC + Typography QC + KV QC + Category QC

## V1.3.1 新增：Product Hero Priority

这是所有美食品类通用的全局硬规则：

> **产品是第一主角，标题是第二主视觉。**

主标题、副标题、Slogan 可以有透视、厚度、材质、空间感和视觉张力，但不得为了突出文字而：
- 缩小主产品；
- 把产品推成远景；
- 把产品当标题的背景或摆设；
- 让空间字压住产品关键食欲区 / 包装识别区；
- 让用户第一眼只记住标题，之后才发现产品。

统一视觉优先级：

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / QR / UTILITY INFO
```

详细规则见 `references/product-hero-priority.md`。

## 12 大品类视觉系统

| Visual System | 适用品类 | 核心视觉语言 |
|---|---|---|
| CN_HOME_STYLE_SYSTEM | 中式家常热菜 | 烟火、锅气、门头、厚中文标题 |
| SPICY_HOT_SYSTEM | 川湘鲜麻热辣 | 强动势、红/绿风味色、厚透视字 |
| CLAYPOT_SOUP_SYSTEM | 砂锅、煲、汤锅 | 蒸汽、围炉、陶/铜、暖琥珀 |
| NOODLE_RICE_NOODLE_SYSTEM | 面、米线、粉 | 上升动线、热汤、主食力量 |
| BBQ_NIGHTMARKET_SYSTEM | 烧烤、炸物、夜市 | 炭火、夜牌、烟雾、悬挂招牌 |
| SEAFOOD_PREMIUM_SYSTEM | 海鲜、高档中餐 | 鲜、精致、宴席、克制金属感 |
| DESSERT_CAKE_SYSTEM | 蛋糕、甜点、西点 | 轻盈、杂志、serif、奶油/玻璃/丝带 |
| COFFEE_TEA_SYSTEM | 咖啡、茶饮、饮品 | Lifestyle、留白、现代无衬线、玻璃窗光 |
| WESTERN_DINING_SYSTEM | 牛排、意面、西餐 | Fine Dining、精致 serif、石材/银器 |
| JAPANESE_KOREAN_SYSTEM | 日料、韩料 | 东亚现代、几何秩序、原木/纸/石 |
| BAKERY_BREAKFAST_SYSTEM | 面包、早餐、烘焙 | 晨光、纸张、麦金、温暖 editorial |
| RETAIL_PACKAGED_SYSTEM | 零食、礼盒、包装食品 | Packshot、品牌识别、货架/展台、转化信息 |

## Category Style Firewall

不同品类必须真正不同，而不是只换颜色：
- 蛋糕甜点：默认禁止中式大金字饭馆门头
- 咖啡茶饮：默认禁止家常菜四圆章卖点模板
- 西餐：默认禁止川湘红金大毛笔字
- 高档海鲜：默认禁止夜市粗糙招牌
- 家常热菜：默认禁止冷感甜品/科技视觉
- 包装食品：包装结构和品牌文字属于产品 DNA，不得随意改写

## 字体不再只有“金色毛笔字”

字体按照品类路由：
- 家常菜 / 川湘：粗中文展示字、毛笔、招牌体
- 高档海鲜：精致宋体 / 现代黑体 / 克制金字
- 蛋糕甜点：Editorial Serif / Fashion Serif / Soft Display
- 咖啡茶饮：Modern Grotesk / Clean Sans
- 西餐：High-contrast Serif + Clean Sans
- 日韩：Minimal Sans / Narrow Grotesk
- 烘焙：Warm Serif / Friendly Sans

但无论哪种字体系统，都必须遵守：

> **Typography builds the world around the product; it does not replace the product.**

## 信息密度也按品类变化

不是所有海报都要 4 个卖点圆章：
- 中式家常 / 川湘 / 包装食品：中高密度
- 汤煲 / 面食 / BBQ：中密度
- 高档海鲜 / 蛋糕 / 咖啡 / 西餐 / 日料：默认低到中密度

## 主要参考文件

- `references/category-router.md`
- `references/category-visual-systems.md`
- `references/category-style-firewall.md`
- `references/typography-personality-map.md`
- `references/layout-bias-map.md`
- `references/brand-positioning-map.md`
- `references/category-qc.md`
- `references/product-hero-priority.md`

## 验收目标

```text
Food Fidelity >= 95
Vessel Fidelity >= 98
Typography Accuracy = 100
Category Visual Language >= 85
KV Design Quality >= 90
Product Dominance = PASS
```

**如果把食物换成完全不同品类，整张 KV 仍几乎不用变，那就是模板化失败。**

**如果去掉产品后标题仍像完整主视觉，而产品只是一个摆设，那就是 Product Hero 失败。**
