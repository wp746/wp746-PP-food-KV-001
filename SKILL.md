---
name: PP-food-KV-001
description: Use when a user provides a real food photo and wants a professional restaurant, dessert, beverage, western-dining, bakery, packaged-food, or other food-category KV/campaign poster built from that exact food with supplied headline/subtitle/business information.
---

# PP-food-KV-001

## Core Principle

**Preserve the food → upgrade the photography → identify the food category → build a category-native KV.**

The skill must never turn every food into the same Chinese home-style poster.

## Entry Gate

Do not enter KV design until:
- headline: required
- subtitle: required
- auxiliary information count >=1

Ask only for the minimum missing information. Never invent factual business data.

## Stage A｜Food Fidelity First

Before KV styling, lock the source food as product truth using `PP-food-001`-style fidelity constraints:
- Food Identity >=95%
- Ingredient Geometry >=95%
- Vessel/Container Identity >=98%
- Plating Topology >=95%
- Physical Relationship Fidelity >=95%

First make the exact food look like a cinematic studio-grade commercial photograph. Background, lighting and environment may change; food DNA may not.

## Stage B｜Category Visual Language Routing

Before creative direction, classify:
- `food_category`
- `cuisine_family`
- `brand_positioning`
- `visual_mood`
- routing confidence

Then select one primary visual system from `references/category-visual-systems.md` using `references/category-router.md`.

Default systems:
- CN_HOME_STYLE_SYSTEM
- SPICY_HOT_SYSTEM
- CLAYPOT_SOUP_SYSTEM
- NOODLE_RICE_NOODLE_SYSTEM
- BBQ_NIGHTMARKET_SYSTEM
- SEAFOOD_PREMIUM_SYSTEM
- DESSERT_CAKE_SYSTEM
- COFFEE_TEA_SYSTEM
- WESTERN_DINING_SYSTEM
- JAPANESE_KOREAN_SYSTEM
- BAKERY_BREAKFAST_SYSTEM
- RETAIL_PACKAGED_SYSTEM

Category system is primary. Brand positioning is a secondary modifier (default weighting: category 70%, brand positioning 30%).

## Category-Native Design Rule

Each category must have its own:
- typography personality
- spatial headline language
- layout bias
- color system
- materials
- environment / prop language
- information density
- negative style rules

Gold brush lettering is not a universal default. It is valid only when category + positioning + dish semantics support it.

Examples:
- home-style Chinese hot dish → warm smoke, signage/portal, bold Chinese typography
- cake/dessert → light editorial serif, soft spatial forms, glass/cream/ribbon materiality
- coffee/tea → modern grotesk, lifestyle negative space, glass/window typography
- western dining → refined serif, fine-dining restraint, stone/linen/silver materiality

See `references/typography-personality-map.md`, `references/layout-bias-map.md`, and `references/brand-positioning-map.md`.

## Category Style Firewall

Transfer KV composition grammar across categories, not the visual skin.

Allowed universal grammar:
- Hero Food / Hero Product
- strong hierarchy
- spatial typography
- perspective
- foreground/midground/background layering
- controlled occlusion
- unified lighting
- negative space

Do not directly copy category skins. Dessert must not default to Chinese gold-brush restaurant signage. Coffee must not default to four circular home-dish selling-point badges. Western dining must not default to Sichuan red-gold restaurant styling.

See `references/category-style-firewall.md`.

## Creative Direction

After routing:
1. define ONE BIG IDEA
2. keep Food Hero as first visual priority
3. choose category-native spatial language
4. set master vanishing point where relevant
5. design headline as spatial structure appropriate to that category
6. create controlled occlusion
7. set category-appropriate information density
8. unify typography, light, material, props and color

## Information Density

Default Campaign set when not explicitly minimal:
- headline
- subtitle
- one slogan / campaign line
- 3–4 concise selling points when appropriate for the category
- address / phone if provided
- QR function zone when a real QR asset or target exists

Density is category-sensitive:
- home-style / spicy / retail packaged: medium-high
- soup / noodles / BBQ: medium
- premium seafood / dessert / coffee / western / Japanese: low-medium by default

Do not force four selling-point badges into every category.

## Typography Accuracy

User-supplied text accuracy must be 100%:
- headline
- subtitle
- store/brand name
- address
- phone
- price
- campaign text

## Final QA

A final KV must pass:
- Food Fidelity QC
- Typography Accuracy QC
- Spatial KV QC
- Category Visual Language QC (`references/category-qc.md`)

Thresholds:
- Food Fidelity >=95
- Vessel Fidelity >=98
- Typography Accuracy =100
- Category Visual Language >=85
- KV Design Quality >=90

If the category can be swapped with a completely different food and the poster still looks almost unchanged, treat it as template failure and reroute.
