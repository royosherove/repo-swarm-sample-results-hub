---
description: Create a new report from a natural language request
---

# Report Generation Rule

## Prerequisites
1. Read all `*.arch.md` files (exclude folders: `prompts`, `diagrams`, `reports`)
2. Apply all cursor rules from `.cursor/rules/` folder if it exists, or `agents.md` or other llm rules folders and files
3. Ignore `architecture-hub.arch.md` unless explicitly requested

## Core Principles
- **FACTS ONLY**: Every statement must be backed by specific file locations and line references
- **No hallucinations**: Uncertain information goes in "⚠️ Unverified Items" section
- **Name normalization**: Treat variants as identical (e.g., `llamaindex` = `llama-index`)
- **Search in files**: search across ALL repos always initially. do not use repo names to decide what should or should not be investigates, since repos can contain things that might not seem related to their name. i.e if you search for "dog", you should not filter for repos whoes names contain dog, but search "dog" inside all arch.md files.
- **Verification**: Double-check for false positives and missing information

## Execution Process

### Phase 1: Planning
1. Create `report/.memory/REPORT_PLAN.md`
2. Document:
   - Search strategy
   - Files to analyze
   - Expected output structure
   - CLI tools needed (from your rules or in `mise.toml`)

### Phase 2: Research
1. Execute searches using available CLI tools
2. Extract facts with file references (format: `file.md:line`)
3. Update `REPORT_PLAN.md` with progress after each major step
4. Track uncertain items separately

### Phase 3: Report Generation

**Standard Report Structure:**

```
# [Report Title]

## Executive Summary
[2-3 paragraph overview of key findings]

## Findings Summary
| Item | Category | Location | Quick Summary |
|------|----------|----------|---------------|
| ...  | ...      | ...      | ...           |

[Use sub-groupings if multiple hierarchy levels exist]

## Architecture Diagram
[Include Mermaid diagram ONLY if relationships exist between items]

## Detailed Findings

### [Item 1]
- **Location**: `path/to/file.md:lines`
- **Details**: [comprehensive details]
- **Related Items**: [if applicable]

[Repeat for each item]

## ⚠️ Unverified Items
[Items requiring clarification, marked with asterisks]

## Reproducibility

### Report Metadata
- **Generated**: [timestamp]
- **Model**: [model name and version]
- **Prompt**: 
  ```
  [exact prompt used]
  ```
- **Context Files**: 
  - [list of files analyzed]
- **CLI Tools Used**: 
  - [commands executed]
```

## Quality Checklist
Before finalizing, verify:
- [ ] All facts have file references
- [ ] No false positives included
- [ ] No relevant items missed
- [ ] Name variants normalized
- [ ] `architecture-hub.arch.md` excluded (unless requested)
- [ ] Plan file updated with final status
- [ ] Diagram included only if relationships exist

## Tool Usage
- Leverage CLI tools from cursor rules
- Use `mise` tools from `mise.toml`
- Create new reusable tools in `mise.toml` as needed
- Document tool usage in report metadata
