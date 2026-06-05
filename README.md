# SeaArt Skills

SeaArt skills help AI coding agents plan, improve, and prepare creative generation prompts. The skills are text-first: they do not install dependencies, store secrets, or require a SeaArt CLI.

## Install

Pick one installation path.

### `npx skills` — recommended, cross-agent

```bash
npx skills add seaartpublic/skills
```

### `gh skill install`

GitHub CLI v2.90+:

```bash
gh skill install seaartpublic/skills
```

### Claude Code marketplace

Inside Claude Code:

```text
/plugin marketplace add seaartpublic/skills
/plugin install seaart@seaart
```

### Setup script

Universal local fallback:

```bash
git clone --depth 1 https://github.com/seaartpublic/skills.git
cd skills
./setup
```

More options are in [INSTALL.md](./INSTALL.md). Agent-driven install instructions are in [INSTALL_FOR_AGENTS.md](./INSTALL_FOR_AGENTS.md).

## Skills

| Skill | Invoke | Description |
|---|---|---|
| [`generation-prompt-builder`](./generation-prompt-builder) | `/seaart:generation-prompt-builder` | Build or optimize high-quality prompts for image, video, audio, and mixed creative generation workflows. |
| [`gpt-image-assistant`](./gpt-image-assistant) | `/seaart:gpt-image-assistant` | Prepare GPT Image / GPT Image 2 generation, editing, inpainting, typography, product, UI, and diagram prompts. |
| [`prompt-preflight-advice`](./prompt-preflight-advice) | `/seaart:prompt-preflight-advice` | Give concise preflight advice, risk checks, and creative direction before writing or generating prompts. |
| [`storyboard-prompt-assistant`](./storyboard-prompt-assistant) | `/seaart:storyboard-prompt-assistant` | Convert concepts, scripts, product ideas, and rough video briefs into storyboard prompts and shot tables. |

## Quick Reference

| What you want | Skill | Note |
|---|---|---|
| Turn a rough idea into a polished generation prompt | `generation-prompt-builder` | Best for prompt text only, not direct generation. |
| Prepare an exact GPT Image prompt or edit instruction | `gpt-image-assistant` | Use for GPT Image-specific workflows and reference edits. |
| Get advice before final prompt writing | `prompt-preflight-advice` | Gives suggestions only; it should not replace the final prompt skill. |
| Break a video idea into shots | `storyboard-prompt-assistant` | Use for storyboard tables, shot lists, and multi-shot AI video prompts. |

## Design Boundaries

- These skills do not install packages, create `.env` files, or store API keys.
- These skills do not call generation tools unless the host environment explicitly provides and requests one.
- These skills keep product, brand, identity, text, and reference constraints explicit.

## License

MIT — see [LICENSE.txt](./LICENSE.txt).
