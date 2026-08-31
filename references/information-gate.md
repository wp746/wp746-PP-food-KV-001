# Information Gate

本文件只解决：**执行B需要哪些上版文字、缺信息时怎么办、什么时候允许系统代写默认文案。**

## Default B Entry Gate

用户说 `B / 执行B` 后，正式进入 Stage B 设计前默认检查：

```text
HEADLINE = required
SUBTITLE = required
AUXILIARY_INFORMATION_COUNT >= 1
```

辅助信息可以是：品牌/店名、Slogan、卖点、核心食材、价格、净含量、地址、电话、活动信息或其他用户明确提供的真实商业信息。

## Missing Information Behavior

如果用户没有给够：

> **先提醒用户补 KV 上要出现的文字，只问最少缺失项。不要未经授权自动把所有缺失文案补完。**

示例：
- 有产品名 + 店名，但无主标题/副标题 → 提醒补主标题和副标题；
- 有主标题，无副标题 → 只问副标题；
- 主副标题都有但无辅助信息 → 只问 1 项辅助信息。

不要重复询问已经提供的信息。

## Default Copy Authorization

只有用户明确表达以下含义时，才进入 `DEFAULT_COPY_AUTHORIZED = TRUE`：

```text
按默认文案来
文案你来安排
剩下的文字你来写
按你判断补文案
```

此时允许：
- 产品名作为 headline；
- 生成非事实型 subtitle；
- 生成感官/传播型 slogan；
- 生成不冒充硬事实的安全卖点。

例如：

```text
现烤出炉
麦香浓郁
清甜多汁
冰爽解暑
茶香回甘
果香满溢
```

## Hard Facts Never Auto-Generated

即使 `DEFAULT_COPY_AUTHORIZED = TRUE`，仍禁止编造：

```text
电话
地址
价格
营业时间
产地
认证
奖项
品牌历史
官方背书
未确认食材
未确认口味
未确认制作工艺
医疗/健康功效
```

用户明确提供后才进入正式文案。

## COPY_ALLOWLIST

每个 B 任务建立当前任务 `COPY_ALLOWLIST`：
- 用户明确提供的产品名/品牌/店铺/地址/电话/价格/活动/卖点；
- 用户明确提供的 headline/subtitle/slogan；
- 用户授权默认文案后生成的安全软文案。

## COPY_BLOCKLIST

默认包含：
- 上一任务全部品牌、产品、地址、电话、Slogan、价格和硬事实；
- 当前用户未确认的商业事实；
- 当前图像无法可靠确认的食材/口味/工艺；
- 所有可能误导消费者的虚构事实。

## Information Density

信息少时：

```text
reduce information density
> ask minimum missing copy
> default copy only after authorization
> NEVER fabricate hard facts
```

视觉可以主动设计；商业事实不能主动发明。
