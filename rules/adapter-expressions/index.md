---
id: adapter-expressions
title: Adapter Expression Rules
description: Rules for using expressions in adapter configuration
tags: 
  - expressions
  - syntax
  - templating
---

# Adapter Expression Rules

Expression engine uses `{{ ... }}` syntax to inject dynamic values into paths, frontmatter, and filenames.

## Available Variables

| Variable | Type | Example | Description |
|----------|------|---------|-------------|
| `spec.name` | string | `auth-rule` | Spec ID (kebab-case) |
| `spec.title` | string\|null | `Authentication Rule` | Spec title |
| `spec.type` | string | `rule` | Spec type |
| `spec.trigger` | string | `always` | Trigger mode |
| `spec.description` | string\|null | `Validates auth` | Description |
| `spec.tags` | string[] | `["auth"]` | Tags array |
| `spec.version` | string | `1.0.0` | Package version |
| `spec.packageName` | string | `auth-rules` | Package name |
| `spec.patterns` | string[]\|undefined | `["*.ts"]` | Glob patterns |
| `config` | object | `{targetDir: {...}}` | Adapter config |

## Operators & Filters

**Fallback (OR):**
```yaml
title: "{{ spec.title | default(spec.name) }}"
```

**Property Access:**
```yaml
path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}.md"
```

**Array Access:**
```yaml
firstTag: "{{ spec.tags[0] }}"
```

**String Filters:**
```yaml
uppercase: "{{ spec.name | upper }}"
lowercase: "{{ spec.name | lower }}"
```

**Array Filters:**
```yaml
joinTags: "{{ spec.tags | join(', ') }}"
length: "{{ spec.tags | length }}"
```

**Comparison:**
```yaml
isRule: "{{ spec.type | equals('rule') }}"
```

## Best Practices

**Always use fallbacks:**
```yaml
# Good
title: "{{ spec.title | default(spec.name) }}"

# Bad (can be null)
title: "{{ spec.title }}"
```

**Use bracket notation for dynamic keys:**
```yaml
# Good
path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}.md"

# Bad (hardcoded)
path: "{{ config.targetDir.rule }}/{{ spec.name }}.md"
```

**Validate array access:**
```yaml
# Good
- when: "spec.tags"
  then:
    tags: "{{ spec.tags }}"

# Bad (can error if undefined)
tags: "{{ spec.tags[0] }}"
```

## Validation

✓ All expressions use `{{ ... }}` syntax
✓ Variables exist in available variables
✓ Fallbacks provided for optional fields
✓ Array access protected with conditionals
✓ Bracket notation for dynamic keys
