# Adapter Examples Index

Real-world adapter examples organized by pattern and use case.

## Quick Selection Guide

Choose the example that matches your IDE requirements:

| Pattern | Use Case | File |
|---------|----------|------|
| **Flat Structure** | Single directory, simple organization | [flat-structure.md](./flat-structure.md) |
| **Nested Structure** | Type-based folders, organized hierarchy | [nested-structure.md](./nested-structure.md) |
| **Package Versioning** | Multiple versions, version isolation | [package-versioning.md](./package-versioning.md) |
| **Custom Extensions** | Type-specific file extensions | [custom-extensions.md](./custom-extensions.md) |
| **Conditional Frontmatter** | Dynamic metadata, optional fields | [conditional-frontmatter.md](./conditional-frontmatter.md) |
| **Metadata-Rich** | Comprehensive metadata, nested objects | [metadata-rich.md](./metadata-rich.md) |
| **File Renaming** | Custom file names, naming conventions | [file-renaming.md](./file-renaming.md) |

## Decision Tree

1. **Does IDE use nested folders?**
   - No → [Flat Structure](./flat-structure.md)
   - Yes → [Nested Structure](./nested-structure.md)

2. **Does IDE need multiple package versions?**
   - Yes → [Package Versioning](./package-versioning.md)

3. **Does IDE require specific file extensions?**
   - Yes → [Custom Extensions](./custom-extensions.md)

4. **Does IDE need dynamic frontmatter?**
   - Yes → [Conditional Frontmatter](./conditional-frontmatter.md)

5. **Does IDE need comprehensive metadata?**
   - Yes → [Metadata-Rich](./metadata-rich.md)

6. **Does IDE require specific file names?**
   - Yes → [File Renaming](./file-renaming.md)

## Combining Patterns

Most adapters combine multiple patterns:

- **Cursor IDE:** Flat + Custom Extensions + File Renaming
- **Google Antigravity:** Nested + Package Versioning + Conditional Frontmatter + File Renaming
- **Simple IDE:** Flat + Conditional Frontmatter
- **Advanced IDE:** Nested + Metadata-Rich + Custom Extensions

## Template

Start with this minimal template, then add patterns as needed:

```yaml
name: my-ide
version: "1.0.0"
description: "My IDE adapter"

config:
  targetDir:
    default: ".myide"

mapping:
  path: "{{ config.targetDir.default }}/{{ spec.name }}.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
```

Then enhance with patterns from the examples above.
