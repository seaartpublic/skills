# Install SeaArt Skills

This repository ships four skills:

- **`generation-prompt-builder`** — builds or optimizes production-ready prompts for image, video, audio, and mixed creative generation.
- **`gpt-image-assistant`** — prepares GPT Image / GPT Image 2 prompts and editing instructions.
- **`prompt-preflight-advice`** — gives concise advice before final prompt writing or generation.
- **`storyboard-prompt-assistant`** — creates storyboard prompts, shot lists, and AI-video-ready prompt tables.

## Option 1 — `npx skills` (recommended, cross-agent)

Works with Claude Code, Cursor, Codex, and any agent that loads Markdown-based skills. Requires Node.js.

```bash
npx skills add seaartpublic/skills
```

Installs all four skills.

## Option 2 — `gh skill install`

GitHub CLI v2.90+:

```bash
gh skill install seaartpublic/skills
```

Installs all four skills.

## Option 3 — Claude Code marketplace

Claude Code only. Inside Claude Code:

```text
/plugin marketplace add seaartpublic/skills
/plugin install seaart@seaart
```

This reads `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`, then registers the skills as:

- `/seaart:generation-prompt-builder`
- `/seaart:gpt-image-assistant`
- `/seaart:prompt-preflight-advice`
- `/seaart:storyboard-prompt-assistant`

## Option 4 — Setup script

Universal fallback. Clone the repo locally and symlink each skill into the detected agent directory.

```bash
git clone --depth 1 https://github.com/seaartpublic/skills.git
cd skills
./setup
```

The script auto-detects Claude Code, Cursor, or Codex. Override detection when needed:

```bash
./setup --host claude
./setup --host cursor
./setup --host codex
```

Detected install paths:

| Agent | Target path |
|---|---|
| Claude Code | `~/.claude/skills/<skill-name>` |
| Cursor | `~/.cursor/plugins/<skill-name>` |
| Codex | `~/.codex/plugins/<skill-name>` |

The script is idempotent. Existing directories that are not symlinks are left untouched.

## Verify

Check that every skill contains `SKILL.md` in the target directory:

```bash
ls ~/.claude/skills/generation-prompt-builder/SKILL.md
ls ~/.claude/skills/gpt-image-assistant/SKILL.md
ls ~/.claude/skills/prompt-preflight-advice/SKILL.md
ls ~/.claude/skills/storyboard-prompt-assistant/SKILL.md
```

Use the matching Cursor or Codex target path if you installed for those agents.

Then ask your agent for one of these:

```text
Improve this product image prompt for SeaArt.
Prepare a GPT Image edit prompt for this reference.
Give preflight advice before I generate this image.
Turn this ad concept into a storyboard prompt table.
```

## Updating

| Method | Update command |
|---|---|
| `npx skills` | Re-run `npx skills add seaartpublic/skills` |
| `gh skill install` | `gh skill update seaartpublic/skills` |
| Claude Code marketplace | `/plugin update seaart@seaart` |
| Setup script | `cd skills && git pull && ./setup` |
