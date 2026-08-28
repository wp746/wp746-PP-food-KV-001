# PP-food-KV-001 Runtime Handoff

本文件只负责 **Stage B 运行环境、Stage A 依赖与图片传递能力**。设计、品类、字体和上限规则由 `RUNTIME_MANIFEST.md` / `references/` 管理。

## 1. Start Here

新的智能体必须先读：

```text
BOOTSTRAP.md
```

Bootstrap 完成后才进行本文件能力检查。

## 2. Required Runtime Capabilities

只确认缺失项：

1. `VISION_MODEL`
   - 能读取用户原图；
   - 能读取 Stage A PASS 图；
   - 能读取 Stage B 生成结果；
   - 用于 Food DNA、Category Router、Typography/Product/QC。

2. `IMAGE_MODEL`
   - 必须支持 reference image / image editing / image-to-image；
   - Stage A 能实际接收用户原图；
   - Stage B 能实际接收 Stage A PASS 图。

3. Stage A Dependency
   - `PP-food-001` 可被真实执行；
   - Stage A QC 可判断 PASS/FAIL；
   - Stage A PASS 图能继续传给 Stage B。

4. Credential / Connection
   - 凭据已配置在宿主 Secret / Environment / Connection；
   - 普通对话只确认状态，不回显完整 Key。

5. Output Pass-through
   - Stage B 输出能被 Agent / VISION_MODEL 读取并 QC。

## 3. Generic Runtime Variables

宿主可自行映射，例如：

```text
VISION_MODEL
IMAGE_MODEL
API_BASE_URL
API_KEY
REFERENCE_IMAGE_EDIT
STAGE_A_TO_STAGE_B_PASS_THROUGH
```

这里只定义接口，不保存真实值。

## 4. Security Boundary

禁止提交到仓库：
- 具体供应商/聚合平台私有名称；
- 实际 API Base URL；
- API Key / Token；
- 用户账户或私有凭据。

## 5. State Machine

能力未知/缺失：

```text
RUNTIME_STATE = SETUP_GATE
```

Bootstrap Proof + Pre-flight + Stage A dependency + Runtime Capabilities 全部通过：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

等待用户说“启动”。之后：

```text
RUNTIME_STATE = PRODUCTION
```

进入 PRODUCTION 后不重复询问模型配置，除非连接失效。

## 6. Failure Recovery

以下任一情况立即退回 SETUP_GATE：
- VISION_MODEL 无法读原图或生成结果；
- IMAGE_MODEL 参考图编辑不可用；
- Credential 失效；
- Stage A 依赖缺失；
- Stage A PASS 图无法传给 Stage B；
- Stage B 输出无法被视觉 QC；
- 上下文压缩后无法证明 P0 规则仍在活跃上下文。

只修复缺失项，不进入“降级但假装完整”的 B 流程。

## 7. Production UX

进入 PRODUCTION 后，用户只需：
- 上传图片；
- 说 A / B；
- 或提供产品名、店铺、价格、地址、电话、卖点等自然语言信息。

Agent 自动完成 A/B Router、Stage A、Stage B、Category Router、Copy Lists、Execution Contract 和 QC。