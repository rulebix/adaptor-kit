---
title: Testing Adapters
description: Guide for testing custom IDE adapters
tags: 
  - testing
  - validation
  - quality-assurance
---

# Testing Adapters

Guide for testing and validating custom IDE adapters.

## Test Strategy

**Unit Testing** - Test individual components
**Integration Testing** - Test with real specs
**Edge Case Testing** - Test with missing/empty fields

## Test Cases

### Case 1: Basic Rule

**Input:**
```yaml
id: auth-rule
type: rule
title: Authentication Rule
description: Validates authentication
```

**Expected:**
```
.myide/rules/auth-rule.md
---
title: Authentication Rule
description: Validates authentication
---
```

### Case 2: Rule with Patterns

**Input:**
```yaml
id: typescript-rule
type: rule
patterns: ["*.ts", "*.tsx"]
trigger: glob
```

**Expected:**
```
.myide/rules/typescript-rule.md
---
globs: *.ts, *.tsx
---
```

### Case 3: Skill

**Input:**
```yaml
id: api-skill
type: skill
title: API Development
```

**Expected:**
```
.myide/skills/api-skill.md
---
title: API Development
---
```

### Case 4: Edge Cases

```yaml
# Missing optional fields
id: no-description
type: rule
title: No Description

# Empty arrays
id: empty-tags
type: rule
tags: []

# Special characters
id: special-chars
title: "Rule with 'quotes'"
```

## Validation

**YAML Syntax:**
✓ Valid YAML ✓ Proper indentation ✓ Quoted strings ✓ Valid data types

**Path Generation:**
✓ Paths correct ✓ Directories created ✓ Extensions correct ✓ No path traversal

**Frontmatter:**
✓ Required fields present ✓ Optional fields handled ✓ Data types correct ✓ Arrays formatted ✓ Nested objects structured

**Expressions:**
✓ All valid ✓ Variables exist ✓ Fallbacks work ✓ Filters applied ✓ Conditionals evaluate

**Edge Cases:**
✓ Missing fields handled ✓ Empty arrays handled ✓ Null values handled ✓ Special chars escaped ✓ Long values handled

## Common Issues

**Invalid Path:**
```yaml
# Bad
path: "{{ config.targetDir.rules }}/{{ spec.name }}.md"

# Good
path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}.md"
```

**Missing Frontmatter:**
```yaml
# Bad
description: "{{ spec.description }}"

# Good
- when: "spec.description"
  then:
    description: "{{ spec.description }}"
```

**Wrong Data Type:**
```yaml
# Bad
alwaysApply: "true"

# Good
alwaysApply: true
```

## Manual Testing Workflow

1. Create test specs with various scenarios
2. Apply adapter to test specs
3. Verify output files generated correctly
4. Check frontmatter transformed properly
5. Test in IDE for compatibility
6. Iterate based on results

## Quality Metrics

- **Coverage**: Test all features and edge cases
- **Accuracy**: Output matches expected format
- **Reliability**: Consistent results
- **Performance**: Fast generation
- **Compatibility**: Works with target IDE
