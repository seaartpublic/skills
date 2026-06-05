---
name: gpt-image-assistant
description: GPT Image workflow assistant for text-to-image, reference-image editing, inpainting instructions, posters, typography, UI mockups, diagrams, product images, and final image prompt preparation. Use when the user explicitly wants GPT Image, GPT Image 2, gpt-image, image generation, or image editing. This skill does not include scripts, reference files, or automatic setup.
---

# GPT Image Assistant

## Purpose

Use this skill to prepare and, when the runtime clearly supports it, execute GPT Image generation or editing workflows. This skill contains no scripts and no external reference files.

## When To Use

Use for:

- GPT Image / GPT Image 2 prompt creation
- text-to-image requests
- reference-image editing
- inpainting or partial edits
- posters, typography, product photos, UI mockups, diagrams, thumbnails, illustrations, and character images
- refining a prompt immediately before image generation

Boundary: If the user only wants generic prompt optimization, use `generation-prompt-builder`. If the user wants video storyboard planning, use `storyboard-prompt-assistant`. This skill never installs tools, writes scripts, creates `.env`, or stores API keys.

## Core Rules

1. If the host environment provides a native image-generation tool and the user wants generation now, use that tool according to the environment rules.
2. If a `gpt-image` command is already available and the user explicitly wants CLI execution, use it after checking required inputs.
3. If no generation tool is available, output a ready-to-copy GPT Image prompt and state that no local image tool was invoked.
4. Do not auto-install packages, create launcher scripts, modify environment files, or write API keys.
5. Never print secret values. If an API key is missing, say it is missing without asking the user to paste it into project files.

## Workflow

Before generating or editing, identify:

- mode: text-to-image, reference edit, inpaint, or multi-reference
- final output goal and audience
- exact text that must appear in the image
- reference images and what to preserve from each
- what must change and what must remain unchanged
- aspect ratio, size, quality, and output file preference if available
- safety, brand, product, or typography constraints

Ask at most one concise question when the missing detail blocks the result. Otherwise make a small labeled assumption.

## Mode Routing

Classify the request first:

| Mode | Trigger | Handling |
|---|---|---|
| Text-to-image | No reference image; user wants an image generated | Write a full image prompt with size and quality suggestions |
| Reference edit | One or more reference images; user wants style, scene, clothing, product background, etc. changed | State what to preserve, what to change, and what must not change |
| Inpaint / partial edit | User specifies a region, mask, or only one local change | Describe target region, replacement, edge blending, and surrounding light consistency |
| Multi-reference | Multiple images provide character, product, scene, style, or composition | Assign each reference a purpose to avoid identity/style confusion |

If the user only asks for a GPT Image prompt, do not assume execution. Enter execution mode only when the user explicitly asks to generate, render, call a tool, or when the host has a native image-generation path the user wants to use.

## Execution And Setup Boundaries

- Prefer the host's native image-generation tool when available and requested.
- Use an existing `gpt-image` command only when it is already available and the user explicitly wants CLI execution.
- If no tool is available, deliver the prompt and recommended settings only.
- Do not install dependencies, write scripts, create `.env`, store keys, or display key values.
- For high-cost, high-quality, multi-reference, or exact-text requests, confirm size, quality, and reference handling before execution.

## GPT Image Patterns

Use these compact patterns instead of external galleries.

Product image:

```text
Create a clean commercial product image of [product]. Preserve accurate product shape, material, color, logo placement, and scale. Show [key benefit or use case] through [scene or props]. Lighting: [studio/lifestyle/soft daylight/high contrast]. Composition: [hero centered/three-quarter angle/flat lay]. Background: [simple contextual background]. No extra text unless specified.
```

Poster or typography:

```text
Create a poster for [topic/product/event]. Exact visible text: "[text]". Layout: strong hierarchy with title, subtitle, and supporting details. Typography: [style], readable, balanced spacing. Visual theme: [style]. Composition: [poster format]. Avoid misspelled text, extra letters, clutter, and illegible small type.
```

UI mockup:

```text
Create a realistic UI mockup for [app/product]. Screen: [desktop/mobile/dashboard]. Include [core components]. Visual style: clean product design, consistent spacing, real interface hierarchy, readable labels. Avoid decorative landing-page composition unless requested.
```

Reference edit:

```text
Edit the reference image. Preserve [identity/composition/product/pose/lighting] exactly. Change only [specific region or attribute] to [new target]. Keep perspective, shadows, reflections, and material consistency. Do not alter [protected details].
```

Character image:

```text
Create [character type] with [age/body type/facial features/hair/outfit/colors/accessories]. Pose: [pose]. Expression: [expression]. Style: [style]. Background: [background]. Keep the character visually consistent and avoid extra characters, text, or watermark.
```

## Asset-Specific Guidance

- **Exact text**: quote the exact text; specify hierarchy, type style, placement, and readability; avoid too much small text.
- **Product images**: lock shape, scale, material, color, and logo placement; do not add unsupported packaging information, certifications, or claims.
- **Posters**: define hierarchy before style; separate headline, subtitle, subject, background, and negative space.
- **UI mockups**: specify screen type, components, states, information hierarchy, and real product feel; avoid turning UI into a decorative poster.
- **Charts / infographics**: prefer simple layout, readable labels, limited data points, and clear legends; do not overload one image with complex data.
- **Characters**: lock age, body type, hairstyle, clothing, palette, expression, and pose; avoid extra characters.
- **Reference edits**: use `Preserve / Change / Do not change` sections to reduce accidental edits.

## Output Format

For prompt-only work:

```text
GPT Image Prompt
[ready-to-copy prompt]

Recommended Settings
- Size / aspect ratio: [recommendation]
- Quality: [low/medium/high if relevant]
- Reference handling: [if any]

Notes
- [short risk or edit constraint, if useful]
```

For executed generation, report only the useful execution details:

- output path or returned image link
- prompt summary
- important settings
- any error message needed for debugging

For reference edits, prefer:

```text
GPT Image Edit Prompt
Preserve:
- [identity, composition, product, lighting, etc. that must remain]

Change:
- [only the region or attribute to change]

Do not change:
- [protected details]

Final instruction:
[complete ready-to-copy edit instruction]
```

## Quality Checks

- For exact text, quote the text and request readable typography.
- For product images, do not invent claims, labels, certifications, or packaging copy.
- For edits, separate "preserve" and "change" instructions clearly.
- For inpainting, describe the target region and surrounding consistency.
- For final assets, prefer precise layout, lighting, and material language over broad style adjectives.

## Anti-Patterns

- Do not pretend a local image tool was invoked when no supported tool was available.
- Do not modify secrets, environment files, or project setup.
- Do not let image-generation execution override the user's exact edit constraints.
- Do not use generic "high quality" phrasing as a substitute for composition, lighting, text, and material details.
