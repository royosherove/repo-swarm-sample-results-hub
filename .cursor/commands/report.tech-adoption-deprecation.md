---
description: Generate Technology Adoption & Deprecation Report - Track which technologies are added, removed, or replaced over time
---

# Technology Adoption & Deprecation Report

## Prerequisites
1. Read `tools/report-types.md` section "2. Technology Adoption & Deprecation Report"
2. Select appropriate git history sampling strategy (Time-Based Sampling recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Time-Based Sampling (one commit per month):
```bash
# Get one commit per month
COMMITS=$(git log --format="%H|%cd" --date=format:"%Y-%m" -- [ARCH_FILE].arch.md | \
  awk -F'|' '{if (!seen[$2]++) print $1}' | head -12)
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md and create a technology adoption/deprecation report:

1. List all technologies mentioned in the architecture file across all commits
2. For each technology, identify:
   - First appearance date (commit)
   - Last appearance date (if removed)
   - Version changes over time (if version numbers tracked)
   - Replacement patterns (e.g., Technology A replaced by Technology B)
3. Create a timeline showing technology lifecycle
4. Identify technologies that were:
   - Added but never removed (stable)
   - Added then removed (deprecated)
   - Replaced by alternatives (migrated)
5. Calculate technology churn rate (additions + removals per month)

Include a summary table with technology status (Active, Deprecated, Replaced) and dates.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include technology lifecycle table
3. Include adoption timeline visualization
4. Include churn metrics
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Technology lifecycle table
- Adoption timeline
- Churn metrics
- Status indicators (Active, Deprecated, Replaced)




