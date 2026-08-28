# PP-food-KV-001 Runtime / Handoff Regression Tests

这些测试定义 Stage B 跨智能体冷启动的硬行为。

## R01｜冷启动必须从 BOOTSTRAP 开始
PASS：优先读取 `BOOTSTRAP.md`，按 Mandatory Read Order 完成加载。
FAIL：只读 `SKILL.md` 摘要或只读少数 references 后直接出 KV。

## R02｜Cold-Start Core 不得选择性跳过
PASS：`REQUIRED_READ_SET.md` 中 `COLD_START_ALWAYS_LOAD` 全部读取，并完成读取证明。
FAIL：自行跳过 Stage A Bridge、Category Firewall、Product Hero、Upper-Bound、QC 或 Retry 核心规则。

## R03｜读取证明必须复述硬规则
Pre-flight 必须准确返回：当前 VERSION、默认 9:16、A/B 路由、B 必经 A、Stage B reference = 当前任务 Stage A PASS 图、Product > Headline、TRUE_UPPER_BOUND、Previous-Skin Contamination、Full Text-System Spatiality、Typography Accuracy = 100%。

## R04｜Mandatory Read 未完成则 Fail Closed
任一必读文件不可访问、未验证或只被摘要代替 → `PRODUCTION_GATE = BLOCKED`。

## R05｜Declared Capability 不等于 Verified Capability
宿主工具描述、schema、配置存在只能证明：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
```

若当前配置没有真实 A→B 端到端证据：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

FAIL：没有真实链路证据却写 `VERIFIED = PASS` 或声称 Stage A→B 已完成 smoke test。

## R06｜Declared 完整时可 READY，但必须标明验证级别
如果 Mandatory Read、Credential presence、Stage A dependency、reference-edit 路由和图片 pass-through 均可静态确认，可进入 READY。

若无匹配的 verified Runtime Profile，必须同时输出：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

`PRODUCTION_GATE = PASS` 只表示“可开始真实生产验证”，不等于已经端到端验证。

## R07｜首次真实 B 任务兼任端到端验证
当 profile 未验证时，用户启动后的第一笔真实 B 任务必须实际证明：
- VISION_MODEL 能读当前原图；
- Stage A IMAGE_MODEL 能接收当前原图 reference；
- Stage A 输出能被视觉 QC；
- 当前 Stage A PASS 图能真实传给 Stage B IMAGE_MODEL；
- Stage B 输出能被视觉 QC。

成功并在最终交付前完成后，才可：

```text
RUNTIME_CAPABILITIES_VERIFIED = PASS
RUNTIME_PROFILE_VERIFIED = TRUE
FIRST_LIVE_VERIFICATION_REQUIRED = FALSE
```

禁止为此额外生成无业务价值的测试海报。

## R08｜A 任务也可部分验证，但不能伪造 B 链路已验证
如果首次真实任务只是 A，可验证视觉读取、reference edit、Stage A 输出回读；但在 Stage A→B pass-through 尚无真实证据时，不得声称完整 B 链路 verified。

可记录 component-level evidence；完整双 Skill profile 只有实际 B 链路成功后才是 FULL VERIFIED。

## R09｜Verified Runtime Profile 可跨会话复用
profile 保存在宿主私有持久状态，禁止提交仓库。

当前非秘密配置 fingerprint 与 profile 匹配时：

```text
RUNTIME_PROFILE_FINGERPRINT_MATCH = TRUE
RUNTIME_CAPABILITIES_VERIFIED = PASS
FIRST_LIVE_VERIFICATION_REQUIRED = FALSE
```

新会话不得重复要求 smoke test。

## R10｜Fingerprint 只使用非秘密身份
可包含模型标识、连接槽/路由标识、reference-edit 路由模式、Stage A→B pass-through 版本、API origin 的不可逆摘要（如需要）。

禁止包含 API Key、Token、完整私有 URL 或用户凭据。

## R11｜配置变化使旧验证失效
视觉模型、图片模型、reference edit 路由、Stage A→B 路由或连接身份变化 → fingerprint mismatch：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

## R12｜真实生产失败立即使 profile 失效
任何已验证 profile 遇到读图、reference edit、Credential、Stage A→B pass-through、Stage B output readback 失败：

```text
RUNTIME_PROFILE_VERIFIED = FALSE
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```

不得继续复用旧 PASS。

## R13｜PP-food-001 依赖必须真实存在
PASS：B 路径能够真正执行 Stage A。
FAIL：声称“双 Skill”但没有 Stage A 或 Stage A 结果不能传入 Stage B。

## R14｜不允许猜图
宿主默认模型无视觉能力时，原图、Stage A 图和 Stage B 图均由 VISION_MODEL 读取/QC。

## R15｜仓库不得保存私有运行配置
FAIL：出现具体供应商名、私有聚合平台名、实际 API Base URL、API Key 或私有模型凭据。

## R16｜READY 后等待“启动”
配置与 Pre-flight 通过后输出 READY 状态和 capability evidence level，然后等待用户“启动”。

## R17｜启动后自然语言生产
进入 PRODUCTION 后用户只需上传图、说 A/B 或提供商业信息；不得要求用户理解内部 JSON、Visual System 或 Prompt。

## R18｜每个 B 任务必须完成 B Job Reads + Execution Contract
PASS：Stage A PASS 后读取 `B_JOB_ALWAYS_LOAD`，解析当前品类字体/空间系统，再建立当前任务 B Contract。
FAIL：冷启动读完后长期不刷新当前品类规则，或直接套上一任务皮肤。

## R19｜Stage A 输出必须传给 Stage B
FAIL：Stage B 回退到原始随手拍或上一任务图片。

## R20｜每个新任务必须重新路由品类
FAIL：因为上一张效果好，直接继承上一品类字体、背景、材质、配色、道具或信息模块皮肤。

## R21｜上下文压缩/恢复必须重新引导
如果智能体无法证明当前 `RUNTIME_MANIFEST.md` 与 P0 规则仍在活跃上下文，应重新 BOOTSTRAP / Pre-flight。

## R22｜连接失效回 SETUP_GATE
Key、模型、参考图编辑、视觉读取或 Stage A→B 传递失效时，退出 PRODUCTION，只修复缺失项。