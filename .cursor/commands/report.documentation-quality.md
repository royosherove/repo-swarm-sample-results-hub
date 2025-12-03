---
description: Generate Architecture Documentation Quality Report - Track architectural documentation completeness and quality
---

# Architecture Documentation Quality Report

## Prerequisites
1. Read `tools/report-types.md` section "16. Architecture Documentation Quality Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md and assess documentation quality evolution:

1. Track documentation metrics:
   - Documentation length (lines, words)
   - Section count (number of sections)
   - Section completeness (required sections present)
   - Detail depth (level of detail)
   - Update frequency (how often updated)
2. Identify documentation improvements:
   - New sections added
   - Sections expanded
   - Sections refined
   - Quality improvements
3. Track documentation gaps:
   - Missing sections (required but absent)
   - Incomplete sections (started but not finished)
   - Outdated sections (not updated)
   - Quality issues
4. Calculate quality scores:
   - Completeness score (sections present / required)
   - Depth score (detail level)
   - Currency score (how up-to-date)
   - Overall quality score
5. Identify:
   - Documentation maturity timeline
   - Quality improvement periods
   - Documentation gaps
   - Quality trends

Format as quality metrics over time with gap analysis.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include quality metrics table
3. Include completeness analysis
4. Include gap identification
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Quality metrics
- Completeness analysis
- Gap identification
- Quality trends




