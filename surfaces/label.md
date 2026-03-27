# Surface: Labels

GitHub issue labels. Universally available on all GitHub plans.

## Namespace Convention

| Namespace | Separator | Example | Meaning |
|-----------|-----------|---------|---------|
| `type/` | `/` | `type/epic` | Issue type classification |
| `domain/` | `/` | `domain/compaction` | Problem domain |
| `status/` | `/` | `status/blocked` | Workflow state |
| `priority/` | `/` | `priority/critical` | Urgency |
| `agent:` | `:` | `agent:kadmon` | Responsible agent |

## Properties

- **Encoding level**: 2 (controlled vocabulary)
- **Queryable**: Yes, via `label:type/epic` in GitHub search
- **Cross-repo**: Must be created on each repo independently
- **Automation**: Can trigger GitHub Actions, branch protection rules
- **Limitations**: No hierarchy, no types, no validation beyond existence
