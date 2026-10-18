# Skills

Personal agent skills by [Ammar Bandukwala](https://github.com/ammario).

| Skill | Purpose |
| --- | --- |
| [handoff](skills/handoff/SKILL.md) | Capture the current session so a fresh agent can continue the work. |
| [subtractive](skills/subtractive/SKILL.md) | Deliver features while reducing code and conceptual complexity. |

## Install

Install both skills globally for Codex and Claude Code with the [skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add ammario/skills -g --agent codex claude-code --skill handoff subtractive
```

Preview the available skills without installing:

```sh
npx skills add ammario/skills --list
```

Both skills retain `disable-model-invocation: true` for agents that support it. Invoke them explicitly when needed.

## Local development

Keep a checkout at `~/Projects/ammario/skills` and link directly to it so edits are available immediately:

```sh
git clone https://github.com/ammario/skills.git ~/Projects/ammario/skills
mkdir -p ~/.agents/skills ~/.claude/skills
for skill in handoff subtractive; do
  ln -s "$HOME/Projects/ammario/skills/skills/$skill" "$HOME/.agents/skills/$skill"
  ln -s "$HOME/Projects/ammario/skills/skills/$skill" "$HOME/.claude/skills/$skill"
done
```

The links require unused destination names; replace an existing installation deliberately before linking. Codex uses `~/.agents/skills`, and Claude Code uses `~/.claude/skills`.

Edit the files under `skills/`, then commit and push changes from this checkout. For a direct checkout installation, update with `git pull --ff-only`; for a CLI installation, use `npx skills update`.
