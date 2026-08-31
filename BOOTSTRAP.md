# PP-food-KV-001 Bootstrap Protocol

本文件用于跨智能体冷启动与恢复，防止只读 `SKILL.md`、漏读 Stage A Bridge / Category / Typography / Upper-Bound / QC 后直接出 KV。

## 1. Bootstrap Triggers

以下任一情况必须重新执行：
- 首次 clone / 安装 / 加载；
- 新智能体或新会话；
- `VERSION` 变化；
- 上下文被压缩、重置或恢复；
- 无法准确复述当前 P0 规则；
- Stage A→Stage B 图片传递状态未知；
- 模型/凭据/视觉能力状态未知。

## 2. Mandatory Read Order

任何生产动作之前按顺序读取：

```text
1. VERSION
2. RUNTIME_MANIFEST.md
3. SKILL.md
4. SOP-B.md
5. HANDOFF.md
6. REQUIRED_READ_SET.md
7. PRE_FLIGHT_CHECKLIST.md
8. REQUIRED_READ_SET.md 的 COLD_START_ALWAYS_LOAD references
9. tests/runtime-handoff-tests.md
10. tests/test-cases.md
11. EXECUTION_CONTRACT_TEMPLATE.md
```

`SOP-B.md` 是执行B的 Canonical Operator SOP。它规定 B 的自然语言交互、信息门槛、Stage A Bridge、品类路由、Product Hero、Spatial Typography、True Upper-Bound、QC 与定向重试。

禁止：
- 自行跳过 `SOP-B.md`；
- 自行跳过 COLD_START_ALWAYS_LOAD；
- 用摘要代替正文；
- Mandatory Read 未完成就先生成一版；
- 用旧会话记忆替代当前仓库；
- 因上一张效果好而继承上一品类具体视觉皮肤。

## 3. Rule Authority

```text
P0 runtime invariants: RUNTIME_MANIFEST.md
Stage role / entrypoint: SKILL.md
B operator workflow: SOP-B.md
Runtime configuration: HANDOFF.md
Detailed methods: references/
Acceptance / regression: tests/
Current-job compilation: EXECUTION_CONTRACT_TEMPLATE.md
```

Stage A 的 Canonical Operator SOP 来自依赖仓库：

```text
PP-food-001/SOP-A.md
```

发现真实冲突：

```text
PRODUCTION_GATE = BLOCKED
```

指出冲突，不自行挑一个版本继续。

## 4. Bootstrap Proof

Mandatory Read 后必须准确确认：

```text
REPO_VERSION = <VERSION>
DEFAULT_ASPECT_RATIO = 9:16
DEFAULT_KV_MODE = TRUE_UPPER_BOUND
DEFAULT_INTENT_WITHOUT_BUSINESS_INFO = A
EXPLICIT_A_OVERRIDES_AUTO_B = TRUE
B_REQUIRES_STAGE_A_PASS = TRUE
STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
PRODUCT_PRIORITY = 1
HEADLINE_PRIORITY = 2
TYPOGRAPHY_ACCURACY = 100%
CATEGORY_SKIN_CONTAMINATION_ALLOWED = FALSE
LEGACY_ENTITY_CONTAMINATION_ALLOWED = FALSE
TRUE_UPPER_BOUND_CAN_REDESIGN_PRODUCT = FALSE
```

还必须能解释：
- `执行B` 为什么必须先真实完成当前任务 Stage A；
- B 信息不足时为什么只追问最少缺失项；
- 用户说“按默认文案来”时哪些软文案可以生成、哪些硬事实禁止编造；
- 只迁移方法，不迁移上一品类皮肤；
- 主标题、副标题、Slogan、辅助信息为什么必须形成完整空间文字系统；
- 标题可以强，但为什么 Product Hero 必须更强；
- 视觉上限与 Food Fidelity 冲突时怎么处理。

任一答不准 → 重读对应文件。

## 5. Runtime Gate

Bootstrap Proof 后执行 `PRE_FLIGHT_CHECKLIST.md`。

只有：

```text
BOOTSTRAP_READ = PASS
RUNTIME_CAPABILITIES = PASS
STAGE_A_DEPENDENCY = PASS
PRODUCTION_GATE = PASS
```

才允许：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

等待用户“启动”后进入 PRODUCTION。

## 6. Production Refresh

每个新 B 任务必须：

1. 刷新 `RUNTIME_MANIFEST.md`；
2. 刷新 `SOP-B.md`；
3. 新建 `CURRENT_JOB_FACTS`；
4. 按 `PP-food-001/SOP-A.md` 真实完成 Stage A 并取得当前任务 Stage A PASS 图；
5. 初步 Category Route；
6. 读取 `REQUIRED_READ_SET.md` 的 `B_JOB_ALWAYS_LOAD`；
7. 加载当前任务需要的 `CONDITIONAL_LOAD`；
8. 编译新的 B `EXECUTION_CONTRACT`；
9. Contract / Stage A reference / Copy Lists 未完成不得调用 Stage B IMAGE_MODEL。

长对话后无法证明 Cold-Start Core 或 `SOP-B.md` 仍在活跃上下文 → 重新 Bootstrap。