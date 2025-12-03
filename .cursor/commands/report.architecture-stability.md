---
description: Generate Architecture Stability Report - Measure architectural stability and change frequency
---

# Architecture Stability Report

## Prerequisites
1. Read `tools/report-types.md` section "10. Architecture Stability Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md and measure architectural stability:

1. Calculate stability metrics:
   - Commit frequency (commits per month)
   - Architecture description change rate
   - Component change frequency
   - Pattern change frequency
   - Technology change frequency
2. Identify stability periods:
   - High change periods (unstable)
   - Low change periods (stable)
   - Stabilization points (when changes slowed)
3. Calculate stability scores:
   - Overall architecture stability score
   - Component stability score
   - Pattern stability score
   - Technology stability score
4. Track stability trends:
   - Stability over time
   - Stability improvement/degradation
   - Current stability status
5. Identify factors affecting stability:
   - What caused instability
   - What led to stabilization
   - Stability patterns

Create stability trend charts and identify stable vs. volatile periods.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include stability metrics table
3. Include trend charts
4. Include stability periods identification
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Stability metrics
- Trend charts
- Stability periods (High/Low change periods)
- Stability scores




