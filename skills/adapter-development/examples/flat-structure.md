# Flat Structure Adapters

Examples for IDEs that prefer simple flat directory structure without nested folders.

## When to Use

- IDE stores all files in single directory
- No type-based organization needed
- Simple file naming convention
- Minimal configuration required

## Example 1: Simple Flat

```yaml
name: simple-flat
version: "1.0.0"

config:
  targetDir:
    default: ".rules"

mapping:
  path: "{{ config.targetDir.default }}/{{ spec.name }}.md"
  
  frontmatter:
    title: "{{ spec.title }}"
    type: "{{ spec.type }}"
    - when: "spec.description"
      then:
        description: "{{ spec.description }}"
```

**Output:** `.rules/my-rule.md`

## Example 2: Cursor IDE

Flat structure with `.mdc` extension.

```yaml
name: cursor
version: "2.0"
description: "Cursor IDE adapter for Rulebix specs"

config:
  targetDir:
    default: ".cursor/rules"
  trigger:
    default: "auto"

mapping:
  path: "{{ config.targetDir.default }}/{{ spec.name }}.mdc"
  
  frontmatter:
    - when: "spec.description"
      then:
        description: "{{ spec.description }}"
    
    - when: "spec.patterns"
      then:
        globs: "{{ spec.patterns | join(', ') }}"
    
    - when: "spec.trigger | equals('always')"
      then:
        alwaysApply: true
  
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.mdc"
```

**Output:** `.cursor/rules/my-rule.mdc`

**Features:**
- Flat structure
- Custom `.mdc` extension
- Conditional frontmatter
- Glob patterns support
- File renaming

## Key Characteristics

- Single directory for all files
- Type information in frontmatter (not folder structure)
- Simple path expressions
- Easy to navigate and maintain
