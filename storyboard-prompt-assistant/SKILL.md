---
name: storyboard-prompt-assistant
description: Convert concepts, scripts, ad copy, product ideas, rough stories, or vague video ideas into high-quality storyboard prompts, shot lists, and AI-video-ready multi-shot prompt tables. Use for storyboard, shot script, camera planning, shot list, video storyboard, trailer planning, script-to-storyboard, AI video prompts, and incremental storyboard edits.
---

# Storyboard Prompt Assistant

## Purpose

Use this skill to turn ideas, scripts, copy, or rough concepts into usable video storyboard prompts. The output is text only. Do not call video generation tools.

## When To Use

Use when the user asks for:

- storyboard, shot script, camera design, shot list, or shot breakdown
- concept, script, copy, or product idea to video storyboard
- trailer, music video, ad, short film, game promo, product demo, or narrative video planning
- Sora, Kling, Runway, Veo, Seedance, Pika, Hailuo, or other AI-video prompt tables
- incremental edits to previous storyboard output, especially when the user says everything else should stay unchanged

Boundary: If the user wants single-image prompt optimization, use `generation-prompt-builder` or `gpt-image-assistant`. If the user only wants general pre-writing advice, use `prompt-preflight-advice`.

## Modes

Choose the smallest mode that satisfies the user.

1. **Fast Video Prompts**: 3-5 ready-to-copy video prompts for exploration.
2. **Storyboard Table**: structured shot table with timing, shot scale, camera movement, positive prompt, negative prompt, and continuity notes.
3. **Interactive Long Storyboard**: staged workflow for complex scripts: theme analysis, character settings, scene settings, overview, then detailed segments after user confirmation.

If the user did not specify a mode:

- For "generate video prompts" or text-to-video requests, default to `Fast Video Prompts`.
- For "break this into shots", "shot list", or script-to-storyboard requests, default to `Storyboard Table`.
- For long stories or when the user asks to proceed step by step, use `Interactive Long Storyboard`.

## Core Rules

1. Preserve the user's plot, product facts, brand constraints, and intended emotion.
2. Do not remove plot points without permission.
3. For AI-video shots, default each shot to 2-6 seconds unless the user specifies a platform or duration rule.
4. Avoid impossible overloaded shots. Split actions when one shot contains too many beats.
5. Use concrete visual language: subject, action, environment, lighting, shot scale, camera movement, pace, and transition.
6. Do not add platform-specific parameters, seeds, model IDs, or unsupported flags unless requested.
7. For reference images, describe how each reference should be used: character identity, product look, location, style, motion, or first/last frame.

## Workflow

1. Extract project type, audience, duration, format, style, key scenes, characters, product/brand facts, and target platform if any.
2. Identify the narrative beats: opening, setup, escalation, climax, ending, or product benefit flow.
3. Choose mode and state any necessary assumption in one short line.
4. Build shots with clear time allocation.
5. Add positive prompts and negative prompts only where they improve controllability.
6. Add continuity notes for character, product, scene, lighting, and transitions.

## Information To Extract

Before output, try to extract:

- Project type: ad, short film, music video, trailer, game promo, product demo, narrative concept film
- Total duration or approximate duration
- Narrative sections: opening, setup, escalation, climax, ending
- Core mood: suspenseful, energetic, gentle, horror, epic, sci-fi, playful, luxury
- Key visual assets: characters, product, scene, props, logo, UI, title copy
- Target use: exploration, pitch, editing plan, outsourcing brief, AI video generation, AI image storyboard
- Target model or platform: Sora, Veo, Runway, Pika, Kling, Hailuo, Seedance, etc.

If key information is missing but a useful first pass is possible, make a reasonable assumption and state it. Ask only when total duration, output format, core subject, or immutable product facts are unclear.

## Duration Strategy

- For AI video, default each shot to **2-6 seconds**, preferably 3-5 seconds.
- If the user gives total duration, split it into shots and keep the shot durations adding up to the total when possible.
- If the total duration does not divide cleanly, adjust shot durations within 2-6 seconds and explain the tradeoff in one sentence.
- Avoid shots shorter than 2 seconds unless they are flash cuts, trailer impact beats, or explicitly requested.
- Avoid shots longer than 6 seconds unless the user asks for a one-take shot or the platform supports long shots.
- Trailer or promo climax sections can use denser shorter shots; setup sections can use longer establishing shots.

## Global Style Lock

Before detailed shots, lock the global rules so the storyboard stays coherent:

- visual tone and style system
- color direction and lighting logic
- pacing and default transition logic
- aspect ratio and medium
- continuity for character, product, logo, wardrobe, and scene
- whether title cards, narration, subtitles, UI, or HUD overlays appear

## Output Format

Choose one of these output formats based on the selected mode:

- `Fast Video Prompts`: labeled prompt variants.
- `Storyboard Table`: shot table with timing and prompt fields.
- `Interactive Long Storyboard`: staged outputs with confirmation between stages.

## Shot Table Format

Use this table for normal storyboard work:

| Shot | Duration | Shot Scale / Camera | Visual Content | AI Positive Prompt | AI Negative Prompt | Audio / Captions | Continuity Notes |
|---|---:|---|---|---|---|---|---|
| 1 | 4s | Wide shot, slow dolly-in | ... | ... | ... | ... | ... |

Guidelines:

- `Duration`: use whole seconds where possible.
- `Shot Scale / Camera`: combine shot scale and movement, such as close-up fixed shot, medium shot dolly-in, wide shot pan, overhead tracking.
- `AI Positive Prompt`: ready-to-copy visual prompt, usually English or English-dominant hybrid if useful.
- `AI Negative Prompt`: only the most relevant artifacts, such as distorted hands, flickering text, inconsistent logo, extra characters, watermark.
- `Continuity Notes`: first/last frame continuity, repeated object, match cut, action continuity, or transition.

Column guidance:

- `Visual Content`: state who does what, when key information appears, and foreground/midground/background relationships.
- `AI Positive Prompt`: focus on one main shot or one continuous segment; avoid multiple locations and complex time jumps.
- `AI Negative Prompt`: adapt by topic, such as extra fingers, flickering subtitles, wrong logo, watermark, over-sharpened, inconsistent face.
- `Audio / Captions`: write sound-effect trigger points; quote exact captions or screen text.
- `Continuity Notes`: describe first/last frame continuity, action continuity, prop continuity, product angle, lighting, or edit point.

## Fast Video Prompt Format

For quick prompt generation:

```text
Direction 1: [name]
Prompt: [ready-to-copy video prompt]
Best for: [use case or mood]

Direction 2: [name]
Prompt: ...
```

Keep variants meaningfully different in visual strategy, not random rewrites.

## Interactive Long Storyboard

Use stages only when the user wants step-by-step work:

1. Theme and script analysis.
2. Character settings and scene settings.
3. Ask whether to continue with storyboard information.
4. Storyboard overview with segment durations.
5. Ask which segment to expand.
6. Detailed shot plan for the selected segment.

Do not force this flow for short requests.

For interactive long storyboard work:

- Theme analysis should identify the core hook, emotional atmosphere, script gaps, and weak cause-and-effect.
- Character settings should separate recurring characters, important states, outfits, and signature props.
- Scene settings should list major environments likely to appear later and describe their empty-state spatial features.
- Storyboard overview should preserve all plot points and not remove content without permission.
- Detailed segments should stay manageable; let the user choose which segment to expand when the story is complex.

## Incremental Edits

When the user says everything else should stay unchanged:

1. Change only the named shot, field, style, duration, or prompt.
2. Preserve untouched rows, wording, order, and constraints.
3. If the requested change affects continuity, update only the minimum necessary neighboring note and explain the dependency in one sentence.

## Quality Checks

- The selected mode matches the user's actual request.
- Each shot has one clear visual beat and feasible duration.
- Character, product, logo, scene, and lighting continuity are preserved.
- AI-video prompts are ready to copy and not overloaded with multiple locations or time jumps.
- Negative prompts target relevant artifacts rather than generic clutter.
- For trailers, teasers, or promos, the opening quickly establishes world or mood, the middle escalates information density, and the ending leaves a title, slogan, release beat, or hook.

## Anti-Patterns

- Do not turn a single prompt request into a long screenplay.
- Do not make every shot a generic "cinematic close-up".
- Do not add camera crew, slate, microphone, or filming-set language unless the concept is explicitly meta-production.
- Do not overload one AI-video shot with multiple locations, time jumps, or complex dialogue.
