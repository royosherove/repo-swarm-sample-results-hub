---
description: Generate Dependency Evolution Report - Track how external dependencies change over time
---

# Dependency Evolution Report

## Prerequisites
1. Read `tools/report-types.md` section "7. Dependency Evolution Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md and create a dependency evolution report:

1. Extract all dependencies mentioned in architecture descriptions:
   - Python packages
   - JavaScript packages
   - Infrastructure services
   - External APIs
   - Database systems
2. For each dependency, track:
   - First appearance date
   - Version changes (if tracked)
   - Last appearance date (if removed)
   - Replacement patterns (if replaced)
3. Identify dependencies that:
   - Were added and remain (stable)
   - Were added then removed (deprecated)
   - Were replaced by alternatives
   - Had version updates
4. Calculate dependency metrics:
   - Total dependencies over time
   - Dependency addition rate
   - Dependency removal rate
   - Dependency churn rate
5. Identify dependency risks:
   - Outdated versions
   - Abandoned dependencies
   - Security concerns

Create a dependency timeline and risk assessment.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include dependency timeline visualization
3. Include version tracking table
4. Include risk assessment
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Dependency timeline
- Version tracking
- Risk assessment
- Churn metrics




