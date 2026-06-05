---
name: prompt-preflight-advice
description: Provide concise, goal-aligned suggestions before generating or optimizing image, video, audio, GPT Image, or storyboard prompts. Use when the user asks for advice, direction, risks, alternatives, or "how should this prompt be improved" before producing the final prompt. This skill gives suggestions only and should not replace the main prompt-building skill.
---

# Prompt Preflight Advice

## Purpose

Use this skill to give focused advice before prompt writing or prompt optimization. This is an auxiliary skill: it should guide the next step, not replace the final prompt deliverable.

## When To Use

Use when the user asks:

- "give me advice first"
- "what is wrong with this prompt"
- "which direction would work better"
- "analyze how to improve this"
- "what are the risks"
- "give me a few directions"
- "is this better for image or video"

Also use as a short add-on after `generation-prompt-builder` or `storyboard-prompt-assistant` when the user wants optional improvement directions.

Boundary: If the user clearly asks for the final prompt, storyboard, or generated asset rather than advice, route to the relevant main skill. This skill gives advice only and never calls generation tools.

## Core Rules

1. Anchor every suggestion to the user's stated subject, medium, goal, style, and constraints.
2. Mark suggestions as optional when they are not required.
3. Keep advice concrete enough to write into a prompt.
4. Do not replace the user's concept with an unrelated theme, story, or visual style.
5. Do not give a generic prompt-writing lecture.
6. Do not call tools or generate assets.

## Workflow

1. Identify the target medium and user goal.
2. Find the highest-impact issues or opportunities.
3. Give 3-7 concrete suggestions.
4. Add 2-3 optional directions only when multiple good paths exist.
5. Ask 0-3 questions only if a missing detail blocks the next step.

## Advice Dimensions

Select only the relevant dimensions:

- **Goal clarity**: what the prompt is trying to make and for whom
- **Subject and information hierarchy**: main subject, supporting details, background hierarchy
- **Camera language**: shot scale, angle, camera movement, rhythm
- **Visual control**: lighting, material, color, composition, texture, era, weather
- **Consistency**: character, product, scene, logo, clothing, props, time of day
- **Text and layout**: exact text, hierarchy, readability, spacing, multilingual issues
- **Platform fit**: image vs video vs audio vs GPT Image vs AI-video constraints
- **Risk points**: ambiguity, overloading, safety-sensitive wording, hard-to-render details, text artifacts
- **Creative branches**: 2-3 viable creative directions that preserve the same goal

## Risk Checks

Prioritize these common issues:

- **Unclear target**: the user has not made clear whether the output should be image, video, audio, storyboard, or GPT Image edit.
- **Too many subjects**: one prompt contains too many characters, products, actions, or scenes.
- **Timeline conflict**: a video prompt asks for multiple places, time periods, or contradictory actions at once.
- **Reference conflict**: multiple reference images are not assigned clear roles for identity, style, composition, or scene.
- **Hard text rendering**: text is too long, too small, unquoted, or asks for complex typography and perfect readability at once.
- **Product fact risk**: the prompt implies unsupported efficacy, certification, material, price, or brand claims.
- **Platform mismatch**: a long storyboard is compressed into one prompt, or a static image prompt is written as complex continuous action.
- **Generic style**: the prompt only says "cinematic, high quality, ultra detailed" without lighting, composition, material, or camera control.

## Suggestion Style

- Each suggestion should explain how adopting it helps the current goal.
- Suggestions should be easy to turn into prompt text, such as shot scale, angle, lighting, material, pacing, or negative constraints.
- If giving creative branches, make the difference visual and strategic: mood-first, information-first, style-first, or product-realism-first.
- Keep advice separate from the main deliverable so the user does not mistake optional suggestions for the only answer.

## Output Format

Use the user's language unless they request otherwise.

```text
Suggestions
- [concrete suggestion]
- [concrete suggestion]
- [concrete suggestion]

Optional Directions
1. [direction A, if useful]
2. [direction B, if useful]

Needs Confirmation
- [only if a missing detail blocks the next step]
```

Keep `Suggestions` to 3-7 bullets. Keep `Needs Confirmation` to 0-3 questions.

## Combined Use

When combined with a main prompt skill:

1. First deliver the requested prompt or storyboard.
2. Then add a short `Optional Suggestions` section.
3. Never let advice override explicit user constraints.

## Quality Checks

- Advice is tied to the user's stated goal and medium.
- Each bullet is actionable and can be written into a prompt.
- Suggestions remain optional unless they fix a contradiction or blocking ambiguity.
- The response is concise enough to help the user decide the next step.

## Anti-Patterns

- Suggesting a different genre just because it sounds more impressive.
- Telling the user to add "cinematic, high quality, ultra detailed" without specifying what should become more controllable.
- Expanding advice into a full prompt when the user only asked for direction.
- Asking many questions when a reasonable first pass is possible.
