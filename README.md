# dotnet-skillz

.NET CLI tools with SKILLS for coding agents.

## Available Skills

| Skill | Description |
|-------|-------------|
| [ilspy-decompile](skills/ilspy-decompile/SKILL.md) | Decompile .NET assemblies to C# source code using ILSpy |

## What are Skills?

Skills are lightweight prompts that teach coding agents how to use CLI tools effectively. They provide:

- **Token-efficient** workflows that don't bloat LLM context
- **Purpose-built commands** for specific tasks
- **Best practices** for common scenarios

## Requirements

- .NET 8 SDK or newer
- Claude Code, GitHub Copilot, or any other coding agent

## Installing Skills

### GitHub Copilot CLI (recommended)

```bash
/plugin marketplace add davidfowl/dotnet-skillz
/skills add ilspy-decompile
```

### Claude Code

```bash
mkdir -p .claude/skills/<skill-name>
curl -o .claude/skills/<skill-name>/SKILL.md \
  https://raw.githubusercontent.com/davidfowl/dotnet-skillz/main/skills/<skill-name>/SKILL.md
```

## Skills-less operation

You can also point your agent directly at a tool's help:

```
Decompile MyLibrary.dll using ilspycmd.
Check ilspycmd --help for available commands.
```

## Contributing

To add a new skill:

1. Create a folder under `skills/<skill-name>/`
2. Add a `SKILL.md` file following the format of existing skills
3. Update the Available Skills table in this README
