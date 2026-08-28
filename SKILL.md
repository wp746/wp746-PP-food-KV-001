---
name: PP-food-KV-001
description: Use when a real food photo should become a category-native professional KV/campaign poster while preserving the exact product and routing typography, background, materials and layout to the current food category.
version: 2.0.1
---

# PP-food-KV-001 V2.0.1

## Mandatory Entry

**Do not start KV production from this file alone.**

Before routing, copy generation, prompt building or image generation:

```text
READ BOOTSTRAP.md
→ complete Mandatory Read Order
→ run PRE_FLIGHT_CHECKLIST.md
→ PRODUCTION_GATE must PASS
```

`RUNTIME_MANIFEST.md` is the canonical P0 runtime rule source. Old conversation memory, host defaults, summaries or a previous successful category skin must never weaken it.

## Role

本 Skill 是 **Stage B / Category-Native KV Engine**，但任何 B 请求都必须真实经过 Stage A：

```text
CURRENT USER IMAGE
→ PP-food-001 Stage A
→ Stage A QC
→ CURRENT JOB Stage A PASS IMAGE
→ current-category routing
→ B Execution Contract
→ Stage B IMAGE_MODEL
→ Product / Typography / Category / Upper-Bound QC
→ targeted retry
→ deliver
```

Stage B 不得回退原始随手拍，也不得使用上一任务图片。

## Runtime Protocol

必须使用：

- `BOOTSTRAP.md` — 冷启动、恢复、读取证明；
- `RUNTIME_MANIFEST.md` — A/B、9:16、Stage A Bridge、Product Hero、TRUE_UPPER_BOUND、Copy Truth、Capability Evidence、Fail-Closed 等 P0 规则；
- `REQUIRED_READ_SET.md` — `COLD_START_ALWAYS_LOAD / B_JOB_ALWAYS_LOAD / CONDITIONAL_LOAD`；
- `PRE_FLIGHT_CHECKLIST.md` — READY、Stage A dependency、Declared/Verified capability evidence 和 B 生产门禁；
- `EXECUTION_CONTRACT_TEMPLATE.md` — 每个 B 任务的当前产品、品类、文案与空间设计合同；
- `HANDOFF.md` — 运行模型、图片传递能力与 Runtime Profile。

不要把整仓库 Markdown 原样拼进 IMAGE_MODEL Prompt。规则先由 Agent 阅读，再编译成当前任务 `EXECUTION_CONTRACT`，最后生成短、明确、品类原生的 Stage B 指令。

## Capability Evidence Rule

必须区分：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS / BLOCKED
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING / BLOCKED
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

静态宿主能力不能冒充完整 A→B 已验证。没有匹配 `FULL_A_TO_B` verified profile 时，第一笔真实 B 任务兼任完整验证；不额外生成测试海报。若首次真实任务只有 A，只能建立 `STAGE_A` scope evidence，不能声称完整 B 链路 verified。

配置 fingerprint 不变时允许跨会话复用 verified profile。

## Category-Native Requirement

每个新任务必须重新路由当前食品品类。

可以迁移：Hero Product、透视、空间字体方法、前中后景、受控遮挡、层级、负空间、One Big Idea。

不能迁移上一任务具体皮肤：字体、标题材质、门头、牌匾、橱窗、丝带、灯箱、圆章、拱门、配色、道具、卖点模板、背景模板。

具体规则按 `REQUIRED_READ_SET.md` 加载对应 references。

## True Upper-Bound

Stage B 默认真正上限版，但定义与评分只以 `RUNTIME_MANIFEST.md` 和 `references/upper-bound-standard.md` 为准。

核心原则：

> **食物极度保守锁定；当前品类自己的背景与字体极度上限设计。**

标题可以强，但产品必须更强。主标题、副标题、Slogan、卖点和品牌/实用信息必须形成同一品类原生的完整空间文字系统。

## Copy Truth

每个 B 任务必须创建 `COPY_ALLOWLIST` 与 `COPY_BLOCKLIST`。

用户未提供的电话、地址、价格、食材、口味、制作工艺、认证、奖项、品牌历史等硬事实不得自动补齐。信息少时降低密度，不靠编造填满版面。

## Acceptance

必须执行 `tests/runtime-handoff-tests.md` 和 `tests/test-cases.md` 的行为约束。

Mandatory Read、Pre-flight、Stage A PASS reference、Category Route、Copy lists、Execution Contract 或 declared runtime ability 任一无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

禁止先出一版再补读规则。

## Security Boundary

仓库不得保存具体供应商名、私有聚合平台配置、实际 API Base URL、API Key、Token、私有模型凭据或 Runtime Profile 真实运行值。运行值由宿主 Secret / Environment / Connection / 私有持久状态提供。