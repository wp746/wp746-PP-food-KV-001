# PP-food-KV-001

高保真、跨品类、品类原生的 Stage B KV / Campaign Skill。

当前版本：**2.0.0**

## 目标

把 `PP-food-001` 的当前任务 Stage A PASS 图继续升级为 9:16 专业 KV，同时保持真实产品第一主角，并根据当前食品品类重新设计字体、背景、材质、空间、信息密度和 One Big Idea。

## V2.0 的重点

V2.0 解决“换一个智能体就漏读、串皮肤、跳 Stage A、主副标题变平、乱补商业信息”的问题。

新增 fail-closed runtime protocol：

```text
AGENTS.md
→ BOOTSTRAP.md
→ RUNTIME_MANIFEST.md
→ REQUIRED_READ_SET.md
→ PRE_FLIGHT_CHECKLIST.md
→ EXECUTION_CONTRACT_TEMPLATE.md
→ Stage A PASS
→ Category-Native Stage B
→ QC / targeted retry
```

核心变化：
- P0 规则只在 `RUNTIME_MANIFEST.md` 定义一次；
- Mandatory Read + 读取证明，不能只说“我读过了”；
- B 必须真实经过 Stage A；
- Stage B reference 只能是当前任务 Stage A PASS 图；
- 每个新食品重新 Category Route；
- 历史任务事实和上一品类视觉皮肤默认全部失效；
- 每个 B 任务先建立 `COPY_ALLOWLIST / COPY_BLOCKLIST` 与 Execution Contract；
- 信息不足时降低密度，不靠编造事实填满；
- 主标题、副标题、Slogan、卖点、品牌/Utility 形成完整品类原生空间文字系统；
- TRUE_UPPER_BOUND 默认开启，但绝不通过重做产品实现；
- Codex 可由根目录 `AGENTS.md` 自动进入 Bootstrap；
- 仓库不保存任何具体聚合平台、URL、Key 或私有模型配置。

## 用户入口

生产状态下：
- `A` → 只执行 Stage A；
- `B` → Stage A → QC → Stage A PASS → Stage B → QC；
- 未说 A/B 且无明显商业信息 → 默认 A；
- 未说 A/B 但给出产品/店铺/价格/地址/电话/主副标题/卖点等 → 自动 B，但仍先 A。

具体硬规则以 `RUNTIME_MANIFEST.md` 为准。

## 真正上限版

默认：

```text
KV_MODE = TRUE_UPPER_BOUND
```

上限发生在当前品类自己的：背景、字体人格、空间介质、材质、透视、光影、One Big Idea 和 Campaign Finish。

不上限食物本体。

## 首次安装

从 `BOOTSTRAP.md` 开始。按 `HANDOFF.md` 配置视觉模型、参考图编辑模型、Credential 和 Stage A→B 图片传递能力；Pre-flight 全部 PASS 后等待用户说“启动”。