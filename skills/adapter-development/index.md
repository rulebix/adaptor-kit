---
id: adapter-development
title: Adapter Development
description: Skills for developing custom IDE adapters
tags: 
    - development
    - adapter
    - ide
---

# Adapter Development Skills

Complete guide for developing custom IDE adapters for Rulebix.

## Getting Started

### Step 1: Understand IDE Requirements

1. File structure (flat vs nested)?
2. File extensions (`.md`, `.mdc`, other)?
3. Frontmatter format (required fields)?
4. Trigger mechanism?
5. Naming conventions?

### Step 2: Create MVP

```yaml
name: my-ide
version: "1.0.0"

mapping:
  path: ".myide/{{ spec.name }}.md"
```

### Step 3: Add Configuration

```yaml
config:
  targetDir:
    default: ".myide"
    rule: ".myide/rules"
    skill: ".myide/skills"

mapping:
  path: "{{ config.targetDir[spec.type] | default(config.targetDir.default) }}/{{ spec.name }}.md"
```

### Step 4: Implement Frontmatter

```yaml
mapping:
  path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    
    - when: "spec.description"
      then:
        description: "{{ spec.description }}"
```

### Step 5: Add Renaming (if needed)

```yaml
mapping:
  path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}/index.md"
  
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.md"
```

## Development Workflow

Research → Design → Implement → Test → Iterate

## Example References

Choose the relevant example based on your IDE requirements:

### [Flat Structure](./examples/flat-structure.md)
**Read when:** IDE uses single directory for all files, no nested folders needed
- Simple organization
- All files in one location
- Type info in frontmatter

### [Nested Structure](./examples/nested-structure.md)
**Read when:** IDE requires folder hierarchy organized by type
- Type-specific directories
- Multi-level organization
- Better for large projects

### [Package Versioning](./examples/package-versioning.md)
**Read when:** IDE needs to support multiple package versions simultaneously
- Version isolation
- Side-by-side versions
- Package management

### [Custom Extensions](./examples/custom-extensions.md)
**Read when:** IDE requires specific file extensions for different types
- Type-based extensions (`.rule`, `.skill`, `.mdc`)
- Extension mapping
- IDE-specific file types

### [Conditional Frontmatter](./examples/conditional-frontmatter.md)
**Read when:** IDE needs dynamic metadata based on conditions
- Optional field handling
- Type-specific metadata
- Trigger-based logic

### [Metadata-Rich](./examples/metadata-rich.md)
**Read when:** IDE requires comprehensive metadata and nested structures
- Complex frontmatter
- Nested objects
- Advanced features

### [File Renaming](./examples/file-renaming.md)
**Read when:** IDE requires specific file names or naming conventions
- `index.md` to custom names
- Type-based naming
- Extension changes

## Best Practices

1. Start simple, iterate incrementally
2. Use meaningful names (cursor-ide, vscode-rules)
3. Provide comprehensive config with defaults
4. Handle edge cases (missing fields, empty arrays)
5. Document with comments

## Troubleshooting

**Files not generated:**
- Cause: Invalid path expression
- Fix: Check syntax, ensure variables exist

**Frontmatter not applied:**
- Cause: Missing conditional checks
- Fix: Add `when` clauses for optional fields

**Rename not working:**
- Cause: Path and rename mismatch
- Fix: Coordinate path structure with rename rules

## Checklist

✓ kebab-case name ✓ semantic version ✓ complete config ✓ valid path ✓ proper frontmatter ✓ conditionals for optional fields ✓ file renaming (if needed) ✓ tested with various cases ✓ documented ✓ edge cases handled ✓ valid YAML
