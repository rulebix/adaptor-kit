---
id: generate-adaptor
title: Generate Adaptor
description: Workflow for creating custom IDE adaptors by analyzing documentation and following available rules and skills
tags:
  - workflow
  - adaptor
  - development
type: workflow
---

# Generate Adaptor

This workflow guides the process of creating custom IDE adaptors for Rulebix.

## Step 1: Analyze IDE Documentation

Gather and analyze target IDE documentation to understand requirements:

-  @placeholder('ide-documentation')

**Output:** Understanding of file structure, frontmatter format, and IDE conventions

## Step 2: Apply Structure Rules

Create basic adaptor structure following rules:

- @rule('adapter-structure')
  - @placeholder('metadata')
  - Create `config` section with `targetDir`
  - Create `mapping` section with `path`

**Output:** Adaptor skeleton with valid structure

## Step 3: Implement Path Mapping

Determine how files will be placed in workspace:

- @rule('adapter-mapping')
  - Configure `mapping.path` according to IDE structure
  - Use kebab-case for output filenames (e.g., `{{ spec.name | kebab }}`)
  - Add `mapping.rename` if needed
  - Use expressions for dynamic paths

**Output:** Path mapping that matches IDE structure

## Step 4: Configure Frontmatter

Transform metadata from generic spec to IDE format:

- @rule('adapter-frontmatter')
  - Map required IDE fields
  - Add conditionals for optional fields
  - Use fallback values

**Output:** Complete frontmatter transformation

## Step 5: Implement Expressions

Use expression engine for dynamic values:

- @rule('adapter-expressions')
  - Use `{{ ... }}` syntax
  - Add fallbacks with `| default()`
  - Validate array access with conditionals

**Output:** Robust and safe expressions

## Step 6: Testing & Validation

Test adaptor with various scenarios:

- @skill('adapter-development') - See testing.md
  - Test with different resource types (rule, skill, workflow)
  - Validate output file structure
  - Check frontmatter transformation
  - Test edge cases (missing fields, empty arrays)

**Output:** Tested and production-ready adaptor

## Step 7: Documentation & Examples

Complete with documentation and examples:

- @skill('adapter-development') - See examples.md
  - Add usage examples
  - Document special configurations
  - Provide troubleshooting guide

**Output:** Well-documented adaptor

## Step 8: Save Adaptor File

Save the adaptor with kebab-case filename:

- Use kebab-case format for the YML filename (e.g., `my-ide-adaptor.yml`)
- Filename should match the adaptor name in metadata
- Add comprehensive comments in the YML file:
  - Header comment with adaptor name and description
  - Section separators (e.g., `# ============================================================`)
  - Inline comments explaining each configuration option
  - Examples in comments where helpful
- Place in appropriate direc

- @skill('adapter-development')
- @rule('adapter-structure')
- @rule('adapter-mapping')
- @rule('adapter-frontmatter')
- @rule('adapter-expressions')