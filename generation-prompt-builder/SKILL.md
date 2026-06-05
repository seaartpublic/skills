---
name: generation-prompt-builder
description: Build or optimize high-quality generation prompts from copy, product information, scripts, rough ideas, reference-image descriptions, or existing prompts. Use for image, video, audio, and mixed creative prompts when the user wants ready-to-copy prompt text, not tool execution. Do not use when the user specifically asks to generate an image with GPT Image or asks for storyboard/shot-list planning.
---

# Generation Prompt Builder

## Purpose

Use this skill to turn user material into clear, production-ready prompts for AI generation tools. The output is prompt text only. Do not call image, video, audio, or CLI tools from this skill.

## When To Use

Use when the user asks to:

- generate prompts from ad copy, product information, scripts, briefs, rough ideas, or reference-image descriptions
- optimize, polish, professionalize, translate, or restructure an existing prompt
- create prompt variants for image, video, audio, product visuals, posters, UI mockups, character art, or creative assets
- preserve an existing concept while making it more specific and controllable

Boundary: If the user wants GPT Image execution, image editing, storyboard planning, shot lists, multi-shot video breakdowns, or pre-writing advice only, route to the corresponding dedicated skill instead.

## Core Rules

1. Preserve the user's intent: keep the same subject, product, story beats, emotional tone, brand constraints, and ending unless the user asks for variants.
2. Do not invent unsupported product facts, specs, prices, brand claims, slogans, certifications, or safety claims.
3. If a key detail is missing but not blocking, make the smallest reasonable assumption and label it in one short line.
4. If a missing detail would change the result significantly, ask 1-3 short questions before finalizing.
5. Keep prompts directly usable. Avoid long lectures, vague style filler, and unnecessary model jargon.
6. Match the user's requested output language. If no language is specified, use the conversation language for explanation and English for prompt blocks when that improves model compatibility.

## Workflow

1. Identify modality: image, video, audio, mixed, or unspecified.
2. Extract anchors: subject, goal, audience, style, mood, scene, composition, motion, text, constraints, and reference material.
3. Decide whether the request is generation from scratch, optimization, translation, or variants.
4. Write the prompt in a structured order the target model can follow.
5. Add negative constraints only when useful for control.
6. Briefly explain meaningful changes.

## Input Extraction

Extract different information from different input types:

- **Copy / ad text**: core selling point, audience, brand voice, required text, visual metaphor, forbidden claims.
- **Product information**: appearance, material, color, scale, use case, benefit, brand elements, and fact boundaries.
- **Script / story**: characters, scene, action, emotional turn, time order, dialogue or captions, ending.
- **Reference-image description**: identity, composition, style, color, material, pose, scene relationship, and allowed changes.
- **Existing prompt**: original hook, ambiguity, contradictions, overloaded details, missing visual controls, removable generic words.

If the input is thin but sufficient, make a first pass and label assumptions. Ask questions only when product facts, exact text, reference use, or target modality is unclear enough to change the result.

## Optimization Dimensions

Strengthen only the dimensions that matter for the task:

| Dimension | What to sharpen |
|---|---|
| Story / beats | Cause and effect, scene goal, emotional turn, who wants what, obstacle, result |
| Continuity | Time, place, wardrobe, props, character identity, product appearance |
| Shot language | Shot scale, angle, focal-length feel, camera movement, establishing / insert / reaction coverage |
| Visual specificity | Lighting, color temperature, palette, materials, weather, era, spatial layers |
| Motion / video | Pacing, action order, duration hints, transitions, subtitles or on-screen text rules |
| Image composition | Focal subject, background hierarchy, negative space, symmetry, rule of thirds, aspect ratio |
| Audio | Timbre, pace, language, sound-effect layers, music role, ambience and spatial feel |

## Prompt Patterns

For image prompts, prioritize:

- subject and exact visual identity
- environment and background hierarchy
- composition, camera angle, focal-length feel, and framing
- lighting, color palette, material details, and texture
- style, medium, and rendering quality
- exact visible text if any
- aspect ratio or output format when stated

For video prompts, prioritize:

- subject and scene goal
- action sequence and emotional progression
- shot scale, camera movement, pace, and transition
- lighting, environment, materials, and continuity
- duration hints only when the user gave or implied them
- audio, subtitles, or on-screen text only when relevant

For audio prompts, prioritize:

- voice, mood, rhythm, language, and pacing
- music role, instruments, ambience, and sound-effect layers
- delivery style and production feel

## Ready-To-Use Templates

Product visual:

```text
Create a high-quality commercial visual for [product]. Preserve the true appearance: [material, color, shape, logo placement]. Show [use case / core benefit] through [scene or action]. Composition: [centered hero / rule of thirds / flat lay / three-quarter angle]. Lighting: [soft studio / natural daylight / high-contrast rim light]. Background: [clean solid color / lifestyle environment / brand-color setting]. Do not add unsupported certifications, slogans, or packaging copy.
```

Poster / typography:

```text
Create a poster for [topic/product/event]. Exact visible text: "[text]". Clear hierarchy between headline, supporting information, and visual subject. Typography: [type direction], readable, balanced spacing. Visual style: [style]. Avoid misspelled text, extra words, crowded layout, and illegible small type.
```

Character image:

```text
Create [character type], age/body/facial features: [description], hair: [description], outfit: [material, color, style], accessories: [description]. Pose: [pose]. Expression: [expression]. Style: [style]. Background: [background]. Keep a single character, consistent identity, no watermark, no extra text.
```

Video segment:

```text
[Subject] performs [action sequence] in [scene]. The shot begins with [starting shot scale / angle] and follows with [camera movement]. Pacing: [slow / fast / escalating]. Lighting and color: [description]. Visual change: [key change]. Overall style: [style]. Avoid multiple location jumps, contradictory actions, and complex hard-to-render text.
```

UI / product interface:

```text
Create a realistic UI mockup for [product/app]. Screen type: [desktop/mobile/dashboard]. Include [core components]. Clear information hierarchy, consistent spacing, readable labels, explicit interaction states. The result should feel like a real shippable product interface, not a decorative marketing poster.
```

## Output Format

Use this format unless the user requested another one:

```text
Final Prompt
[ready-to-copy prompt]

Negative Prompt / Constraints
[only if useful]

Change Notes
- [short note]
- [short note]

Optional Variants
1. [optional variant, if useful]
2. [optional variant, if useful]
```

For new prompt creation, rename `Final Prompt` to `Generated Prompt`.

## Quality Checks

- The prompt preserves the user's subject, intent, and constraints.
- Any assumptions are small, labeled, and necessary.
- Product and brand claims are not invented.
- The output is ready to copy into a generation tool.
- Platform-specific flags are included only when the user requested a specific platform.

## Anti-Patterns

- Do not rewrite a simple product prompt into an unrelated story.
- Do not replace concrete user details with generic words like "cinematic" or "premium" without actionable visual specifics.
- Do not add platform-specific flags such as seeds, CFG, sampler, model IDs, or resolution suffixes unless the user requests a specific platform.
- Do not produce a full storyboard unless the user asks for multi-shot planning.
