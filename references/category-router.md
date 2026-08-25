# Category Visual Language Router

## Purpose

在 Stage A 完成 Food DNA 锁定与电影级商拍后，进入 Stage B 之前，必须先识别食品品类、菜系、品牌定位与情绪气质，再选择对应的专属 KV 视觉系统。

## Required Classification

输出至少包含：

```json
{
  "food_category": "",
  "cuisine_family": "",
  "brand_positioning": "",
  "visual_mood": [],
  "category_confidence": 0.0,
  "selected_visual_system": "",
  "fallback_level": "specific | family | generic"
}
```

## Priority

1. 用户明确提供的菜名 / 品类 / 品牌定位
2. 图片可见证据
3. 菜系与食材语义推断
4. 保守品类级 fallback

禁止因为模型偏好把未知甜点自动做成中式大金字，也禁止把未知热菜自动做成咖啡杂志风。

## Default Systems

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

## Confidence Rule

- >=0.85：使用具体品类视觉系统
- 0.60–0.84：使用品类家族视觉系统，减少地域符号
- <0.60：使用保守食品广告基础系统，避免强风格假设

## Non-negotiable

Category routing only changes the visual language. It must never alter the source food identity or override Stage A fidelity locks.
