# Representation Matrix

How each semantic dimension maps to each GitHub surface.

## Dimensions × Surfaces

| Dimension | Title Prefix | Label | Project Field | YAML Frontmatter | Comment Meta | Native Type |
|-----------|-------------|-------|---------------|-------------------|-------------|------------|
| **type** | `[EPIC]`, `[BUG]` | `type/epic`, `type/bug` | `Type = Epic` | `type: epic` | `{"type":"epic"}` | Issue Type (alpha) |
| **status** | — | `status/blocked` | `Status = In Progress` | `status: open` | — | State (open/closed) |
| **priority** | `[P0]` | `priority/critical` | `Priority = P0` | `priority: critical` | — | — |
| **parent** | — | — | `Parent = #N` | `parent: org/repo#N` | `<!-- parent: #N -->` | Sub-issues (beta) |
| **domain** | `[compaction]` | `domain/compaction` | `Domain = compaction` | `domain: compaction` | — | — |
| **agent** | — | `agent:kadmon` | `Agent = kadmon` | `agent: kadmon` | `<!-- agent: kadmon -->` | — |
| **session** | — | — | — | `session: 36c485ab` | — | — |

## Encoding Levels

Each cell in the matrix above has an **encoding level** indicating how structured the data is:

| Level | Name | Example | Parseable by |
|-------|------|---------|-------------|
| 0 | **Absent** | Not encoded on this surface | — |
| 1 | **Convention** | `[EPIC]` in title | Regex, humans |
| 2 | **Controlled vocab** | `type/epic` label (from label set) | GitHub API, search |
| 3 | **Typed field** | Project v2 custom field | GraphQL, Projects API |
| 4 | **Schema-native** | GitHub Issue Type | REST/GraphQL, first-class |

## Reading Order

For any given dimension, check surfaces in this priority order (highest fidelity first):

1. Schema-native (Level 4) — if available in your GitHub plan
2. Project field (Level 3) — requires project board setup
3. Label (Level 2) — universally available
4. YAML frontmatter (Level 2) — requires body parsing
5. Title prefix (Level 1) — fragile but universal
6. Comment metadata (Level 1) — hidden, requires comment scanning

## Writing Order (Progressive Enhancement)

When filing an issue, write to **all available surfaces**, highest fidelity first:

1. Set the native type if available
2. Add to the project with typed fields
3. Apply labels from the controlled vocabulary
4. Include YAML frontmatter in the body
5. Add title prefix as human-readable hint
6. Optionally add comment metadata for bot state

Never stop at step 1. Each subsequent surface is a fallback for agents and scripts that can't access the higher-fidelity surface.
