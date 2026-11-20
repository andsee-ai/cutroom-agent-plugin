# Using Cutroom from an agent

## Claude Code

```sh
/plugin marketplace add andsee-ai/cutroom-agent-plugin
/plugin install cutroom@andsee
```

or, once Cutroom itself is installed, link the full skill directly:

```sh
cutroom skill install --agent claude
```

Then ask for what you want: "把这条口播按这条对标视频复刻一遍", "edit this take into a 30-second TikTok".

## Codex, Antigravity and other agents with a shell

```sh
cutroom skill install            # links the skill into every agent found on this computer
cutroom skill status             # where it is linked
```

An agent without a skills folder can still use Cutroom: point it at the `SKILL.md` that `cutroom skill status --json`
prints, or paste this into it:

```text
Read https://github.com/andsee-ai/cutroom-agent-plugin/blob/main/skills/cutroom-start/SKILL.md and follow it.
```

## As MCP tools

The same engine is available as MCP tools over stdio, for one project folder at a time:

```sh
claude mcp add cutroom -- cutroom mcp --project /path/to/project
```

## Cutroom Editor

`cutroom editor` opens the browser editor: timeline, preview, layers, and a chat with the same skill built in.
