# Conditional Frontmatter

Examples for adapters with dynamic frontmatter based on conditions and spec properties.

## When to Use

- IDE requires different metadata for different types
- Optional fields need conditional handling
- Dynamic frontmatter based on spec values
- Type-specific metadata requirements

## Example 1: Basic Conditional

```yaml
name: conditional-basic
version: "1.0.0"

mapping:
  path: ".config/{{ spec.name }}.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    
    - when: "spec.description"
      then:
        description: "{{ spec.description }}"
    
    - when: "spec.tags"
      then:
        tags: "{{ spec.tags }}"
```

**Features:** Only adds frontmatter fields when spec has those properties

## Example 2: Type-Specific Behavior

```yaml
name: conditional-type
version: "1.0.0"

config:
  targetDir:
    rule: ".rules"
    skill: ".skills"

mapping:
  path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}/index.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    
    - when: "spec.type | equals('rule')"
      then:
        priority: 100
        enabled: true
    
    - when: "spec.type | equals('skill')"
      then:
        category: "development"
        manual: true
  
  rename:
    - from: "index.md"
      to: "RULE.md"
      when: "spec.type | equals('rule')"
    
    - from: "index.md"
      to: "SKILL.md"
      when: "spec.type | equals('skill')"
```

**Features:** Different frontmatter and file names based on resource type

## Example 3: Trigger-Based Conditions

```yaml
name: conditional-trigger
version: "1.0.0"

mapping:
  path: ".ide/{{ spec.name }}.md"
  
  frontmatter:
    - key: title
      value: "{{ spec.title }}"
    
    - when: "spec.trigger | equals('always')"
      then:
        alwaysApply: true
    
    - when: "spec.trigger | equals('glob')"
      then:
        globs: "{{ spec.patterns }}"
    
    - when: "spec.trigger | equals('manual')"
      then:
        manual: true
```

**Features:** Frontmatter adapts based on trigger type

## Key Characteristics

- `when` clause for conditions
- `then` block for conditional output
- Filter expressions (`equals`, `contains`, etc.)
- Optional field handling
- Type-based logic

## Common Patterns

### Optional Fields
```yaml
- when: "spec.description"
  then:
    description: "{{ spec.description }}"
```

### Equality Check
```yaml
- when: "spec.type | equals('rule')"
  then:
    priority: 100
```

### Array Handling
```yaml
- when: "spec.patterns"
  then:
    globs: "{{ spec.patterns | join(', ') }}"
```

### Nested Objects
```yaml
- when: "spec.author"
  then:
    author:
      name: "{{ spec.author.name }}"
      email: "{{ spec.author.email }}"
```
