---
description: Generate Architecture Risk Assessment Report - Identify architectural risks from evolution patterns
---

# Architecture Risk Assessment Report

## Prerequisites
1. Read `tools/report-types.md` section "12. Architecture Risk Assessment Report"
2. Select appropriate git history sampling strategy (Significant Commits Only recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Significant Commits Only (commits with major changes):
```bash
# Find commits with significant changes (>100 lines added/removed)
git log --format="%H" -- [ARCH_FILE].arch.md | \
  while read commit; do
    lines=$(git show $commit --stat -- [ARCH_FILE].arch.md | tail -1 | awk '{print $4}')
    if [ "$lines" -gt 100 ]; then echo $commit; fi
  done
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md and identify architectural risks:

1. Identify risk indicators:
   - Rapid architecture changes (high change rate = instability risk)
   - Abandoned patterns (experimentation risk)
   - Incomplete migrations (migration risk)
   - Dependency risks (outdated, abandoned dependencies)
   - Complexity risks (rapid complexity growth)
   - Stability risks (frequent changes)
2. For each risk, assess:
   - Risk type (Stability, Migration, Dependency, Complexity, etc.)
   - Severity (High/Medium/Low)
   - Likelihood (High/Medium/Low)
   - Impact (High/Medium/Low)
   - Current status (Active, Mitigated, Resolved)
   - Risk date (when risk appeared)
3. Calculate risk metrics:
   - Overall risk score
   - Risk trend (increasing/decreasing)
   - Risk density (risks per month)
4. Identify risk patterns:
   - Common risk types
   - Risk clusters (multiple risks at same time)
   - Risk mitigation patterns
5. Create risk mitigation recommendations:
   - Priority risks to address
   - Mitigation strategies
   - Risk monitoring recommendations

Format as risk matrix with severity, likelihood, and mitigation plans.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include risk matrix (Severity × Likelihood)
3. Include risk timeline visualization
4. Include mitigation recommendations
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Risk matrix (Severity × Likelihood × Impact)
- Risk timeline
- Mitigation recommendations
- Risk metrics




