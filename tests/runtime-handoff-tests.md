# PP-food-KV-001 Runtime / Handoff Regression Tests

## Test R01｜首次加载进入 SETUP_GATE

条件：新智能体首次安装或运行状态未知。

PASS：先读取 `HANDOFF.md`，确认 VISION_MODEL、IMAGE_MODEL、API_BASE_URL、Credential、参考图编辑能力和 Stage A→Stage B 图片传递能力。

FAIL：安装后直接进入 KV 生成。

## Test R02｜PP-food-001 依赖检查

PASS：优先检测/加载 `PP-food-001`；缺失时提醒安装或明确进入降级模式。

FAIL：一边声称执行双 Skill，一边实际上没有 Stage A。

## Test R03｜默认文本模型禁止猜图

PASS：宿主默认模型无视觉时，上传图必须交给 VISION_MODEL。

FAIL：通过文件名、用户描述或常识推测图片构图并直接路由。

## Test R04｜双模型角色不混淆

PASS：VISION_MODEL 负责识图/路由/QC；IMAGE_MODEL 负责参考图编辑与最终出图。

FAIL：把“IMAGE_MODEL 能看参考图”理解成不需要前置路由和后置 QC。

## Test R05｜Stage A 输出必须传给 Stage B

PASS：Stage B IMAGE_MODEL 输入参考图是 Stage A 商拍结果。

FAIL：Stage B 重新用原始随手拍，导致 Food DNA 和商业质感不稳定。

## Test R06｜配置完成后等待“启动”

PASS：状态为 `READY_WAITING_FOR_START`，明确提示用户回复“启动”。

FAIL：未收到“启动”就自动生产。

## Test R07｜“启动”后进入自然语言生产

PASS：用户说“启动”后切换 `PRODUCTION`，用户可用大白话上传照片和信息。

FAIL：要求用户提供内部 JSON、Visual System 名称或 Prompt。

## Test R08｜KV 信息门槛

PASS：headline + subtitle + N≥1 才进入 Stage B；缺失时只追问最少项。

FAIL：信息不足时编造店名、地址、电话、价格或 Slogan 事实。

## Test R09｜Stage A Prompt Hard Lock

PASS：明确锁定食物、主要食材几何、器皿/包装、摆盘与物理关系。

FAIL：只写“保持原图风格”。

## Test R10｜Stage B Product Hero Lock

PASS：明确要求产品第一视觉主角，标题可有厚度/透视/空间张力但不得把产品缩小、后退或当背景。

FAIL：为了主标题视觉冲击让产品变成小摆设。

## Test R11｜Category Router 依赖视觉分析

PASS：VISION_MODEL 判断 food_category / cuisine_family / positioning，再进入品类系统。

FAIL：所有食品默认用同一套中式大字海报。

## Test R12｜连接失效自动退出生产

条件：Key 失效、模型名无效、参考图端点不可用或 VISION_MODEL 不能读图。

PASS：切回 `SETUP_GATE`，只提示修复具体缺失项。

FAIL：继续假装生成流程正常。
