# Category Visual Language QC

## Score

- Category Recognition Accuracy / 15
- Typography-Category Match / 15
- Spatial Language Match / 15
- Full Text-System Spatiality / 10
- Layout Bias Match / 10
- Color & Material Match / 10
- Information Density Match / 5
- Prop / Environment Relevance / 5
- Anti-template Distinctiveness / 5
- Product Dominance / 10

Total = 100

## Threshold

- >=90: strong category-native KV
- 85–89: acceptable but not true upper-bound
- 80–84: targeted retry
- <80: fail

## Product Dominance QC

所有品类都必须通过：
- 主产品是否仍是第一视觉主角；
- 是否因为主标题、副标题、Slogan 或空间字而缩小产品；
- 产品是否被推成背景、边角摆设或装饰物；
- 产品关键食欲区 / 包装识别区是否完整可见；
- 用户第一眼是否先感知产品，再阅读文字；
- 标题是否在服务产品，而不是利用产品当背景。

Product Dominance 低于 8/10，直接进入定向重试；若产品明确沦为次要视觉，直接 FAIL。

## Typography + Spatial Medium QC

必须同时检查：

1. 主标题字体人格是否属于当前食品品类；
2. 主标题的材质、厚度、透视、投影或附着关系是否属于当前品类；
3. 副标题是否与主标题形成空间层级，而不是普通平贴横排；
4. Slogan / 卖点 / 品牌信息是否仍在同一品类原生文字系统内；
5. 标题所依附的空间介质（门头、橱窗、包装纸、玻璃、丝带、菜单墙、吊牌等）是否能回答“为什么属于这个品类/品牌”；
6. 是否出现上一品类成功 KV 的字体、材质、圆章、门头、配色、道具直接继承。

如果只有主标题“做了设计”，副标题和辅助文字仍像 PPT 平贴层，True Upper-Bound 直接不通过。

## Mandatory Fail

无论总分多少，以下情况直接 FAIL：
- 蛋糕/甜点被做成中式饭馆大金字门头
- 烘焙/早餐被做成重黑金江湖毛笔门头、爆炒火焰或密集餐馆圆章
- 西餐被做成川湘热炒视觉
- 咖啡被做成家常菜四宫格卖点模板
- 包装商品产品文字/包装结构被改写
- 家常热菜被做成与食欲无关的冷感科技 KV
- 食品类别与标题/场景/字体语义明显错配
- 主标题属于当前品类，但副标题/卖点/徽章仍属于上一品类模板
- 当前任务明显继承上一任务的字体皮肤、场景皮肤、配色模板或卖点模块
- 为了放大标题，把主产品缩成背景或摆设
- 标题成为第一主角，产品只剩辅助作用
- 空间字或装饰结构遮挡产品关键食欲区 / 包装识别区
- 为了视觉张力改变 Food DNA / Packaging DNA

## Anti-template Test

问：如果把当前食物替换为另一完全不同品类，海报结构、字体皮肤、标题材质、空间介质、道具和信息模块是否几乎不需要变化？

若答案是“是”，则说明品类专属设计不足，需要重路由。

## Previous-Skin Contamination Test

问：

1. 上一张成功 KV 的字体能否直接复制到当前图？
2. 上一张的门头/橱窗/圆章/丝带/灯箱等具体结构是否被无理由沿用？
3. 上一张的配色与道具是否只是换了产品仍继续使用？
4. 当前所有视觉元素是否都能解释“为什么属于这道菜 / 这类产品 / 这个品牌”？

任何一项出现无依据继承，应判定 `CATEGORY_SKIN_CONTAMINATION = TRUE`，直接定向重试。

## Product Hero Test

问：
1. 去掉所有文字，当前产品是否仍然是一张强商拍主视觉？
2. 第一眼是否先看到产品？
3. 如果把标题缩小 15–20%，产品吸引力是否反而更合理？
4. 产品是否仍然是整个 KV 的视觉锚点？

若答案明显是否定，则进行 Product Hero 定向重试。

## True Upper-Bound Gate

要判定为真正上限版，必须同时满足：

```text
Food Fidelity = PASS
Product Dominance = PASS
Category Visual Language >= 90
Typography-Category Match >= 13/15
Spatial Language Match >= 13/15
Full Text-System Spatiality >= 9/10
CATEGORY_SKIN_CONTAMINATION = FALSE
```

任何一项不满足，都不能标记为 True Upper-Bound Ready。
