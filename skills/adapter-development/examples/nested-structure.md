# Nested Structure Adapters

Examples for IDEs that require organized folder structure with type-specific directories.

## When to Use

- IDE organizes files by type (rules, skills, workflows)
- Requires folder hierarchy
- Better organization for large projects
- Type-based navigation

## Example 1: Organized Nested

```yaml
name: organized-nested
version: "1.0.0"

config:
  targetDir:
    rule: ".config/rules"
    skill: ".config/skills"
    workflow: ".config/workflows"

mapping:
  path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}/index.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    - when: "spec.tags"
      then:
        tags: "{{ spec.tags }}"
```

**Output:** `.config/rules/my-rule/index.md`

## Example 2: Google Antigravity

Nested structure with package versioning.

```yaml
name: google-antigravity
version: "1.0"
description: "Google Antigravity / Gemini CLI adapter"

config:
  targetDir:
    default: ".agent"
    rule: ".agent/rules"
    skill: ".agent/skills"
    workflow: ".agent/workflows"
  
  trigger:
    default: "always"

mapping:
  path: "{{ config.targetDir[spec.type] }}/{{ spec.packageName }}@{{ spec.version }}/{{ spec.name }}/index.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    - key: trigger
      value: "{{ spec.trigger | default(config.trigger.default) }}"
    
    - when: "spec.description"
      then:
        description: "{{ spec.description }}"
    
    - when: "spec.trigger | equals('glob')"
      then:
        globs: "{{ spec.patterns }}"
  
  rename:
    - from: "index.md"
      to: "SKILL.md"
      when: "spec.type | equals('skill')"
```

**Output:** `.agent/rules/my-package@1.0.0/my-rule/index.md`

**Features:**
- Nested folder structure
- Package versioning in path
- Type-specific directories
- Conditional file renaming
- Default value handling

## Key Characteristics

- Multiple directory levels
- Type-based folder organization
- `index.md` as entry point
- Clear separation of concerns
- Scalable for large projects
