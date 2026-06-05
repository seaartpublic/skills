# Install for Agents

You are an AI coding agent. The user asked you to install SeaArt skills. Follow this exactly.

## Step 1 — Choose the target agent

Detect the user's agent platform:

| Agent | Path |
|---|---|
| Claude Code | `~/.claude/skills` |
| Cursor | `~/.cursor/plugins` |
| Codex | `~/.codex/plugins` |

If the repository is already cloned, prefer the setup script:

```bash
./setup
```

If auto-detection fails, run one of:

```bash
./setup --host claude
./setup --host cursor
./setup --host codex
```

## Step 2 — Manual fallback

If the setup script cannot be used, clone the repository and symlink each skill directory into the target path.

```bash
git clone https://github.com/seaartpublic/skills.git seaart-skills
cd seaart-skills
```

For Claude Code:

```bash
mkdir -p ~/.claude/skills
ln -s "$PWD/generation-prompt-builder" ~/.claude/skills/generation-prompt-builder
ln -s "$PWD/gpt-image-assistant" ~/.claude/skills/gpt-image-assistant
ln -s "$PWD/prompt-preflight-advice" ~/.claude/skills/prompt-preflight-advice
ln -s "$PWD/storyboard-prompt-assistant" ~/.claude/skills/storyboard-prompt-assistant
```

Use `~/.cursor/plugins` or `~/.codex/plugins` instead when installing for Cursor or Codex.

## Step 3 — Verify

Confirm these files exist in the selected target directory:

```text
generation-prompt-builder/SKILL.md
gpt-image-assistant/SKILL.md
prompt-preflight-advice/SKILL.md
storyboard-prompt-assistant/SKILL.md
```

## Step 4 — Done

Report this to the user:

```text
SeaArt skills installed. Try: "Improve this product image prompt" or "Turn this video idea into a storyboard table".
```

Do not ask the user for API keys. These skills are text-first and do not require local secrets or a SeaArt CLI.
