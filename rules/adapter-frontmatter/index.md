---
id: adapter-frontmatter
title: Adapter Frontmatter Rules
description: Rules for frontmatter transformation in adapters
tags: 
  - frontmatter
  - metadata
  - transformation
---

# Adapter Frontmatter Rules

`mapping.frontmatter` defines how metadata transforms from generic spec to IDE-specific format.

## Basic Transformation

**Adapter Config:**
```yaml
mapping:
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    - key: description
      value: "{{ spec.description }}"
    - key: tags
      value: "{{ spec.tags }}"
```

## Formats

**Key-Value Pairs:**
```yaml
frontmatter:
  - key: title
    value: "{{ spec.title }}"
```

**Direct Object (Shorthand):**
```yaml
frontmatter:
  title: "{{ spec.title }}"
  description: "{{ spec.description }}"
```

**Conditional:**
```yaml
frontmatter:
  - key: title
    value: "{{ spec.title }}"
  
  - when: "spec.description"
    then:
      description: "{{ spec.description }}"
  
  - when: "spec.trigger | equals('glob')"
    then:
      globs: "{{ spec.patterns | join(', ') }}"
```

## Field Mapping

**Rename fields:**
```yaml
frontmatter:
  name: "{{ spec.title }}"        # title → name
  summary: "{{ spec.description }}" # description → summary
  keywords: "{{ spec.tags }}"      # tags → keywords
```

**Add static fields:**
```yaml
frontmatter:
  title: "{{ spec.title }}"
  enabled: true              # Static boolean
  version: "1.2.0"          # Static string
  priority: 1               # Static number
```

**Nested objects:**
```yaml
frontmatter:
  metadata:
    title: "{{ spec.title }}"
    version: "{{ spec.version }}"
    package: "{{ spec.packageName }}"
```

**Array handling:**
```yaml
frontmatter:
  tags: "{{ spec.tags }}"              # Full array
  primaryTag: "{{ spec.tags[0] }}"     # First element
  tagString: "{{ spec.tags | join(', ') }}" # Joined string
```

## IDE-Specific Examples

**Cursor:**
```yaml
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
```

**Google Antigravity:**
```yaml
frontmatter:
  - key: title
    value: "{{ spec.title }}"
  
  - key: trigger
    value: "{{ spec.trigger | default('always') }}"
  
  - when: "spec.description"
    then:
      description: "{{ spec.description }}"
```

## Best Practices

**Use conditionals for optional fields:**
```yaml
# Good
- when: "spec.description"
  then:
    description: "{{ spec.description }}"

# Bad (can be null)
description: "{{ spec.description }}"
```

**Provide fallbacks:**
```yaml
# Good
trigger: "{{ spec.trigger | default('always') }}"

# Bad (can be undefined)
trigger: "{{ spec.trigger }}"
```

**Use proper data types:**
```yaml
# Good
enabled: true              # boolean
priority: 100             # number
title: "{{ spec.title }}" # string

# Bad
enabled: "true"           # string instead of boolean
```

## Validation

✓ All required IDE fields in frontmatter
✓ Optional fields use conditional checks
✓ Fallbacks provided for missing data
✓ Data types match IDE requirements
✓ Array fields handled properly
✓ Nested objects structured correctly
✓ Static fields have valid values
