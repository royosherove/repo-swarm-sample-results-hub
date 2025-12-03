---
description: Generate Architecture Compliance & Standards Report - Track adherence to architectural standards over time
---

# Architecture Compliance & Standards Report

## Prerequisites
1. Read `tools/report-types.md` section "13. Architecture Compliance & Standards Report"
2. Select appropriate git history sampling strategy (Time-Based Sampling quarterly recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Time-Based Sampling (one commit per quarter):
```bash
# Get one commit per quarter for last 4 quarters
COMMITS=$(git log --format="%H|%cd" --date=format:"%Y-Q%q" -- [ARCH_FILE].arch.md | \
  awk -F'|' '{if (!seen[$2]++) print $1}' | head -4)
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md and assess compliance with architectural standards:

1. Define architectural standards to check:
   - Pattern standards (e.g., must use Repository Pattern)
   - Technology standards (approved technology list)
   - Structure standards (required components)
   - Documentation standards (required sections)
   - Security standards (security considerations)
2. For each standard, track:
   - First compliance date (when standard was met)
   - Compliance status over time (Compliant/Non-Compliant)
   - Compliance gaps (when standards not met)
   - Compliance improvements (when gaps were filled)
3. Calculate compliance metrics:
   - Overall compliance score
   - Compliance trend (improving/degrading)
   - Compliance gaps count
   - Time to compliance (how long to meet standards)
4. Identify:
   - Standards consistently met
   - Standards inconsistently met
   - Standards never met
   - Standards abandoned
5. Create compliance recommendations:
   - Gaps to address
   - Standards to adopt
   - Compliance improvement plan

Format as compliance matrix with dates and status for each standard.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include compliance matrix
3. Include gap analysis
4. Include improvement plan
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Compliance matrix
- Gap analysis
- Improvement plan
- Compliance scores




