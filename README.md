# PP-food-KV-001

高保真、跨品类、品类原生的 Stage B KV / Campaign Skill。

当前版本：**2.0.1**

## 目标

把 `PP-food-001` 的当前任务 Stage A PASS 图继续升级为 9:16 专业 KV，同时保持真实产品第一主角，并根据当前食品品类重新设计字体、背景、材质、空间、信息密度和 One Big Idea。

## V2.0 架构

跨智能体 fail-closed runtime protocol：

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

核心：B 必经 A、当前 Stage A PASS 为唯一 Stage B reference、每任务重新 Category Route、Previous Skin / Legacy Entity 隔离、Copy Allowlist / Blocklist、完整空间文字系统、TRUE_UPPER_BOUND 不改产品。

## V2.0.1 稳定性补丁

修正“没有真实 A→B 证据却把运行能力写成已验证”的问题：

```text
RUNTIME_CAPABILITIES_DECLARED
!=
RUNTIME_CAPABILITIES_VERIFIED
```

- 静态工具/schema/连接只能证明 `DECLARED = PASS`；
- 只有真实完整 A→B 链路成功，或匹配 `FULL_A_TO_B` verified Runtime Profile，才是 `VERIFIED = PASS`；
- 没有 profile 时可以 READY，但必须标记 `VERIFIED = PENDING` 与 `FIRST_LIVE_VERIFICATION_REQUIRED = TRUE`；
- 第一笔真实 B 业务兼任完整验证，不额外生成测试海报；
- 如果第一笔只有 A，只建立 `STAGE_A` scope evidence，不冒充完整 B 链路已验证；
- verified profile 存在宿主私有持久状态，配置 fingerprint 不变即可跨会话复用；
- 配置变化或实际读图/reference edit/A→B pass-through/QC 回读失败立即使 profile 失效；
- profile fingerprint 不得包含 API Key、Token、完整私有 URL 或用户凭据。

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

上限发生在当前品类自己的背景、字体人格、空间介质、材质、透视、光影、One Big Idea 和 Campaign Finish；不上限食物本体。

## 首次安装

从 `BOOTSTRAP.md` 开始。按 `HANDOFF.md` 配置视觉模型、参考图编辑模型、Credential 和 Stage A→B 图片传递能力；Pre-flight 的 Declared 能力完整后进入 READY，Verified 状态由 Runtime Profile 或首次真实业务链路决定。