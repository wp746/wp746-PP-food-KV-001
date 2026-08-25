# Information Gate

## PASS 条件

```text
headline != empty
subtitle != empty
valid_auxiliary_fields >= 1
```

辅助字段：store_name, brand_name, slogan, core_ingredients, flavor_highlight, selling_point, address, phone, reservation_phone, opening_hours, price, cuisine_type, campaign_info, other_business_info。

## 不足时

只询问最少缺失项，不重复索取已知信息。

示例：

- 只有图片 → 询问主标题、副标题，再任选 1 项辅助信息。
- 已有主标题 + 副标题 → 只再询问任意 1 项辅助信息。
- 已有主标题 + 地址 → 只询问副标题。

## 禁止编造

电话、地址、价格、营业时间、活动、认证、店史、奖项、原产地、每日现杀等商业事实不得自动生成。

## 可自动推断

菜系、风味、情绪、背景语义、摄影模式、字体性格、构图方向可以从图片和菜名推断，但不能冒充用户提供的事实。