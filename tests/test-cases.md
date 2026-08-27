# PP-food-KV-001 Regression Tests

这些测试只保留直接影响稳定生产的真实失败模式。

## Test 01｜显式 A
输入：用户说 A。
PASS：只执行 Stage A 商拍。
FAIL：因为用户同时给了产品名/店铺信息而自动进入 KV。

## Test 02｜显式 B 必经 A
输入：用户说 B。
PASS：原图 → Stage A → Stage A QC → Stage A PASS 图 → Stage B。
FAIL：直接用原始随手拍做 KV。

## Test 03｜默认 A
输入：用户只上传美食图，未说 A/B，无明显商业信息。
PASS：默认 Stage A。

## Test 04｜商业信息自动 B
输入：未说 A/B，但提供产品名、店铺、主副标题、地址、电话、价格、核心食材、卖点或新品信息。
PASS：自动判 B，并先走完整 Stage A。

## Test 05｜9:16 全局输出
输入：横图 / 方图 / 竖图。
PASS：KV 最终均为 9:16，产品关键区域完整。
FAIL：为竖版拉伸、压缩或重做产品。

## Test 06｜Stage A Food DNA Gate
PASS：Food >=95、Vessel >=98、Plating/Physical Relationship >=95 后才能进入 Stage B。
FAIL：Stage A 漂移但仍继续做 KV。

## Test 07｜Current Job Isolation
上一任务：泡菜米线；当前任务：宽面/贝果/饮品。
PASS：当前 KV 不出现上一任务品牌、米线、泡菜、酸萝卜、Slogan 等旧事实。
FAIL：任何旧实体污染当前任务。

## Test 08｜视觉皮肤不得串台
上一任务：中式宽面使用厚金门头字、深木、圆章。
当前任务：烘焙贝果。
PASS：重新路由 BAKERY_BREAKFAST_SYSTEM；上一任务皮肤不继承。
FAIL：只换产品，字体/背景/圆章结构几乎不变。

## Test 09｜蛋糕甜点
PASS：editorial serif / elegant sans、奶油/玻璃/丝带等轻盈空间语言。
FAIL：饭馆金色毛笔门头、油烟、深木江湖风。

## Test 10｜咖啡茶饮 / 水果饮品
PASS：现代无衬线、玻璃/窗面/透明空间字、自然光、Lifestyle 留白；杯体/水果主体第一。
FAIL：中式大金字、家常菜圆章模板、重油重火背景。

## Test 11｜烘焙早餐
PASS：warm serif / friendly sans / subtle handwritten，晨光、橱窗、包装纸、吊牌、烘焙材质。
FAIL：川湘毛笔金字、爆炒火焰、饭馆江湖门头。

## Test 12｜面食粉类
PASS：面食自己的纵向节奏、拉伸/上升动线、主食力量；产品造型仍完全锁定。
FAIL：为了“上限”改变面条宽度、堆叠、酱料或器皿。

## Test 13｜Product Hero
PASS：第一眼先看到产品，再读标题。
FAIL：标题成为第一主角、产品退到远景/角落或被空间字遮挡。

## Test 14｜主标题空间感
PASS：标题材质、厚度、透视和空间介质与当前品类一致。
FAIL：只用放大、描边或统一 3D 金字冒充高级。

## Test 15｜副标题不能平贴
PASS：Subtitle 明显从属主标题，并使用该品类合理的吊牌/纸带/玻璃字/菜单条/标签等空间介质。
FAIL：主标题有设计，副标题/Slogan/卖点像 PPT 平贴字层。

## Test 16｜Full Text-System Spatiality
TRUE_UPPER_BOUND 必须让 Headline / Subtitle / Slogan / Brand / Utility 形成完整层级系统，而不是多行同平面排版。

## Test 17｜Typography Accuracy
用户提供的产品名、品牌、主副标题、地址、电话、价格、活动文字必须 100% 准确。
任何错字、乱码、数字错误 → FAIL。

## Test 18｜商业事实安全
PASS：可用用户事实创作文案，但不冒充事实。
FAIL：编造食材、口味、价格、地址、认证、品牌历史、奖项、原产地或官方背书。

## Test 19｜Anti-template Test
把当前食品替换成完全不同品类，如果字体、背景、材质、道具和信息结构几乎无需变化 → FAIL。

## Test 20｜TRUE_UPPER_BOUND 不改产品
PASS：上限发生在背景、空间、字体、材质、光影、One Big Idea、Campaign Finish。
FAIL：加减食材、换器皿、重摆盘、重做产品造型。

## Test 21｜最终硬门槛

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

任意硬门槛不满足 → 不得标记 True Upper-Bound Ready。

## Test 22｜Targeted Retry
PASS：Food Drift 回 Stage A；标题平 → Spatial Typography Retry；品类串台 → Category Router Retry；旧皮肤污染 → 重建当前品类系统；文字错误 → Typography Accuracy Retry。
FAIL：随机整张重抽导致已经正确的产品或文字再次漂移。
