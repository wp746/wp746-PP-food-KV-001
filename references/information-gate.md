# Information Gate

本文件只解决“哪些信息可以进入正式 KV、缺信息时怎么办”。不得通过补写硬事实来提高信息密度。

## Entry Logic

B 已被显式触发或由商业信息自动触发后，不要求用户必须懂“主标题/副标题/辅助字段”的内部结构。

最低可用条件：

```text
product_name OR explicit_headline OR user_identified_product != empty
```

如果用户明确说 B 但连产品身份/主标题都无法可靠确认，只询问**一个最少必要项**：产品名或希望使用的主标题。

## Headline

优先级：

```text
1. 用户明确主标题
2. 用户明确产品/菜名 → 直接作为 headline
3. 无法可靠确认 → 询问最少必要项
```

不得自行给未知产品起一个具体菜名。

## Subtitle / Slogan

如果用户已给副标题，必须 100% 准确使用。

如果未给，可以生成**非硬事实型传播文案**，但必须满足：
- 不新增食材；
- 不新增具体口味；
- 不新增制作工艺；
- 不新增产地、认证、奖项、店史；
- 不把推测写成用户事实。

用户说“新品”“纯手制”“可预定”等，只有当前消息明确提供时才能作为正式事实文案。

## Auxiliary Information

用户提供多少真实信息，就用多少；信息少时降低版面信息密度。

可用真实字段包括：

```text
store_name
brand_name
address
phone
reservation_phone
opening_hours
price
core_ingredients
selling_point
campaign_info
other_user_provided_business_info
```

**不再为了满足固定 N 值而编造辅助字段。**

## COPY_ALLOWLIST

每个 B 任务必须建立当前任务 `COPY_ALLOWLIST`：
- 用户明确提供的产品名/品牌/店铺/地址/电话/价格/活动/卖点；
- 当前图像能够可靠确认、且不会冒充商业事实的可见产品事实；
- 用户明确授权的标题/副标题。

不确定的信息不要进入 Allowlist。

## COPY_BLOCKLIST

默认包含：
- 上一任务所有品牌、产品名、食材、口味、地址、电话、Slogan；
- 未确认的食材/口味/制作工艺；
- 未确认的价格、地址、电话、营业时间、认证、奖项、原产地、店史和官方背书。

## Insufficient Information Strategy

优先顺序：

```text
reduce information density
> use safe non-factual campaign copy
> ask one minimum necessary fact
> NEVER fabricate hard facts
```

“剩下的你自己安排”只授权视觉设计和安全传播文案，不授权编造产品/商业事实。