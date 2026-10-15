# Summary Authoring Guide

Apply this guide when creating or editing `references/python-<major>.<minor>-summary.md`.

## Keep this guide synchronized

When the user changes the requirements for summary content, scope, examples, or formatting, update this guide in the same task to reflect the latest confirmed requirements. Replace superseded rules instead of accumulating conflicting instructions. A factual correction to one feature does not automatically become a general authoring rule.

## Source and scope

1. Read the target version's official What's New page at `https://docs.python.org/<major>.<minor>/whatsnew/<major>.<minor>.html`.
2. Include only new syntax, new built-in types, and new typing features introduced in that version. This scope explicitly includes `frozendict`, even though it is a built-in type rather than a syntax change.
3. Exclude bug fixes, performance improvements, contributor information, and unrelated standard-library, tooling, configuration, or C API changes.
4. Provide the relevant PEP URL for each PEP-backed feature. Follow the source's PEP links; do not invent a PEP for a feature without one. Consult the PEP only when the source page lacks information needed for an accurate minimal example.

## Content and format

1. Write the document in English, with a version heading and a short section for each feature.
2. Give each feature the smallest useful Python example and only the minimum explanation needed to understand it. Include imports when required.
3. Leave derivable behavior and implications to the agent using the skill. For `frozendict`, explaining that it is an immutable dictionary is sufficient; omit additional discussion of hashing, inheritance, ordering, or interoperability.
4. Avoid rationale, historical comparisons, exhaustive restrictions, and long demonstrations. Include a restriction only when necessary to avoid misunderstanding or misusing the minimal example.
5. End the document with a separate `## Source and exclusions` section. Include a `Source:` link to the official What's New page used for that version and explicitly list the excluded content types defined under Source and scope.
6. Use spaces for indentation, UTF-8, CRLF line endings, and a final newline. Do not use U+2014.

## Skill boundary

Keep feature explanations and examples in the summary references. Keep `SKILL.md` focused on routing: determine the project's required Python version first, then cumulatively load every listed reference at or below the target version in ascending version order. A Python 3.15 target requires both the 3.14 and 3.15 references. Read each reference only once while its contents remain available in context. Applying features must still respect the project's minimum supported Python version.

When adding a version, add its reference link to the version table in `SKILL.md`.
