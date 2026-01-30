---
id: adapter-mapping
title: Adapter Mapping Rules
description: Rules for path mapping and file renaming in adapters
tags: 
  - mapping
  - paths
  - renaming
---

# Adapter Mapping Rules

The `mapping` section controls how spec files are transformed and placed in the workspace.

## Path Mapping

`mapping.path` determines output file location.

**Flat Structure:**
```yaml
path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}.md"
# Output: .myide/rules/auth-rule.md
```

**Folder Structure:**
```yaml
path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}/index.md"
# Output: .myide/rules/auth-rule/index.md
```

**Nested by Package:**
```yaml
path: "{{ config.targetDir[spec.type] }}/{{ spec.packageName }}/{{ spec.name }}.md"
# Output: .myide/rules/auth-package/login-rule.md
```

**Versioned:**
```yaml
path: "{{ config.targetDir[spec.type] }}/{{ spec.packageName }}@{{ spec.version }}/{{ spec.name }}/index.md"
# Output: .myide/rules/auth-package@1.0.0/login-rule/index.md
```

## File Renaming

`mapping.rename` changes filenames within specs (for multi-file specs).

**Basic:**
```yaml
rename:
  - from: "index.md"
    to: "{{ spec.name }}.md"
```

**Type-Specific:**
```yaml
rename:
  - from: "index.md"
    to: "{{ spec.type | upper }}.md"
```

**Conditional:**
```yaml
rename:
  - from: "index.md"
    to: "SKILL.md"
    when: "spec.type | lower | equals('skill')"
  
  - from: "index.md"
    to: "RULE.md"
    when: "spec.type | lower | equals('rule')"
```

## Best Practices

**Choose appropriate structure:**
- Flat: IDE prefers single directory
- Folder: Specs with multiple files
- Versioned: Support multiple package versions

**Use consistent naming:**
```yaml
# Good
path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}.md"

# Bad
path: "{{ config.targetDir[spec.type] }}/{{ spec.name | upper }}.MD"
```

**Handle missing directories:**
```yaml
path: "{{ config.targetDir[spec.type] | default(config.targetDir.default) }}/{{ spec.name }}.md"
```

**Coordinate path and rename:**
```yaml
mapping:
  path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}/index.md"
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.md"
# Result: .myide/rules/auth-rule/auth-rule.md
```

## Validation

✓ `mapping.path` exists and is valid
✓ Path expressions use proper syntax
✓ Fallbacks provided for optional config
✓ Rename rules don't conflict with path
✓ File extensions consistent
✓ Directory structure matches IDE requirements
✓ Conditional renames use proper `when` clauses
