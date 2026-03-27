# Atomic Transforms

Operations that add a metadata representation without removing any existing one. Each transform is idempotent and additive.

## Transform Catalog

### T1: Add Label from Title Prefix

- **Input**: Issue with `[EPIC]` in title, no `type/epic` label
- **Output**: Issue with `[EPIC]` in title AND `type/epic` label
- **Does NOT**: Remove `[EPIC]` from title
- **Implementation**: `POST /repos/{owner}/{repo}/issues/{number}/labels`

### T2: Add Frontmatter from Labels

- **Input**: Issue with `type/epic` label, no YAML frontmatter in body
- **Output**: Issue body prepended with `---\ntype: epic\n---\n`
- **Does NOT**: Remove the label
- **Implementation**: `PATCH /repos/{owner}/{repo}/issues/{number}` (update body)

### T3: Add Parent Reference from Task List

- **Input**: Parent issue with `- [ ] #N` task list item
- **Output**: Child issue (#N) gets `parent: owner/repo#M` in frontmatter
- **Does NOT**: Remove the task list from parent
- **Implementation**: Read parent body, parse task list, update each child's frontmatter

### T4: Add Agent Label from Frontmatter

- **Input**: Issue body contains `agent: kadmon`, no `agent:kadmon` label
- **Output**: `agent:kadmon` label added
- **Does NOT**: Remove frontmatter field
- **Prerequisite**: Label must exist (see T0)

### T5: Add Domain Label from Frontmatter

- **Input**: Issue body contains `domain: compaction`, no `domain/compaction` label
- **Output**: `domain/compaction` label added
- **Does NOT**: Remove frontmatter field

### T6: Add Project Field from Label

- **Input**: Issue with `type/epic` label, in project but Type field empty
- **Output**: Project Type field set to "Epic"
- **Does NOT**: Remove the label
- **Requires**: GitHub Projects v2, appropriate field defined

### T7: Add Cross-Repo Reference from Parent

- **Input**: Epic on repo A mentions child on repo B, child has no `parent:` frontmatter
- **Output**: Child on repo B gets `parent: A-owner/A-repo#N` in frontmatter
- **Does NOT**: Remove the mention from parent

### T8: Backfill Title Prefix from Label

- **Input**: Issue with `type/epic` label but no `[EPIC]` in title
- **Output**: Title updated to `[EPIC] <original title>`
- **Does NOT**: Remove the label
- **Note**: Most controversial — title changes are visible and noisy. Use only when opted in.

## Transform Properties

| Transform | Idempotent | Additive | Reversible | Noisy |
|-----------|-----------|----------|------------|-------|
| T1 | Yes | Yes | Label can be removed | Low |
| T2 | Yes | Yes | Frontmatter can be stripped | Low |
| T3 | Yes | Yes | Frontmatter can be stripped | Low |
| T4 | Yes | Yes | Label can be removed | Low |
| T5 | Yes | Yes | Label can be removed | Low |
| T6 | Yes | Yes | Field can be cleared | Low |
| T7 | Yes | Yes | Frontmatter can be stripped | Low |
| T8 | Yes | Yes | Prefix can be removed | High |

All transforms are designed to be safe to run repeatedly. Running T1 on an issue that already has the label is a no-op.

## Anti-Transform (Consolidation)

An **anti-transform** removes a representation. Anti-transforms are NEVER automatic. They require:

1. A PR authored by the stakeholder who owns the deprecated form
2. Acknowledgment that all known consumers of that form have been updated
3. A grace period during which both forms coexist

Example: Removing `[EPIC]` from titles after native Issue Types are adopted. Only a human or authorized agent who owns the title-scanning workflow may merge this.
