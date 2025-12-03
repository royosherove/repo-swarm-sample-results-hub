---
description: Generate Architecture Cost Evolution Report - Track how architectural changes affect costs
---

# Architecture Cost Evolution Report

## Prerequisites
1. Read `tools/report-types.md` section "19. Architecture Cost Evolution Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md and identify cost-related architectural changes:

1. Identify cost indicators:
   - Infrastructure changes (may affect costs)
   - Technology additions (licensing costs)
   - Service proliferation (more services = more cost)
   - Scaling patterns (affects infrastructure cost)
   - Optimization patterns (may reduce costs)
2. Track cost-related changes:
   - Infrastructure additions (Terraform, new services)
   - Technology additions (new dependencies)
   - Service additions (more microservices)
   - Optimization additions (caching, etc.)
3. Identify cost implications:
   - Changes that likely increase costs
   - Changes that likely decrease costs
   - Changes with unclear cost impact
4. Calculate cost indicators:
   - Infrastructure complexity (proxy for cost)
   - Service count (proxy for cost)
   - Technology count (proxy for licensing)
5. Identify:
   - Cost optimization opportunities
   - Cost-increasing changes
   - Cost trends
   - Cost efficiency improvements

Format as cost impact analysis with cost indicators and optimization opportunities.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include cost impact analysis
3. Include optimization opportunities
4. Include trend analysis
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Cost impact analysis
- Optimization opportunities
- Trend analysis
- Cost indicators




