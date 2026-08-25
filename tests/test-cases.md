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
