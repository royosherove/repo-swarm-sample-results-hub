---
description: Generate Architecture Performance & Scale Evolution Report - Track how architecture evolves to support performance/scale
---

# Architecture Performance & Scale Evolution

## Prerequisites
1. Read `tools/report-types.md` section "14. Architecture Performance & Scale Evolution"
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
Analyze the git commit history of [ARCH_FILE].arch.md and track performance/scale-related architectural changes:

1. Identify scale/performance indicators:
   - Scalability patterns (e.g., horizontal scaling mentions)
   - Caching strategies (Redis, CDN, etc.)
   - Database optimization patterns
   - Load balancing mentions
   - Performance optimization indicators
   - Infrastructure scaling patterns
2. Track evolution of:
   - Caching strategies (when added, how evolved)
   - Database patterns (optimization, scaling)
   - Infrastructure scaling (auto-scaling, etc.)
   - Performance optimizations
3. Identify scale-related decisions:
   - When scaling concerns were addressed
   - What scaling solutions were adopted
   - Scaling pattern evolution
4. Calculate scale maturity:
   - Scale readiness score
   - Performance optimization score
   - Infrastructure scalability score
5. Identify:
   - Scaling milestones
   - Performance improvements
   - Scale-related risks
   - Future scaling needs

Format as scale evolution timeline with scaling decisions and patterns.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include scale evolution timeline visualization
3. Include scaling patterns analysis
4. Include maturity assessment
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Scale evolution timeline
- Scaling patterns
- Maturity assessment
- Future scaling needs




