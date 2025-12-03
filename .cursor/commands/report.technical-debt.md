---
description: Generate Technical Debt Identification Report - Identify architectural technical debt from commit patterns
---

# Technical Debt Identification Report

## Prerequisites
1. Read `tools/report-types.md` section "6. Technical Debt Identification Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md using significant commits only (focus on commits with major changes) and identify architectural technical debt:

1. Identify indicators of technical debt:
   - Rapid architecture changes (many commits in short time)
   - Experimental patterns that were abandoned
   - Incomplete migrations (started but not finished)
   - Architecture description inconsistencies
   - Missing architectural concerns (security, monitoring added late)
   - Pattern reversals (decisions undone)
2. For each debt indicator, identify:
   - When it occurred
   - What it indicates
   - Severity (High/Medium/Low)
   - Current status (Resolved, Ongoing, Unknown)
3. Calculate technical debt metrics:
   - Change frequency (commits per month)
   - Stability score (inverse of change rate)
   - Debt accumulation rate
4. Identify areas needing architectural attention
5. Prioritize technical debt by severity and impact

Format as technical debt inventory with severity, dates, and recommendations.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include technical debt inventory table
3. Include severity matrix
4. Include recommendations
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Technical debt inventory
- Severity matrix (High/Medium/Low)
- Recommendations
- Status tracking (Resolved, Ongoing, Unknown)




