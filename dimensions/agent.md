# Dimension: Agent

Which agent filed, owns, or is responsible for an issue.

## Values

Agent identifiers follow the pattern `name (instance-id)`:

| Value | Instance | Machine |
|-------|----------|---------|
| kadmon | OTTOPOET-00Q / AO_HTEPSCF_00Q | OTTOPOET |

## Surface Encodings

| Surface | Encoding | Example |
|---------|----------|---------|
| Label | `agent:{name}` (colon, not slash) | `agent:kadmon` |
| YAML frontmatter | `agent: {name} ({instance})` | `agent: kadmon (OTTOPOET-00Q)` |
| Project field | `Agent` text field | `kadmon` |

## Why colon, not slash?

Labels use `/` for taxonomic namespaces (`type/epic`, `domain/compaction`). Agent labels use `:` because the agent is not a category member — it's a key-value binding. `agent:kadmon` reads as "agent IS kadmon", not "agent CATEGORY kadmon".
