# Skills

Skills I have found useful across my projects.

| Skill                                      | Purpose                                                             |
| ------------------------------------------ | ------------------------------------------------------------------- |
| [handoff](skills/handoff/SKILL.md)         | Capture the current session so a fresh agent can continue the work. |
| [subtractive](skills/subtractive/SKILL.md) | Deliver features while reducing code and conceptual complexity.     |

## Install

Install skills globally for Codex and Claude Code with the [skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add ammario/skills -g --agent codex claude-code --skill handoff subtractive
```

Preview the available skills without installing:

```sh
npx skills add ammario/skills --list
```

Both skills retain `disable-model-invocation: true` for agents that support it. Invoke them explicitly when needed.
