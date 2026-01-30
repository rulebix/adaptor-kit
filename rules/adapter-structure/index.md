---
id: adapter-structure
title: Adapter Structure Rules
description: Rules for creating valid adapter YAML structure
tags: 
  - structure
  - yaml
  - validation
---

# Adapter Structure Rules

Every Rulebix adapter must follow a valid and consistent YAML structure.

## Required Root Properties

```yaml
name: string # Required: unique identifier (kebab-case)
version: string # Required: semantic version (e.g., "1.0.0")
description: string # Optional: human-readable description
```

## Config Section (Required)

Stores adapter-specific values referenced in mapping expressions:

```yaml
config:
  targetDir:
    default: ".myide"
    rule: ".myide/rules"
    skill: ".myide/skills"
    workflow: ".myide/workflows"
  
  filename: "{{ spec.name }}"
  trigger:
    default: "always"
```

**Best Practices:**
- Use `targetDir` to define output locations by resource type
- Provide `default` values for fallback
- Use consistent naming (kebab-case for directories)

## Mapping Section (Required)

Defines file transformation:

```yaml
mapping:
  # Path expression (required)
  path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}.md"

  # Frontmatter transformation (optional)
  frontmatter:
    title: "{{ spec.title }}"
    description: "{{ spec.description }}"

  # File renaming (optional)
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.md"
```

## Minimum Viable Adapter

```yaml
name: my-ide
version: "1.0.0"

mapping:
  path: ".myide/{{ spec.name }}.md"
```

## Validation

✓ `name` exists and uses kebab-case
✓ `version` exists and uses semantic versioning
✓ `mapping.path` exists and is valid
✓ All expressions use `{{ ... }}` syntax
✓ Valid YAML syntax (proper indentation, no tabs)
✓ File extension is `.yml` or `.yaml`
