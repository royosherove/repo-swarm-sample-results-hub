---
description: Generate Architecture Evolution Timeline Report - Visualize how architecture patterns and components change over time
---

# Architecture Evolution Timeline Report

## Prerequisites
1. Read `tools/report-types.md` section "1. Architecture Evolution Timeline Report"
2. Select appropriate git history sampling strategy (Time-Based Sampling recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Time-Based Sampling (one commit per month):
```bash
# Get one commit per month for last 12 months
COMMITS=$(git log --format="%H|%cd" --date=format:"%Y-%m" -- [ARCH_FILE].arch.md | \
  awk -F'|' '{if (!seen[$2]++) print $1}' | head -12)
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md using time-based sampling (one commit per month) and create a comprehensive timeline report showing:

1. Architecture pattern changes over time (identify when patterns changed and what they changed to)
2. Major component additions/removals with dates
3. Technology stack evolution timeline
4. Key architectural decisions with dates and rationale
5. Migration patterns (e.g., moving from one architecture pattern to another)

For each change, include:
- Date of change (from commit date)
- What changed (before → after)
- Commit hash for reference
- Brief description of the change

Format as a chronological timeline with visual indicators for major architectural shifts.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include timeline visualization (Mermaid diagram if relationships exist)
3. Format as chronological timeline with dates, before/after comparisons, commit references
4. Add report metadata with prompt used and commits analyzed

## Output Format
- Timeline with dates
- Before/after comparisons
- Commit references
- Visual indicators for major shifts




