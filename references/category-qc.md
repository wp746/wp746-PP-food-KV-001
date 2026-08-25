# Category Visual Language QC

## Score

- Category Recognition Accuracy / 20
- Typography-Category Match / 15
- Spatial Language Match / 15
- Layout Bias Match / 10
- Color & Material Match / 10
- Information Density Match / 10
- Prop / Environment Relevance / 10
- Anti-template Distinctiveness / 10

Total = 100

## Threshold

- >=90: strong category-native KV
- 85–89: acceptable
- 80–84: targeted retry
- <80: fail

## Mandatory Fail

无论总分多少，以下情况直接 FAIL：
- 蛋糕/甜点被做成中式饭馆大金字门头
- 西餐被做成川湘热炒视觉
- 咖啡被做成家常菜四宫格卖点模板
- 包装商品产品文字/包装结构被改写
- 家常热菜被做成与食欲无关的冷感科技 KV
- 食品类别与标题/场景/字体语义明显错配

## Anti-template Test

问：如果把当前食物替换为另一完全不同品类，海报结构和视觉皮肤是否几乎不需要变化？

若答案是“是”，则说明品类专属设计不足，需要重路由。
