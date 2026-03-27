# Dimension: Domain

The problem domain or technical area an issue belongs to.

## Values (open vocabulary)

Unlike Type, Domain values are not a closed set. New domains are added as the project encounters them.

| Value | Meaning | Origin |
|-------|---------|--------|
| compaction | VS Code chat session compaction/reboot detection | VGM9 tooling |
| session | Chat session format, JSONL parsing, session identity | VGM9 tooling |
| cli | VS Code CLI shim, `code` command resolution | OTTOPOET setup |
| lmstudio | LM Studio server, model loading, API | OTTOPOET setup |
| piaf | PIAF/UPN path conventions, enfoldered workspace | OTTOPOET setup |
| taxonomy | TypesAndLevelsOf framework, metadata representation | Meta |

## Surface Encodings

| Surface | Encoding | Example |
|---------|----------|---------|
| Title prefix | `[domain]` lowercase | `[compaction] Fix parser` |
| Label | `domain/{value}` | `domain/compaction` |
| Project field | `Domain` single-select | `compaction` |
| YAML frontmatter | `domain: {value}` | `domain: compaction` |
