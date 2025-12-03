---
description: Generate Architecture Future Prediction Report - Predict future architectural evolution based on patterns
---

# Architecture Future Prediction Report

## Prerequisites
1. Read `tools/report-types.md` section "20. Architecture Future Prediction Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md and predict future architectural evolution:

1. Identify trends:
   - Architecture pattern trends (what patterns are growing)
   - Technology trends (what technologies are being adopted)
   - Component trends (what components are growing)
   - Complexity trends (increasing/decreasing)
2. Extrapolate trends:
   - Pattern continuation predictions
   - Technology adoption predictions
   - Component growth predictions
   - Complexity predictions
3. Identify patterns:
   - Recurring patterns (what happens repeatedly)
   - Seasonal patterns (if any)
   - Growth patterns (exponential, linear, etc.)
4. Predict future changes:
   - Likely pattern additions
   - Likely technology adoptions
   - Likely component additions
   - Likely architectural shifts
5. Identify risks:
   - Trends that may reverse
   - Unsustainable growth patterns
   - Potential architectural issues
6. Create predictions:
   - Short-term predictions (next 1-3 months)
   - Medium-term predictions (next 3-6 months)
   - Long-term predictions (next 6-12 months)
   - Confidence levels for each prediction

Format as prediction report with timelines, confidence levels, and rationale.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include prediction timeline visualization
3. Include trend extrapolation
4. Include confidence levels
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Prediction timeline
- Trend extrapolation
- Confidence levels
- Risk identification




