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

## 3. Capability Evidence Levels

静态能力与真实验证必须分开：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS / BLOCKED
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING / BLOCKED
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

工具 schema、宿主说明和已配置连接只能证明 `DECLARED = PASS`。

完整双 Skill `VERIFIED = PASS` 需要：
- 真实读取当前用户图；
- 真实执行 Stage A reference edit；
- 真实回读 Stage A 输出并 QC；
- 真实把当前 Stage A PASS 图传给 Stage B；
- 真实回读 Stage B 输出并 QC；

或者存在与当前配置 fingerprint 匹配的 `FULL_A_TO_B` 已验证 Runtime Profile。

若没有真实证据，不得写“端到端已验证 / smoke tested”。

## 4. Runtime Profile Reuse

允许宿主把验证结果保存在**仓库之外的私有持久状态**：

```text
RUNTIME_PROFILE_SCHEMA = 1
RUNTIME_PROFILE_VERIFIED = TRUE / FALSE
RUNTIME_PROFILE_SCOPE = STAGE_A / FULL_A_TO_B
RUNTIME_PROFILE_FINGERPRINT = <opaque non-secret digest>
```

Fingerprint 只使用非秘密运行身份：模型标识、连接/路由身份、reference-edit 模式、Stage A→B pass-through 路由版本，以及必要时 API origin 的不可逆摘要。

禁止包含 API Key、Token、完整私有 URL 或用户凭据。

当前 fingerprint 匹配 `FULL_A_TO_B` verified profile：

```text
RUNTIME_PROFILE_FINGERPRINT_MATCH = TRUE
RUNTIME_CAPABILITIES_VERIFIED = PASS
FIRST_LIVE_VERIFICATION_REQUIRED = FALSE
```

无需每次新会话重复测试。

Profile 不存在或 fingerprint 不匹配：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

## 5. First Live Verification Without Waste

不额外生成测试海报。

若首次真实任务为 B，当前真实 B 任务本身完成 `FULL_A_TO_B` 验证；在最终交付前确认完整链路成功，再写入 verified profile。

若首次真实任务只有 A，只能形成 `STAGE_A` 级 evidence：不能因为 Stage A 成功就声称 Stage A→B 完整链路已验证。第一次真实 B 成功后再升级为 `FULL_A_TO_B`。

## 6. Generic Runtime Variables

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

## 7. Security Boundary

禁止提交到仓库：
- 具体供应商/聚合平台私有名称；
- 实际 API Base URL；
- API Key / Token；
- 用户账户或私有凭据；
- Runtime Profile 的真实值。

## 8. State Machine

Mandatory Read、Stage A dependency 或静态能力缺失：

```text
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```

Bootstrap Proof + Pre-flight + `RUNTIME_CAPABILITIES_DECLARED = PASS` 后可进入：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

但必须同时准确标注：

```text
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

等待用户说“启动”。之后进入 `PRODUCTION`。

## 9. Failure Recovery / Profile Invalidation

以下任一情况立即使 profile 失效并回 SETUP_GATE：
- VISION_MODEL 无法读原图或生成结果；
- IMAGE_MODEL 参考图编辑不可用；
- Credential 失效；
- Stage A 依赖缺失；
- Stage A PASS 图无法传给 Stage B；
- Stage B 输出无法被视觉 QC；
- 当前 fingerprint 与 verified profile 不匹配；
- 上下文压缩后无法证明 P0 规则仍在活跃上下文。

```text
RUNTIME_PROFILE_VERIFIED = FALSE
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```

只修复缺失项，不进入“降级但假装完整”的 B 流程。

## 10. Production UX

进入 PRODUCTION 后，用户只需上传图片、说 A/B 或提供产品名、店铺、价格、地址、电话、卖点等自然语言信息。

Agent 自动完成 A/B Router、Stage A、Stage B、Category Router、Copy Lists、Execution Contract 和 QC。