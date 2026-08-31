# PP-food-KV-001 Bootstrap Protocol

目标：跨智能体稳定复现 B，同时避免“为了防漏读而全仓库加载”造成品类串台、文字规则冲突和 Prompt 过载。

## 1. Bootstrap Triggers

首次安装/新会话、VERSION 变化、上下文压缩/恢复、A→B 能力未知、无法准确复述 P0 时重新执行。

## 2. Runtime Minimal Core｜正常生产必读

按顺序读取：

```text
1. VERSION
2. RUNTIME_MANIFEST.md
3. SKILL.md
4. SOP-B.md
5. HANDOFF.md
6. REQUIRED_READ_SET.md
7. PRE_FLIGHT_CHECKLIST.md
8. EXECUTION_CONTRACT_TEMPLATE.md
```

正常生产冷启动不要读取：

```text
tests/*
全部 references/*
全部 12 品类视觉系统正文
历史案例 / 旧对话总结
```

`tests/*` 只用于 Skill 开发、升级、审计和回归验证。

## 3. Authority

```text
P0 invariants              → RUNTIME_MANIFEST.md
B 操作流程                  → SOP-B.md
runtime / Stage A 能力      → HANDOFF.md
当前任务加载策略            → REQUIRED_READ_SET.md
生产门禁                    → PRE_FLIGHT_CHECKLIST.md
当前 B 合同                 → EXECUTION_CONTRACT_TEMPLATE.md
细节方法                    → references/（按当前任务）
开发/回归                   → tests/（非生产）
```

Stage A 的 Canonical SOP 来自 `PP-food-001/SOP-A.md`。

真实冲突未解决：`PRODUCTION_GATE = BLOCKED`。

## 4. Bootstrap Proof｜只证明关键不变量

必须确认：

```text
REPO_VERSION = <VERSION>
DEFAULT_ASPECT_RATIO = 9:16
EXPLICIT_A = STAGE_A_ONLY
B_REQUIRES_CURRENT_STAGE_A_PASS = TRUE
STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
PRODUCT_PRIORITY = 1
HEADLINE_PRIORITY = 2
TYPOGRAPHY_ACCURACY = 100%
PREVIOUS_SKIN_IMPORT = OFF
TRUE_UPPER_BOUND_CAN_REDESIGN_PRODUCT = FALSE
```

并能解释：
- B 为什么必须先真实完成当前任务 A；
- 为什么每个新任务重新 Category Route；
- “按默认文案来”只授权软文案，不授权硬事实；
- 标题可以强，但产品必须更强。

## 5. Context Budget｜防串台硬规则

正常生产：

```text
FULL_REPO_DUMP = FORBIDDEN
TESTS_IN_RUNTIME_CONTEXT = FORBIDDEN
ALL_12_CATEGORY_SKINS_ACTIVE = FORBIDDEN
PREVIOUS_JOB_SKIN_IMPORT = OFF
```

当前任务只激活：

```text
1 selected_visual_system
+ optional 1 weak auxiliary system
+ current typography rules
+ current information/layout rules if needed
```

IMAGE_MODEL 只接收：当前 Stage A PASS 图 + 当前 B 短合同 + 当前 B 短 Prompt。

## 6. Runtime Gate

完成 Bootstrap Proof 后运行 `PRE_FLIGHT_CHECKLIST.md`。

静态能力完整可进入 `READY_WAITING_FOR_START`。若完整 A→B 尚无真实证据，标注 `VERIFIED = PENDING`，第一笔真实 B 业务兼任验证。

用户说“启动”后进入 PRODUCTION。

## 7. Production Refresh｜每个 B 新任务

```text
new CURRENT_JOB_FACTS
→ current PP-food-001 Stage A
→ current Stage A QC PASS
→ refresh B P0
→ current Category Route
→ load B_JOB_CORE
→ load only current conditional refs
→ COPY_ALLOWLIST / COPY_BLOCKLIST
→ compact B Execution Contract
→ Stage B IMAGE_MODEL
→ QC
→ targeted retry
```

不要每张图完整 Bootstrap；只有版本/能力/上下文状态变化时才重新冷启动。
