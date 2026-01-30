# Package Versioning Adapters

Examples for IDEs that support multiple package versions simultaneously.

## When to Use

- IDE needs to handle multiple versions of same package
- Version isolation required
- Package management features
- Dependency tracking needed

## Example 1: Package-Versioned

```yaml
name: package-versioned
version: "1.0.0"

config:
  targetDir:
    default: ".packages"

mapping:
  path: "{{ config.targetDir.default }}/{{ spec.packageName }}@{{ spec.version }}/{{ spec.type }}/{{ spec.name }}.md"
  
  frontmatter:
    title: "{{ spec.title }}"
    package: "{{ spec.packageName }}"
    version: "{{ spec.version }}"
```

**Output:** `.packages/my-package@1.0.0/rule/my-rule.md`

## Example 2: Google Antigravity (with versioning)

See [nested-structure.md](./nested-structure.md) for full example.

**Output:** `.agent/rules/my-package@1.0.0/my-rule/index.md`

## Key Characteristics

- Package name and version in path
- Version format: `packageName@version`
- Supports multiple versions side-by-side
- Clear version identification
- Easy version switching

## Path Pattern

```
.targetDir/{{ spec.packageName }}@{{ spec.version }}/{{ spec.type }}/{{ spec.name }}.md
```

## Benefits

- Multiple versions coexist
- No version conflicts
- Clear version tracking
- Easy rollback/upgrade
- Package isolation
