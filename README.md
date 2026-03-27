# Types and Levels of Issue Metadata Representation

A taxonomy of how semantic concepts (type, status, priority, parent, domain, agent) manifest across GitHub surfaces — and why they should coexist rather than replace each other.

## The Problem

A GitHub issue's "type" can be encoded in at least six different ways:

| Surface | Example | Who reads it |
|---------|---------|-------------|
| Title prefix | `[EPIC] Fix the thing` | Humans scanning issue lists |
| Label | `type/epic` | GitHub search, automation, branch protection |
| Project field | `Type = Epic` | GitHub Projects (v2) boards and views |
| YAML frontmatter | `type: epic` (in issue body) | Agent parsers, markdown-aware tools |
| Comment metadata | JSON in HTML comment | Bots, hidden state machines |
| Issue type (native) | GitHub Issues "type" field (alpha) | GitHub UI, API v4 |

Each surface was chosen by **someone** — a human setting up a project, an agent filing issues, a bot parsing bodies. Removing one breaks whoever relies on it.

## The Middle Space

> All representations of the same semantic concept coexist. They are children of the same declarative; all imperatives to the same meaning.

This repo documents the **types** of metadata (what dimensions exist) and the **levels** at which each dimension can be encoded (which GitHub surfaces carry it). The organizing principle:

1. **Progressive enhancement**: Add new representations, never remove old ones
2. **Graceful degradation**: If a surface is unavailable (no Projects, no native types), fall back to the next best
3. **Opt-in consolidation**: Only the stakeholder who owns a deprecated form may merge a PR to decommission it
4. **Schema versioning**: Track which VS Code / GitHub API version introduced each surface

## Taxonomy Structure

- [`dimensions/`](dimensions/) — The semantic dimensions (type, status, priority, parent, domain, agent, session)
- [`surfaces/`](surfaces/) — The GitHub surfaces where dimensions can be encoded
- [`REPRESENTATIONS.md`](REPRESENTATIONS.md) — The full matrix: which dimension × which surface × encoding format
- [`TRANSFORMS.md`](TRANSFORMS.md) — Atomic operations that add a representation without removing any

## Lineage

Part of [TypesAndLevelsOf](https://github.com/TypesAndLevelsOf), extending the PSW 2000 "Types and Levels of Automation" framework to GitHub issue metadata. See also:

- [Automation](https://github.com/TypesAndLevelsOf/Automation) — The original LOA taxonomy (Parasuraman, Sheridan & Wickens 2000)
- [AgentSpawn](https://github.com/TypesAndLevelsOf/AgentSpawn) — DISPATCH lattice for agent spawning
- [GHORGS](https://github.com/TypesAndLevelsOf/GHORGS) — GitHub org semantic ladder

## Filed by

Agent kadmon (OTTOPOET-00Q / AO_HTEPSCF_00Q), session `36c485ab`, Q 0.0.6+.
