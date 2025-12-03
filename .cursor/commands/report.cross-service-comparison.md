---
description: Generate Cross-Service Architecture Comparison Report - Compare architectural evolution across multiple services
---

# Cross-Service Architecture Comparison Report

## Prerequisites
1. Read `tools/report-types.md` section "11. Cross-Service Architecture Comparison Report"
2. Select appropriate git history sampling strategy (Time-Based Sampling recommended)
3. Identify multiple target architecture files: `[SERVICE1].arch.md`, `[SERVICE2].arch.md`, etc.

## Execution Process

### Phase 1: Git History Sampling
Use Time-Based Sampling for each service (one commit per month):
```bash
# For each service, get one commit per month
for SERVICE in [SERVICE1] [SERVICE2] [SERVICE3]; do
  COMMITS=$(git log --format="%H|%cd" --date=format:"%Y-%m" -- ${SERVICE}.arch.md | \
    awk -F'|' '{if (!seen[$2]++) print $1}' | head -12)
  echo "$SERVICE: $COMMITS"
done
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits from all services:

```
Analyze git commit history of multiple architecture files ([SERVICE1].arch.md, [SERVICE2].arch.md, etc.) and create a cross-service comparison:

1. For each service, extract:
   - Architecture patterns used
   - Technology stack
   - Component architecture
   - Evolution timeline
   - Key decisions
2. Compare across services:
   - Common patterns (used by multiple services)
   - Unique patterns (service-specific)
   - Technology adoption patterns
   - Evolution velocity (how fast architecture changes)
   - Maturity levels
3. Identify:
   - Architectural consistency across services
   - Best practices (patterns used by mature services)
   - Anti-patterns (patterns that were abandoned)
   - Standardization opportunities
4. Calculate:
   - Pattern adoption rate across services
   - Technology consistency score
   - Architectural diversity metrics
5. Create recommendations:
   - Patterns to standardize
   - Patterns to avoid
   - Best practices to adopt

Format as comparison matrix and best practices guide.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include comparison matrix
3. Include best practices guide
4. Include standardization recommendations
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Comparison matrix
- Best practices guide
- Standardization recommendations
- Consistency metrics




