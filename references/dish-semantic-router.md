# Dish Semantic Router

背景、光影、空间材质和字体性格必须服从具体菜品，而不是统一套“暗木桌 + 暖金灯”。

## Priority

```text
user-provided dish information
> high-confidence visual inference
> category-level inference
> conservative generic food direction
```

## Suggested Semantic Families

- SICHUAN_FRESH_PEPPER：青花椒、藤椒、鲜麻、酸菜鱼等；藤椒绿、酸菜黄绿、深灰石材、现代川菜空间。
- SICHUAN_SPICY_HOT：水煮鱼、毛血旺、火锅；红油、炭黑、暖红、强热感。
- SHAANXI_SOUTHERN_LOCAL：陕南地方菜；木构、山地餐饮、粗粝石材、自然木、烟火气，但避免俗套“古风景区”。
- CANTONESE_LIGHT_FRESH：清蒸、白切、煲汤；明亮克制、低饱和、清透高级中餐。
- BBQ_STREET：烧烤、夜市；炭火、夜色、摊位暖灯、烟气纵深。
- JAPANESE_MINIMAL：日料；原木、石材、留白、极简招牌。
- DESSERT_ELEGANT：甜点；柔光、奶油色、玻璃/亚克力、轻盈空间。
- CAFE_LIFESTYLE：咖啡/烘焙；城市、自然光、松弛、编辑感。

## Rule

语义背景只能支持食物，不得把背景道具变成新增食材。