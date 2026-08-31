---
name: PP-food-KV-001
description: Use when a real food, beverage, bakery, or packaged-product photo should become a professional KV or campaign poster and product fidelity, category-native styling, copy accuracy, and cross-agent reproducibility matter.
version: 2.2.0
---

# PP-food-KV-001 V2.2.0

## Entry

Start with `BOOTSTRAP.md`.

Normal production uses the **Runtime Minimal Core** only. Do not load `tests/*`, all references, or all 12 category skins into production context.

Authority:

```text
P0 invariants        → RUNTIME_MANIFEST.md
B operator SOP       → SOP-B.md
runtime / A bridge   → HANDOFF.md
per-job reads        → REQUIRED_READ_SET.md
production gate      → PRE_FLIGHT_CHECKLIST.md
current B contract   → EXECUTION_CONTRACT_TEMPLATE.md
```

## Role

```text
CURRENT USER IMAGE
→ PP-food-001 current Stage A
→ Stage A QC PASS
→ CURRENT_STAGE_A_PASS_IMAGE
→ current Category Route
→ compact B Execution Contract
→ Stage B IMAGE_MODEL
→ QC
→ targeted retry
```

Stage B must never use the raw snapshot after current Stage A PASS exists, and must never use a previous-job image.

## Non-Negotiables

```text
B_REQUIRES_CURRENT_STAGE_A_PASS = TRUE
STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
PRODUCT_PRIORITY = 1
HEADLINE_PRIORITY = 2
TYPOGRAPHY_ACCURACY = 100%
PREVIOUS_JOB_SKIN_IMPORT = OFF
TRUE_UPPER_BOUND_CAN_REDESIGN_PRODUCT = FALSE
RETRY = TARGETED_NOT_RANDOM
```

## Execute B

When the user says `B / 执行B`:

1. complete current Stage A first;
2. inspect current copy;
3. if headline / subtitle / at least one auxiliary field is missing, ask only for the minimum missing copy;
4. only after explicit default-copy authorization may the agent generate missing soft campaign copy;
5. build `COPY_ALLOWLIST / COPY_BLOCKLIST`;
6. re-route the current food category;
7. activate only the current visual system + current typography rules;
8. build a compact current-job contract;
9. generate Stage B;
10. QC and targeted retry.

“按默认文案来 / 文案你来安排” may authorize non-factual headline/subtitle/slogan/sensory copy, but never authorizes invented phone numbers, addresses, prices, certifications, awards, origin, process, history or unverified ingredients.

## Product Hero + Category-Native Rule

Transfer methods, never previous skin.

Allowed to transfer: Hero Product, perspective, spatial typography method, depth, controlled occlusion, hierarchy, negative space, One Big Idea.

Do not automatically transfer: fonts, title material, signboard, arch, ribbon, lightbox, badges, palette, props, information modules, background skin.

Headline can be strong; product must remain stronger.

## Anti-Drift Runtime Rule

Every new image creates new `CURRENT_JOB_FACTS` and a new Category Route.

IMAGE_MODEL receives only:

```text
current Stage A PASS image
+ compact current B contract
+ compact current B prompt
```

Never send the whole repository or all category examples to IMAGE_MODEL.

## Fail Closed

If current Stage A PASS is missing, current category is unresolved, copy lists are missing, VISION/IMAGE/pass-through/credential capability is unavailable, the contract is contaminated/incomplete, or a P0 conflict is unresolved:

```text
PRODUCTION_GATE = BLOCKED
```

## Security

Never store real API keys, private provider configuration, private base URLs, or user credentials in the repository.
