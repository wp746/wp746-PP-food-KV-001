# PP-food-KV-001 Runtime / Handoff Regression Tests

这些测试定义 Stage B 跨智能体冷启动的硬行为。

## R01｜冷启动必须从 BOOTSTRAP 开始
PASS：优先读取 `BOOTSTRAP.md`，按 Mandatory Read Order 完成加载。
FAIL：只读 `SKILL.md` 摘要或只读少数 references 后直接出 KV。

## R02｜必读集不得选择性跳过
PASS：`REQUIRED_READ_SET.md` 中 ALWAYS_LOAD 全部读取，并完成读取证明。
FAIL：因为“当前是烘焙/饮品”就跳过 food-fidelity-bridge、product-hero、category-style-firewall、typography、upper-bound、retry、QC 或 tests。

## R03｜读取证明必须复述硬规则
Pre-flight 必须准确返回：
- 当前 VERSION；
- 默认 9:16；
- A/B 路由；
- B 必经 A；
- Stage B reference = 当前任务 Stage A PASS 图；
- Product > Headline；
- TRUE_UPPER_BOUND 的正确定义；
- Previous-Skin Contamination 判废；
- Full Text-System Spatiality；
- Typography Accuracy = 100%。

## R04｜Mandatory Read 未完成则 Fail Closed
任一必读文件不可访问、未验证或只被摘要代替 → `PRODUCTION_GATE = BLOCKED`。

## R05｜运行能力未确认则 Fail Closed
READY 前必须确认：VISION_MODEL、reference-image IMAGE_MODEL、Credential、Stage A→Stage B 图片传递、视觉读取生成结果。任一 UNKNOWN/MISSING → BLOCKED。

## R06｜PP-food-001 依赖必须真实存在
PASS：B 路径能够真正执行 Stage A。
FAIL：声称“双 Skill”但没有 Stage A 或 Stage A 结果不能传入 Stage B。

## R07｜不允许猜图
宿主默认模型无视觉能力时，原图、Stage A 图和 Stage B 图均由 VISION_MODEL 读取/QC。

## R08｜仓库不得保存私有运行配置
FAIL：出现具体供应商名、私有聚合平台名、实际 API Base URL、API Key 或私有模型凭据。

## R09｜READY 后等待“启动”
配置与 Pre-flight 通过后输出：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

等待用户“启动”。

## R10｜启动后自然语言生产
进入 PRODUCTION 后用户只需上传图、说 A/B 或提供商业信息；不得要求用户理解内部 JSON、Visual System 或 Prompt。

## R11｜每个 B 任务必须建立 Execution Contract
合同至少包含：CURRENT_JOB_FACTS、Stage A PASS reference、Category Route、Copy Allowlist、Copy Blocklist、Product Priority、TRUE_UPPER_BOUND、Forbidden。

## R12｜Stage A 输出必须传给 Stage B
FAIL：Stage B 回退到原始随手拍或上一任务图片。

## R13｜每个新任务必须重新路由品类
FAIL：因为上一张效果好，直接继承上一品类字体、背景、材质、圆章、门头、橱窗、配色或道具皮肤。

## R14｜上下文压缩/恢复必须重新引导
如果智能体无法证明当前 `RUNTIME_MANIFEST.md` 与 P0 规则仍在活跃上下文，应重新 BOOTSTRAP / Pre-flight。

## R15｜连接失效回 SETUP_GATE
Key、模型、参考图编辑、视觉读取或 Stage A→B 传递失效时，退出 PRODUCTION，只修复缺失项。