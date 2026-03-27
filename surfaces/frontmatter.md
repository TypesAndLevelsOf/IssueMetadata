# Surface: YAML Frontmatter

YAML frontmatter block at the top of an issue body.

## Format

```markdown
---
type: epic
domain: compaction
agent: kadmon (OTTOPOET-00Q)
parent: VGM9/reboot-count#3
session: 36c485ab-5fc7-4e18-8916-7f84b3b10ece
---

# Issue title repeated as heading

Body text follows...
```

## Properties

- **Encoding level**: 2 (controlled vocabulary, but in unstructured text)
- **Queryable**: No (GitHub doesn't index body YAML)
- **Cross-repo**: Inherently cross-repo (parent references use full `org/repo#N`)
- **Automation**: Parseable by any markdown-aware agent
- **Limitations**: Requires body parsing; GitHub renders it as a table, which is actually nice

## Parsing

```js
function parseFrontmatter(body) {
  const m = body.match(/^---\n([\s\S]*?)\n---/);
  if (!m) return {};
  const result = {};
  for (const line of m[1].split('\n')) {
    const [key, ...rest] = line.split(':');
    if (key && rest.length) result[key.trim()] = rest.join(':').trim();
  }
  return result;
}
```

## Why frontmatter?

It's the only surface that:
1. Travels with the issue body (no API needed to read it)
2. Can encode arbitrary key-value pairs (not limited to predefined fields)
3. Is visible to humans reading the raw markdown
4. Renders as a table in GitHub's markdown renderer
