# PP-food-KV-001

高保真、跨品类、品类原生的 Stage B KV / Campaign Skill。

当前版本：**2.2.0**

## 这版解决什么

V2.2.0 专门针对“Skill 拉到其他智能体后越调越漂”的问题做运行时减法：

- 正常生产不再加载 tests 和全部 references；
- 不再同时激活 12 个品类视觉皮肤；
- 每个新任务重新 Category Route；
- 上一任务字体、背景、门头、丝带、圆章、配色、卖点模块默认失效；
- Stage B Contract 压缩为当前产品、当前品类、当前文案、当前空间文字系统、One Big Idea、Hard Negatives 六块；
- IMAGE_MODEL 只接收当前 Stage A PASS 图 + 当前短合同 + 当前短 Prompt。

核心原则：

> **只迁移方法，不迁移上一张的皮肤。少而明确的当前任务规则，优先于大而全的仓库提示词。**

## Runtime Minimal Core

新智能体从 `BOOTSTRAP.md` 开始，正常生产只加载：

```text
VERSION
RUNTIME_MANIFEST.md
SKILL.md
SOP-B.md
HANDOFF.md
REQUIRED_READ_SET.md
PRE_FLIGHT_CHECKLIST.md
EXECUTION_CONTRACT_TEMPLATE.md
```

`tests/*` 只用于开发/升级/回归，不进入正常 KV 生成上下文。

## 执行B

标准链路：

```text
CURRENT USER IMAGE
→ PP-food-001 Stage A
→ CURRENT Stage A QC PASS
→ CURRENT Stage A PASS IMAGE
→ current Category Route
→ COPY_ALLOWLIST / COPY_BLOCKLIST
→ Compact B Contract
→ Stage B IMAGE_MODEL
→ QC
→ targeted retry
```

B 不得回退原始随手拍，不得使用上一任务图片。

## 文案边界

- 产品名可以成为 headline；
- 缺 subtitle 时可生成非事实型传播副标题；
- 用户说“按默认文案来”只授权感官/传播软文案；
- 未确认电话、地址、价格、认证、奖项、工艺、产地、品牌历史等不得编造。

## Product Hero

```text
1. PRODUCT / FOOD HERO
2. HEADLINE
3. SPATIAL CONCEPT
4. SUBTITLE
5. SLOGAN / SELLING POINTS
6. BUSINESS / UTILITY
```

标题可以强，但产品必须更强。

## Category-Native

当前任务只激活：

```text
1 primary visual system
+ optional 1 weak auxiliary system
+ current typography rules
```

禁止全 12 品类同时进入当前 Prompt。

## True Upper-Bound

上限发生在当前品类自己的背景、字体人格、空间介质、材质、透视、光影、One Big Idea 和 Campaign Finish；不上限产品本体。

## Security

仓库不保存真实 API Key、私有 Base URL、私有供应商配置或用户凭据。
