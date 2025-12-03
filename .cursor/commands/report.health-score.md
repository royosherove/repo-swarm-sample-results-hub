---
description: Generate Architecture Health Score Report - Overall architectural health metrics over time
---

# Architecture Health Score Report

## Prerequisites
1. Read `tools/report-types.md` section "18. Architecture Health Score Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md and calculate architecture health scores:

1. Define health components:
   - Stability (low change rate = healthy)
   - Completeness (all required components = healthy)
   - Consistency (consistent patterns = healthy)
   - Maturity (stable patterns = healthy)
   - Documentation (complete docs = healthy)
   - Standards compliance (meets standards = healthy)
2. Calculate component scores:
   - Stability score (inverse of change rate)
   - Completeness score (components present / required)
   - Consistency score (pattern consistency)
   - Maturity score (pattern stability)
   - Documentation score (doc quality)
   - Compliance score (standards met)
3. Calculate overall health score:
   - Weighted average of component scores
   - Health trend over time
   - Health milestones
4. Identify health factors:
   - What improves health
   - What degrades health
   - Health patterns
5. Create health recommendations:
   - Areas to improve
   - Health maintenance strategies
   - Health monitoring

Format as health score dashboard with component breakdowns and trends.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include health score dashboard
3. Include component breakdowns
4. Include trend analysis
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Health score dashboard
- Component scores breakdown
- Trend analysis
- Health recommendations




