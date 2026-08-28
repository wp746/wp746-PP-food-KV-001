# PP-food-KV-001 Execution Contract Template

每个 B 任务在调用 Stage B IMAGE_MODEL 前，先把仓库规则编译成一个短、明确、当前任务专属的合同。用户不需要填写或看到内部字段。

## Contract

```text
JOB_MODE = B
ASPECT_RATIO = 9:16
KV_MODE = TRUE_UPPER_BOUND | USER_REQUESTED_LOWER_MODE

CURRENT_JOB_FACTS =
- user_visible_facts:
- user_explicit_business_facts:
- continuation_from_previous_job: NO unless user explicitly requests it

SOURCE_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
STAGE_A_QC = PASS

PRODUCT_LOCK =
- product / food identity:
- major ingredients:
- identity-defining geometry:
- visible count / arrangement:
- vessel / packaging:
- plating topology:
- sauce / oil / broth / cream / ice state:
- physical relationships:

CATEGORY_ROUTE =
- food_category:
- cuisine_family:
- brand_positioning:
- visual_mood:
- category_confidence:
- selected_visual_system:
- optional_weak_aux_system:

COPY_ALLOWLIST =
- exact product name:
- exact store / brand:
- exact headline if provided:
- exact subtitle if provided:
- exact address:
- exact phone:
- exact price:
- exact ingredients / selling points / campaign facts explicitly provided:

GENERATED_COPY_POLICY =
- product name may become headline if no headline is provided
- subtitle/slogan may be generated only as non-factual campaign language
- do not invent ingredients, flavor, process, origin, certification, price, address, phone, awards or history
- if facts are sparse, reduce information density instead of fabricating facts

COPY_BLOCKLIST =
- all previous-job brand/product/ingredient/flavor/address/phone/slogan/copy unless explicitly continued
- unsupported hard facts

PRODUCT_PRIORITY = 1
HEADLINE_PRIORITY = 2

TYPOGRAPHY_SYSTEM =
- headline personality / material / spatial medium:
- subtitle subordinate spatial medium:
- slogan / selling-point lower-volume medium:
- brand / utility placement:
- shared perspective / vanishing logic:
- occlusion limits:

CATEGORY_NATIVE_WORLD =
- background:
- materials:
- color:
- props:
- information density:
- negative style rules:

ONE_BIG_IDEA =
- one thumbnail-readable campaign concept:

TRUE_UPPER_BOUND =
- push background / typography / spatial medium / materials / perspective / lighting / campaign finish
- NEVER redesign product

FORBIDDEN =
- use raw user photo as Stage B reference after Stage A exists
- use previous-job image
- redesign food / packaging / vessel / plating
- add/remove/replace major ingredients
- import previous category skin without current-category justification
- let headline become visual priority #1
- keep subtitle/slogan/auxiliary copy as generic PPT-flat text while headline is spatial
- invent business facts
- random full regeneration after a targeted failure

FINAL_QC_REQUIRED = TRUE
TARGETED_RETRY_ONLY = TRUE
```

## Contract Compilation Rules

1. 先从当前 Stage A PASS 图提取 `PRODUCT_LOCK`，不能从上一任务记忆补全。
2. `CATEGORY_ROUTE` 每个新任务重新计算。
3. `COPY_ALLOWLIST` 只收当前用户事实；不确定就不进入 allowlist。
4. `COPY_BLOCKLIST` 默认包含上一任务所有实体和未确认硬事实。
5. `TRUE_UPPER_BOUND` 只增强当前品类自己的视觉语言。
6. Contract 完成后才生成 Stage B Prompt；不要把整仓库 Markdown 原样拼给 IMAGE_MODEL。

## Failure Mapping

```text
Stage A product drift → return Stage A, rebuild PRODUCT_LOCK after PASS
Product too small / headline dominates → Product Hero Retry
Headline/subtitle flat → Spatial Typography Retry
Wrong category skin → Category Router Retry
Previous skin/entity contamination → rebuild CURRENT_JOB_FACTS + category system + copy lists
Typography error → Typography Accuracy Retry
Unsupported copy → remove from COPY_ALLOWLIST and regenerate copy layer
Weak Big Idea → Upper-Bound Creative Retry without touching product
```

最多 3 次定向重试；硬门槛无法满足时不假装 PASS。