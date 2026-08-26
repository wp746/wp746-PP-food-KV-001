# PP-food-KV-001 Regression Tests

这些测试来自真实失败模式。任何版本升级都必须避免回归。

## Test 01｜Food DNA 必须先锁住
输入：真实美食随手拍 + 完整信息。
PASS：先生成同一份食物的电影级商拍；食材、器皿、摆盘高度一致。
FAIL：为了 KV 重做食物、换器皿或加高级配料。

## Test 02｜KV 不能只是“上字下菜”
PASS：标题参与空间，Food Hero 最近景，有明确纵深。
FAIL：顶部平贴大字 + 底部食物的宣传单结构。

## Test 03｜信息门槛
主标题 + 副标题 + 至少一个辅助字段才允许进入 KV。

## Test 04｜信息真实性
禁止编造电话、地址、认证、历史、奖项、每日现杀等硬事实。

## Test 05｜蛋糕甜点必须路由到 DESSERT_CAKE_SYSTEM
PASS：轻盈 editorial serif、奶油/玻璃/丝带等柔性空间语言、低中信息密度。
FAIL：金色毛笔字饭馆门头、油烟、深木川菜馆背景。

## Test 06｜咖啡茶饮必须路由到 COFFEE_TEA_SYSTEM
PASS：现代无衬线、Lifestyle 留白、玻璃/窗光、品牌感。
FAIL：四宫格家常菜卖点圆章、传统饭馆门头大金字。

## Test 07｜西餐必须路由到 WESTERN_DINING_SYSTEM
PASS：Fine Dining、refined serif、石材/银器/亚麻、克制层级。
FAIL：川湘红金、毛笔门头、火锅式热烈空间。

## Test 08｜家常热菜保持家常菜语义
PASS：烟火、锅气、食欲、暖材质、强中文标题。
FAIL：冷感甜品杂志、科技产品发布会。

## Test 09｜包装食品必须锁定包装 DNA
PASS：包装 Logo、文字、形状、材质和比例保持准确。
FAIL：把包装商品改成堂食菜或重画包装文字。

## Test 10｜Category Style Firewall
不同品类可以共享透视、空间字、Hero Product 等方法，但不能共享同一字体皮肤、场景皮肤、卖点模板。

## Test 11｜Category 70% + Brand Positioning 30%
同一蛋糕：bakery_editorial 与 youthful_trendy 可有差异，但都必须仍然像甜点 KV，而不是跨品类。

## Test 12｜低置信度保守路由
品类识别置信度 <0.60 时，减少强地域/品类符号，使用食品广告基础系统，不硬猜。

## Test 13｜Anti-template Test
把当前食物替换成完全不同品类后，如果字体、布局、材质、环境和信息结构几乎无需变化 → FAIL。

## Test 14｜Typography Accuracy
用户提供的主标题、副标题、地址、电话、价格等必须 100% 准确。

## Test 15｜二维码真实性
有真实二维码则锁定；无真实目标则仅预留 safe zone，不把 AI 随机矩阵当正式二维码。

## Test 16｜Product Hero Priority：标题不能压过产品
输入：任意美食品类 + 强主标题。
PASS：主产品仍是第一视觉主角；标题有设计张力但视觉权重第二；用户第一眼先感知产品，再读取文字。
FAIL：为了做大标题缩小产品、把产品推到远景/角落、把产品当作标题背景或摆设。

## Test 17｜甜点中的标题克制
输入：高级蛋糕 KV。
PASS：主标题可有材质和空间感，但蛋糕仍占据关键视觉区域，奶油纹理、层次、装饰第一时间可见。
FAIL：大片 serif / 装置字占据画面，蛋糕成为小道具。

## Test 18｜饮品中的 Product Hero
输入：咖啡 / 奶茶 / 果茶 KV。
PASS：杯体、液体、冰块/奶泡是视觉锚点，标题围绕产品建立生活方式场景。
FAIL：字体、Logo、留白成为绝对主角，饮品只是桌面小摆件。

## Test 19｜包装商品中的品牌字不能替代商品
PASS：包装盒/袋是第一购买锚点，品牌标题和卖点服务于包装展示。
FAIL：品牌大字占据大部分画面，真实商品缩小成为背景货架元素。

## Test 20｜Product Hero QA 强制失败条件
以下任意情况判 FAIL：
- 第一眼主要看到标题而不是产品；
- 产品关键食欲区/包装识别区被标题或装饰遮挡；
- 去掉产品后海报仍然像完整主视觉，而产品存在与否影响很小；
- 为了字体张力改变 Food DNA、器皿、包装结构。

## Test 21｜默认真正上限版不能改食物本体
输入：任意食品原图，用户未要求降级。
PASS：默认进入 TRUE_UPPER_BOUND，但 Food DNA、器皿、摆盘、可见数量与物理关系保持；上限设计主要发生在背景、空间、字体、材质、光影和排版。
FAIL：因为“真正上限版”重新造型、加减食材、重摆盘、改变包装/器皿或把产品变成另一道菜。

## Test 22｜上一品类视觉皮肤不得污染下一品类
输入 A：中式宽面 KV 成功使用厚金门头字、深木、圆章。
随后输入 B：烘焙贝果新品。
PASS：B 重新路由 BAKERY_BREAKFAST_SYSTEM，使用晨光、橱窗/包装纸/轻门店标牌、warm serif/clean sans，A 的毛笔金字/江湖门头/圆章不自动继承。
FAIL：B 只是把宽面换成贝果，视觉皮肤几乎不变。

## Test 23｜烘焙贝果专属上限版
输入：碱水原味贝果 + 烘焙连锁品牌 + 新品上市。
PASS：贝果原始造型、深琥珀色表皮、白色开口纹理、阵列关系保持；主标题具有 bakery-native 空间感，可用橱窗立体字/包装纸字/吊牌/晨光投影；副标题与新品信息使用从属空间介质；整体温暖、品牌级、生活方式而非餐馆江湖风。
FAIL：重黑金毛笔门头、爆炒火焰、密集圆章、传统饭馆视觉。

## Test 24｜主标题有设计但副标题平贴仍 FAIL
输入：任意真正上限版 KV。
PASS：Headline、Subtitle、Slogan、辅助信息形成完整空间文字系统，层级、材质、介质和视角匹配品类。
FAIL：只有主标题做成立体字，副标题/Slogan/卖点全部像 PPT 平贴字层。

## Test 25｜Typography Spatial Medium 必须属于当前品类
PASS：每个文字空间介质都能回答“为什么属于这类食品/品牌”。
FAIL：咖啡使用饭馆牌匾、烘焙使用川湘厚毛笔、甜点使用夜市灯箱等无语义依据的介质。

## Test 26｜Previous-Skin Contamination QC
如果当前结果沿用了上一任务的字体、门头、橱窗、圆章、丝带、灯箱、配色或道具模板，且当前品类没有独立理由支持 → `CATEGORY_SKIN_CONTAMINATION = TRUE` → FAIL。

## Test 27｜真正上限版 Full Text-System Gate
TRUE_UPPER_BOUND 必须同时满足：
- Food Fidelity PASS
- Product Dominance PASS
- Category Visual Language >=90
- Typography-Category Match >=13/15
- Spatial Language Match >=13/15
- Full Text-System Spatiality >=9/10
- CATEGORY_SKIN_CONTAMINATION = FALSE
任何一项不满足 → 不得标记 True Upper-Bound Ready。
