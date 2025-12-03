---
description: Generate Architecture Complexity Metrics - Measure architectural complexity evolution over time
---

# Architecture Complexity Metrics

## Prerequisites
1. Read `tools/report-types.md` section "8. Architecture Complexity Metrics"
2. Select appropriate git history sampling strategy (Adaptive Sampling recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Adaptive Sampling (more commits during high-change periods):
```bash
# Group commits by week, sample more from high-activity weeks
git log --format="%H|%cd" --date=format:"%Y-%W" -- [ARCH_FILE].arch.md | \
  awk -F'|' '{count[$2]++; commits[$2] = commits[$2] " " $1} END {
    for (week in count) {
      if (count[week] > 3) {
        print commits[week] | "head -2"
      } else {
        print commits[week] | "head -1"
      }
    }
  }'
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md using adaptive sampling (more commits during high-change periods) and calculate architecture complexity metrics:

1. Extract complexity indicators from each commit:
   - Component count (services, handlers, modules mentioned)
   - Service count (number of distinct services)
   - Pattern count (number of architecture patterns)
   - Dependency count (number of dependencies)
   - Architecture description length (lines/words)
   - Sub-component depth (layers, hierarchies)
2. Calculate metrics over time:
   - Component growth rate
   - Service proliferation rate
   - Pattern adoption rate
   - Complexity trend (increasing/decreasing/stable)
3. Identify complexity milestones:
   - When complexity increased significantly
   - When complexity decreased (simplification)
   - Complexity stabilization points
4. Calculate complexity scores:
   - Overall complexity score per commit
   - Component complexity score
   - Pattern complexity score
5. Identify complexity trends and predict future complexity

Create charts showing complexity metrics over time and trend analysis.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include complexity metrics charts
3. Include trend analysis
4. Include predictions
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Complexity metrics charts
- Trend analysis
- Predictions
- Milestone tracking




