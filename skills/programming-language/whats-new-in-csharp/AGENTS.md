# Summary Authoring Guide

## Keep this guide synchronized

When the user changes summary requirements, update this guide in the same task to reflect the latest confirmed rules. Replace superseded rules. A factual correction to one feature does not automatically become a general authoring rule.

## Source and scope

1. Use the requested version's official Microsoft What's New page. Follow its language reference or feature specification links only when needed for an accurate minimal example.
2. Keep C# language changes in `references/csharp-<version>-summary.md` and .NET runtime changes in `references/dotnet-<version>-summary.md`. Do not combine the two release tracks or generate unrequested versions.
3. Language summaries include new syntax and language or type-system features. Runtime summaries cover new runtime capabilities and relevant .NET APIs when requested. Exclude bug fixes, performance optimization reports, contributor information, and unrelated tooling or configuration changes. Retain new source directives explicitly listed as language features, identifying their SDK dependency.
4. Link the corresponding official feature specification when available, otherwise the language or API reference. Do not invent proposal identifiers.

## Content and format

1. Write in English. Use a version heading and one short section per feature, with the smallest useful example and minimum necessary explanation. Include required imports. Leave derivable implications to the agent using the skill.
2. In each language summary, state the supported .NET target and required SDK/compiler version. Distinguish official support policy from a feature's technical runtime or library dependency; document specific requirements beside the affected feature when needed.
3. Avoid rationale, historical comparisons, exhaustive restrictions, and long demonstrations. Include a restriction only when necessary to understand or use the example correctly.
4. End each summary with a separate `## Source and exclusions` section containing the source URL and excluded content types.
5. Use spaces, UTF-8, CRLF line endings, and a final newline. Do not use U+2014.

## Skill boundary

Keep examples and feature explanations in references. Keep `SKILL.md` focused on determining language and runtime targets separately, cumulative loading within each release track, and reusing references already read in context. Add new references to their respective version tables.
