# Custom File Extensions

Examples for IDEs that require specific file extensions for different resource types.

## When to Use

- IDE uses file extensions for type detection
- Different extensions for rules, skills, workflows
- Extension-based syntax highlighting
- Type-specific file handling

## Example 1: Custom Extension by Type

```yaml
name: custom-extension
version: "1.0.0"

config:
  targetDir:
    rule: ".rules"
    skill: ".skills"
  
  extensions:
    rule: ".rule"
    skill: ".skill"
    default: ".md"

mapping:
  path: "{{ config.targetDir[spec.type] }}/{{ spec.name }}{{ config.extensions[spec.type] | default(config.extensions.default) }}"
  
  frontmatter:
    title: "{{ spec.title }}"
```

**Output:**
- Rules: `.rules/my-rule.rule`
- Skills: `.skills/my-skill.skill`

## Example 2: Cursor IDE (.mdc extension)

```yaml
name: cursor
version: "2.0"

config:
  targetDir:
    default: ".cursor/rules"

mapping:
  path: "{{ config.targetDir.default }}/{{ spec.name }}.mdc"
  
  frontmatter:
    - when: "spec.description"
      then:
        description: "{{ spec.description }}"
  
  rename:
    - from: "index.md"
      to: "{{ spec.name }}.mdc"
```

**Output:** `.cursor/rules/my-rule.mdc`

## Key Characteristics

- Type-specific extensions
- Extension mapping in config
- Default fallback extension
- Rename rules for extension changes
- IDE-specific file types

## Common Extensions

- `.md` - Standard markdown
- `.mdc` - Cursor markdown
- `.rule` - Rule files
- `.skill` - Skill files
- `.workflow` - Workflow files

## Implementation Pattern

```yaml
config:
  extensions:
    rule: ".rule"
    skill: ".skill"
    workflow: ".workflow"
    default: ".md"

mapping:
  path: "{{ targetDir }}/{{ spec.name }}{{ config.extensions[spec.type] | default(config.extensions.default) }}"
```
