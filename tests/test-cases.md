# PP-food-KV-001 Regression Tests

这些测试只保留直接影响稳定生产的失败模式，并避免把历史真实项目词或某几个品类皮肤反复注入冷启动上下文。

## Test 01｜显式 A
输入：用户说 A。
PASS：只执行 Stage A 商拍。
FAIL：因为同时给了产品名/店铺信息而自动进入 KV。

## Test 02｜显式 B 必经 A
输入：用户说 B。
PASS：原图 → Stage A → Stage A QC → Stage A PASS 图 → Stage B。
FAIL：直接用原始随手拍做 KV。

## Test 03｜默认 A
输入：用户只上传美食图，未说 A/B，无明显商业信息。
PASS：默认 Stage A。

## Test 04｜商业信息自动 B
输入：未说 A/B，但提供产品名、店铺、主副标题、地址、电话、价格、核心食材、卖点或新品/活动信息。
PASS：自动判 B，并先走完整 Stage A。

## Test 05｜9:16 全局输出
输入：横图 / 方图 / 竖图。
PASS：KV 最终均为 9:16，产品关键区域完整。
FAIL：为竖版拉伸、压缩、裁坏或重做产品。

## Test 06｜Stage A Food DNA Gate
PASS：Food >=95、Vessel >=98、Plating/Physical Relationship >=95 后才能进入 Stage B。
FAIL：Stage A 漂移但仍继续做 KV。

## Test 07｜Stage B reference lock
PASS：Stage B reference 只使用当前任务 `STAGE_A_PASS_IMAGE`。
FAIL：回退原图、引用上一任务图片或用文字描述代替实际参考图。

## Test 08｜Current Job Isolation
上一任务含 `LEGACY_PRODUCT_X / LEGACY_BRAND_X / LEGACY_COPY_X`；当前任务为 `CURRENT_PRODUCT_Y`。
PASS：当前 KV 不出现任何 legacy entity。
FAIL：上一任务事实、文案或品牌混入当前任务。

## Test 09｜B Execution Contract
PASS：Stage B 生成前合同至少包含：

```text
JOB_MODE = B
ASPECT_RATIO = 9:16
CURRENT_JOB_FACTS
STAGE_A_PASS_IMAGE = REQUIRED
CATEGORY_ROUTE
COPY_ALLOWLIST
COPY_BLOCKLIST
PRODUCT_PRIORITY = 1
HEADLINE_PRIORITY = 2
TRUE_UPPER_BOUND
FORBIDDEN
```

FAIL：未建立合同就直接让 IMAGE_MODEL 自由解释仓库。

## Test 10｜每个新任务重新 Category Route
输入：连续两个明显不同的食品品类 A → B。
PASS：B 重新确定字体人格、空间介质、背景、材质、配色、道具和信息密度。
FAIL：B 只换产品，仍继承 A 的具体视觉皮肤。

## Test 11｜Method vs Skin
PASS：可迁移 Hero Product、透视、空间字体方法、层级、负空间、One Big Idea。
FAIL：直接迁移上一任务字体、门头/橱窗/灯箱/丝带/圆章、配色、道具或背景模板。

## Test 12｜Product Hero
PASS：第一眼先看到产品，再读标题。
FAIL：标题成为第一主角、产品退到远景/角落或被空间字遮挡。

## Test 13｜Headline Category Match
PASS：主标题的字体人格、材质、厚度、透视和空间介质能解释“为什么属于当前品类/品牌”。
FAIL：只靠放大、描边或通用 3D 效果冒充高级。

## Test 14｜Subtitle / Auxiliary Spatiality
PASS：Subtitle 明显从属主标题，Slogan/卖点/品牌/Utility 继续降级但仍属于同一品类空间语法。
FAIL：只有主标题有设计，其余文字像 PPT 平贴字层。

## Test 15｜Full Text-System Spatiality
TRUE_UPPER_BOUND 必须让 Headline / Subtitle / Slogan / Brand / Utility 形成完整层级与统一空间逻辑。

## Test 16｜Typography Accuracy
用户提供的产品名、品牌、主副标题、地址、电话、价格、活动文字必须 100% 准确。
任何错字、乱码、数字错误 → FAIL。

## Test 17｜商业事实安全
PASS：产品名可作为 headline；缺 subtitle 时可用非硬事实传播文案；信息少时降低密度。
FAIL：为了填版面编造食材、口味、价格、地址、电话、认证、品牌历史、奖项、原产地、制作工艺或官方背书。

## Test 18｜Anti-template Test
把当前食品替换成完全不同品类，如果字体、背景、材质、道具和信息结构几乎无需变化 → FAIL。

## Test 19｜TRUE_UPPER_BOUND 不改产品
PASS：上限发生在背景、空间、字体、材质、光影、One Big Idea、Campaign Finish。
FAIL：加减食材、换器皿、重摆盘、重做产品造型或包装。

## Test 20｜保真与上限冲突
PASS：降低标题/背景/空间激进度，保留 Food DNA。
FAIL：为了上限设计牺牲产品真相。

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
PASS：Food Drift 回 Stage A；Product Demotion → Product Hero Retry；标题系统平 → Spatial Typography Retry；品类串台 → Category Router Retry；旧皮肤污染 → 重建当前品类系统；文字错误 → Typography Accuracy Retry。
FAIL：随机整张重抽导致已经正确的产品或文字再次漂移。

## Test 23｜Fail Closed
Mandatory Read、Pre-flight、Stage A PASS reference、Category Route、Copy Lists 或当前 B Contract 任一无法确认 → 不得调用 Stage B IMAGE_MODEL。