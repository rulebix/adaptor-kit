# Metadata-Rich Adapters

Examples for IDEs that require comprehensive metadata and advanced features.

## When to Use

- IDE needs detailed metadata
- Complex frontmatter structure
- Nested metadata objects
- Advanced IDE features
- Rich information display

## Example 1: Comprehensive Metadata

```yaml
name: metadata-rich
version: "1.0.0"

config:
  targetDir:
    default: ".metadata"

mapping:
  path: "{{ config.targetDir.default }}/{{ spec.type }}/{{ spec.name }}.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    
    - key: package
      value:
        name: "{{ spec.packageName }}"
        version: "{{ spec.version }}"
    
    - when: "spec.author"
      then:
        author:
          name: "{{ spec.author.name }}"
          email: "{{ spec.author.email }}"
    
    - when: "spec.tags"
      then:
        tags: "{{ spec.tags }}"
    
    - when: "spec.dependencies"
      then:
        dependencies: "{{ spec.dependencies }}"
```

**Output Frontmatter:**
```yaml
---
title: My Rule
package:
  name: my-package
  version: 1.0.0
author:
  name: John Doe
  email: john@example.com
tags:
  - security
  - validation
---
```

## Example 2: Advanced Features

```yaml
name: advanced-metadata
version: "1.0.0"

mapping:
  path: ".advanced/{{ spec.name }}.md"
  
  frontmatter:
    - key: metadata
      value:
        id: "{{ spec.id }}"
        title: "{{ spec.title }}"
        type: "{{ spec.type }}"
        created: "{{ spec.created }}"
        updated: "{{ spec.updated }}"
    
    - key: configuration
      value:
        trigger: "{{ spec.trigger }}"
        priority: "{{ spec.priority | default(100) }}"
        enabled: "{{ spec.enabled | default(true) }}"
    
    - when: "spec.patterns"
      then:
        patterns:
          include: "{{ spec.patterns }}"
          exclude: "{{ spec.excludePatterns }}"
```

## Key Characteristics

- Nested frontmatter objects
- Comprehensive metadata
- Multiple metadata sections
- Default value handling
- Complex data structures

## Common Metadata Sections

### Package Information
```yaml
package:
  name: "{{ spec.packageName }}"
  version: "{{ spec.version }}"
  author: "{{ spec.author }}"
```

### Configuration
```yaml
configuration:
  trigger: "{{ spec.trigger }}"
  priority: "{{ spec.priority }}"
  enabled: true
```

### Patterns
```yaml
patterns:
  include: "{{ spec.patterns }}"
  exclude: "{{ spec.excludePatterns }}"
```

### Dependencies
```yaml
dependencies:
  requires: "{{ spec.requires }}"
  optional: "{{ spec.optional }}"
```

## Benefits

- Rich IDE integration
- Better discoverability
- Enhanced features
- Detailed documentation
- Advanced filtering
