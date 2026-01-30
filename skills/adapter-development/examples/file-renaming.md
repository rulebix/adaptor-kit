# File Renaming Patterns

Examples for adapters that need to rename files during transformation.

## When to Use

- IDE requires specific file names
- Type-specific naming conventions
- Extension changes needed
- `index.md` to custom names
- Conditional file naming

## Example 1: Basic Renaming

```yaml
name: basic-rename
version: "1.0.0"

mapping:
  path: ".config/{{ spec.name }}/index.md"
  
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.md"
```

**Transform:** `index.md` → `my-rule.md`

## Example 2: Type-Based Renaming

```yaml
name: type-rename
version: "1.0.0"

mapping:
  path: ".config/{{ spec.type }}/{{ spec.name }}/index.md"
  
  rename:
    - from: "index.md"
      to: "RULE.md"
      when: "spec.type | equals('rule')"
    
    - from: "index.md"
      to: "SKILL.md"
      when: "spec.type | equals('skill')"
    
    - from: "index.md"
      to: "WORKFLOW.md"
      when: "spec.type | equals('workflow')"
```

**Transform:**
- Rules: `index.md` → `RULE.md`
- Skills: `index.md` → `SKILL.md`
- Workflows: `index.md` → `WORKFLOW.md`

## Example 3: Extension Change

```yaml
name: extension-rename
version: "1.0.0"

mapping:
  path: ".cursor/rules/{{ spec.name }}/index.md"
  
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.mdc"
```

**Transform:** `index.md` → `my-rule.mdc`

## Example 4: Multiple Renames

```yaml
name: multi-rename
version: "1.0.0"

mapping:
  path: ".config/{{ spec.name }}/index.md"
  
  rename:
    - from: "index.md"
      to: "README.md"
    
    - from: "examples.md"
      to: "EXAMPLES.md"
    
    - from: "testing.md"
      to: "TESTING.md"
```

**Transform:** Multiple files renamed with uppercase convention

## Example 5: Conditional with Default

```yaml
name: conditional-rename
version: "1.0.0"

mapping:
  path: ".ide/{{ spec.name }}/index.md"
  
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.md"
      when: "spec.flatten | equals(true)"
```

**Transform:** Only renames if `spec.flatten` is true

## Key Characteristics

- `from` field: source filename
- `to` field: target filename (supports expressions)
- `when` clause: optional condition
- Multiple rename rules supported
- Processes in order

## Common Patterns

### Flatten Structure
```yaml
rename:
  - from: "index.md"
    to: "{{ spec.name }}.md"
```

### Type-Specific Names
```yaml
rename:
  - from: "index.md"
    to: "RULE.md"
    when: "spec.type | equals('rule')"
```

### Extension Change
```yaml
rename:
  - from: "index.md"
    to: "{{ spec.name }}.mdc"
```

### Uppercase Convention
```yaml
rename:
  - from: "index.md"
    to: "README.md"
```

## Important Notes

- Rename happens after file generation
- Path must include original filename
- Expressions evaluated at runtime
- Conditions optional but recommended
- Order matters for multiple renames
