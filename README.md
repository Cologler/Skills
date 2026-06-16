# Skills

A collection of agent skills.
Each skill provides specialized instructions and workflows for an AI agent to handle specific tasks.

This repository focuses on reusable skill content. One-time setup material,
such as installation or initial configuration steps, is usually trimmed unless
it is needed repeatedly during normal agent workflows.

## Doc

Doc skills focus on generating and bundling source documentation for agents to
consult, rather than teaching experience-based tool usage patterns.

| Skill | Description |
|-------|-------------|
| [justfile-docs](doc/justfile-docs/SKILL.md) | Route agents to the bundled official just usage documentation snapshot |

## Tool

| Skill | Description |
|-------|-------------|
| [cli-toolkit-catalog](tool/cli-toolkit-catalog/SKILL.md) | Category catalog of commonly available CLI tools |
| [tiged](tool/tiged-tool/SKILL.md) | A scaffolding tool to download a git repo's snapshot without history |
| [poethepoet](tool/poethepoet-tool/SKILL.md) | Run and manage Poe tasks in Python projects |
