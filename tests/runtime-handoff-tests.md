# PP-food-KV-001 Runtime / Handoff Regression Tests

这些测试用于 **Skill 开发、升级和回归审计**，不是正常生产时的 Mandatory Runtime Read。

## R01｜冷启动从 BOOTSTRAP 开始
PASS：先读 `BOOTSTRAP.md`。
FAIL：只读 `SKILL.md` 摘要就出 KV。

## R02｜Runtime Minimal Core
正常生产冷启动只加载：

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

references 按当前任务条件加载；tests 不进入生产上下文。

## R03｜Tests = Development Only
仅在版本升级、Skill 审计、回归验证时读取 `tests/*`。

## R04｜B 必经 A
PASS：当前原图 → PP-food-001 Stage A → 当前 Stage A QC PASS → 当前 Stage A PASS 图 → Stage B。
FAIL：原始随手拍一步激进 KV；回退上一任务图。

## R05｜Current Job Isolation
上一任务的产品、品牌、地址、文案、品类皮肤、字体、背景、卖点模块默认全部失效。

## R06｜每个新任务重新路由
PASS：重新计算 current category / visual system。
FAIL：因为上一张效果好直接继承上一品类皮肤。

## R07｜Product Hero Priority
第一视觉主角必须是产品；Headline 第二。不得为了标题缩小、后退或遮挡产品。

## R08｜Full Text-System Spatiality
主标题、副标题、Slogan/卖点必须形成同一品类空间文字系统；不能只有主标题立体、其他像 PPT 平贴。

## R09｜Copy Truth
每个 B 任务建立 `COPY_ALLOWLIST / COPY_BLOCKLIST`。未确认电话、地址、价格、认证、奖项、历史、工艺、食材等硬事实不得编造。

## R10｜默认文案授权边界
用户说“按默认文案来”只授权非事实型传播/感官软文案，不授权新增硬事实。

## R11｜Category Style Firewall
只迁移方法，不迁移上一品类视觉皮肤。

## R12｜True Upper-Bound 不重做产品
上限发生在背景、字体、空间、材质、透视、光影和 Campaign Finish，不发生在 Food DNA / 包装 DNA。

## R13｜禁止整仓库 Prompt Dump
Agent 必须从当前合同编译短 Stage B Prompt；不得把 SOP、tests、全部 category references 原文塞给 IMAGE_MODEL。

## R14｜Conditional Reference Budget
只加载当前 `selected_visual_system`、当前 Typography 规则和必要的 0–2 个辅助 reference。不得一次加载全部 12 品类视觉皮肤。

## R15｜Declared != Verified
静态能力不等于真实 A→B 已验证。无真实证据时 `VERIFIED = PENDING`。

## R16｜首次真实 B 任务兼任验证
不额外生成测试海报；真实任务验证 original vision read、Stage A edit/readback、A→B pass-through、Stage B edit/readback。

## R17｜Typography Accuracy
用户提供的产品名、品牌、价格、地址、电话等只要错一字/数字即 FAIL。

## R18｜Targeted Retry Only
按 Food Drift / Product Demotion / Typography / Category / Copy / Density / Big Idea 定向重试，不随机整张重抽。

## R19｜连接失效 Fail Closed
VISION / IMAGE reference edit / Stage A dependency / A→B pass-through / Credential 失败 → 回 SETUP_GATE。
