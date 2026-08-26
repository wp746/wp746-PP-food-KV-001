# PP-food-KV-001｜安装交接与启动协议

本文件是跨智能体运行交接文档。新的智能体安装/加载本 Skill 后，应先完成运行环境配置，然后等待用户说 **“启动”**，再进入正常生产。

## 1. 依赖关系

`PP-food-KV-001` 是 Stage B KV 引擎，推荐与 `PP-food-001` 同时安装。

标准链路：

```text
用户原始随手拍
→ PP-food-001：Stage A 高保真电影级商拍
→ Stage A 输出图
→ PP-food-KV-001：Stage B 品类原生 KV
→ QC / 定向重试
```

如果 `PP-food-001` 未安装，应优先提醒用户安装/挂载；如果用户明确要求单独使用 KV Skill，也要说明高保真稳定性会下降。

## 2. 首次加载必须进入 SETUP_GATE

在运行状态未知时，不要直接出 KV。先告诉用户：

> 已加载 PP-food-KV-001。为了稳定执行“识图 → 锁 Food DNA → 商拍 → KV → QC”，请先配置视觉模型、图片模型和 API 连接。配置完成后你回复“启动”即可正常生产。

只收集/确认缺失项：

1. **VISION_MODEL**：负责识图、Food DNA、品类路由、信息判断和生成后 QC；
2. **IMAGE_MODEL**：负责参考图编辑、Stage A 商拍、Stage B KV 出图；
3. **API_BASE_URL**：聚合平台 / 模型服务 URL；
4. **API Key/Credential**：放入 Secret / Environment / Connection，不要求用户长期明文粘贴完整 Key；
5. **Reference Image Capability**：IMAGE_MODEL 支持上传参考图/image editing；
6. **Sequential Image Pass-through**：Stage A 输出能继续作为 Stage B 输入；
7. **Image Read Capability**：VISION_MODEL 能读取用户上传图和生成结果。

推荐环境变量名：

```text
PP_FOOD_API_BASE_URL
PP_FOOD_API_KEY
PP_FOOD_VISION_MODEL
PP_FOOD_IMAGE_MODEL
```

若宿主使用自己的 Connection/Secret 名称，可以映射，不强制变量名。

## 3. 模型职责

### VISION_MODEL
负责：
- 读取用户上传图片；
- Food DNA / Fidelity Manifest；
- `food_category` / `cuisine_family` / `scene_type` / `brand_positioning`；
- Category Visual Language Router；
- KV 信息门槛判断；
- Food Fidelity QC；
- Product Dominance QC；
- Category QC；
- Typography/布局的视觉复检（在模型能力允许范围内）。

如果宿主默认模型不识图，**禁止猜测图片内容**，必须调用 VISION_MODEL。

### IMAGE_MODEL
负责：
- Stage A：接收原始参考图并生成高保真电影级商拍；
- Stage B：接收 Stage A 输出参考图并生成 KV；
- 在 Prompt 约束下保持产品 DNA 与执行空间字体/品类视觉语言。

## 4. 能力自检

进入 READY 前至少确认：

```text
[ ] PP-food-001 已安装或明确允许降级运行
[ ] PP-food-KV-001 已加载
[ ] VISION_MODEL 可识图
[ ] IMAGE_MODEL 可接收参考图并编辑
[ ] API 凭据有效
[ ] Stage A 输出可传入 Stage B
[ ] 智能体可保存/读取生成图片
[ ] 智能体能读取 SKILL.md、HANDOFF.md、references/
```

如果某项不确定，智能体应帮助用户测试/确认，而不是直接宣称 READY。

## 5. READY → 启动

全部准备完成后，智能体必须回复类似：

> **PP Food 双 Skill 运行环境已准备就绪。视觉模型负责识图与 QC，图片模型负责参考图商拍和 KV。回复“启动”进入生产模式。**

状态：

```text
RUNTIME_STATE = READY_WAITING_FOR_START
```

收到用户“启动”：

```text
RUNTIME_STATE = PRODUCTION
```

进入生产后，用户只需正常大白话交流。

## 6. 生产模式自然语言示例

用户可以直接说：

> 这是一款欧丰园现烤的肥牛恰巴塔，主标题肥牛恰巴塔，副标题现烤出炉，一口满足，帮我出 KV。

后台自动：

```text
VISION_MODEL 识图
→ 信息门槛检查
→ PP-food-001 Stage A
→ IMAGE_MODEL 生成同一产品的电影级商拍
→ VISION_MODEL Fidelity QC
→ PP-food-KV-001 Category Router
→ IMAGE_MODEL Stage B KV
→ VISION_MODEL Product/Category/KV QC
→ 定向重试或交付
```

不要要求用户提供 JSON、Prompt、Visual System 名称或内部评分。

## 7. KV 信息门槛

正式 KV 默认要求：

```text
headline = required
subtitle = required
auxiliary_information_count >= 1
```

N 可以是：店名、品牌名、Slogan、核心食材、卖点、地址、电话、价格、营业信息、菜系或其他真实商业信息。

不足时只问最少缺失项，不重复问已经有的信息。

禁止编造电话、地址、价格、认证、品牌历史、奖项等硬事实。

## 8. Stage A 必须先于 Stage B

默认禁止：

```text
原始随手拍 → 一步激进 KV
```

标准：

```text
原始随手拍
→ Stage A 高保真商拍
→ Stage A 图作为 Stage B 唯一产品真相之一
→ KV
```

这是跨智能体稳定复现的关键。

## 9. IMAGE_MODEL Prompt 首段硬锁

Stage A 调用 IMAGE_MODEL 时，Prompt 前部必须包含同等强度规则：

> 以用户上传参考图为唯一产品真相。严格锁定原始食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑和物理关系。不得为了高级感重做、替换、增减或重新摆放主体。只升级灯光、环境、背景、景深、调色和商业摄影品质。

Stage B 还必须增加：

> 以 Stage A 商拍图中的产品为 Hero Product。产品必须始终是第一视觉主角。标题可以有厚度、透视、材质和空间张力，但不得把产品缩小、后退、遮挡或降为背景/摆设。调用当前食品品类自己的字体、空间、色彩、材质和信息密度系统。

## 10. 双 Skill 共用一套配置

如果两个 Skill 在同一智能体中运行，只需配置一次：
- VISION_MODEL
- IMAGE_MODEL
- API_BASE_URL
- API Credential

后续用户说“启动”后即可持续自然语言生产，不要每次重新走安装配置。

## 11. 连接失效时

如果 API Key 过期、模型名变化、图片接口不支持 reference image、VISION_MODEL 无法识图等，应退出 PRODUCTION：

```text
RUNTIME_STATE = SETUP_GATE
```

只提醒用户修复具体缺失项，修复后再次进入 READY，等待“启动”。
