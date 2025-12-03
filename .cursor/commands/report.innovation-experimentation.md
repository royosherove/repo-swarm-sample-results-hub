---
description: Generate Architecture Innovation & Experimentation Report - Track architectural experimentation and innovation
---

# Architecture Innovation & Experimentation Report

## Prerequisites
1. Read `tools/report-types.md` section "17. Architecture Innovation & Experimentation Report"
2. Select appropriate git history sampling strategy (Significant Commits Only recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Significant Commits Only (commits with major changes):
```bash
# Find commits with "add", "remove", "migrate" in message
git log --format="%H|%s" --grep="add\|remove\|migrate\|refactor\|experiment\|poc" -- [ARCH_FILE].arch.md | \
  cut -d'|' -f1
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md and track architectural innovation:

1. Identify experimental patterns:
   - Patterns mentioned briefly then removed
   - Experimental terminology (e.g., "Hexagonal Architecture")
   - Innovation attempts
   - Pattern experiments
2. Track innovation timeline:
   - When experiments started
   - When experiments ended
   - Experiment duration
   - Experiment outcomes (Success/Failure)
3. Identify successful innovations:
   - Experiments that became permanent
   - Innovations that were adopted
   - Successful pattern introductions
4. Identify failed innovations:
   - Experiments that were abandoned
   - Patterns that didn't work
   - Innovations that were reversed
5. Calculate innovation metrics:
   - Innovation rate (experiments per month)
   - Success rate (successful / total experiments)
   - Experimentation velocity
   - Innovation adoption rate
6. Analyze innovation patterns:
   - What types of innovations succeed
   - What types fail
   - Innovation best practices
   - Innovation risks

Format as innovation timeline with success/failure indicators and lessons learned.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include innovation timeline visualization
3. Include success analysis
4. Include lessons learned
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Innovation timeline
- Success analysis
- Lessons learned
- Innovation metrics




