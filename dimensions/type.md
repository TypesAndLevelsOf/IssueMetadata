# Dimension: Type

The most fundamental semantic dimension — what kind of issue is this?

## Values

| Value | Meaning | Used for |
|-------|---------|----------|
| epic | A collection of related issues toward a goal | Tracking, roadmap |
| bug | Something is broken | Triage, fix |
| feature | A new capability | Planning, roadmap |
| task | A unit of work | Sprint tracking |
| question | A request for information | Discussion, docs |
| meta | About the project itself (labels, CI, docs) | Housekeeping |

## Surface Encodings

| Surface | Encoding | Example |
|---------|----------|---------|
| Title prefix | `[TYPE]` uppercase | `[EPIC] Fix compaction` |
| Label | `type/{value}` | `type/epic` |
| Project field | `Type` single-select | `Epic` |
| YAML frontmatter | `type: {value}` | `type: epic` |
| GitHub native | Issue Type dropdown | `Epic` |

## Notes

- The `type/` label namespace is shared across all repos in a cross-org project
- Agent kadmon creates labels via `gh-setup-labels.js` using the GitHub API
- Native Issue Types are in alpha (2026) and not available on all plans
