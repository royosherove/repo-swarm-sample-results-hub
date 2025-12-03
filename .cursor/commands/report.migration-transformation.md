---
description: Generate Migration & Transformation Report - Track architectural migrations and transformations
---

# Migration & Transformation Report

## Prerequisites
1. Read `tools/report-types.md` section "9. Migration & Transformation Report"
2. Select appropriate git history sampling strategy (Significant Commits Only recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Significant Commits Only (commits with major changes):
```bash
# Find commits with "add", "remove", "migrate" in message
git log --format="%H|%s" --grep="add\|remove\|migrate\|refactor" -- [ARCH_FILE].arch.md | \
  cut -d'|' -f1
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md and identify architectural migrations:

1. Identify all architectural migrations:
   - Architecture pattern migrations (e.g., Serverless → Microservices)
   - Technology migrations (e.g., requests → httpx)
   - Infrastructure migrations (e.g., Serverless Framework → Serverless + Terraform)
   - Data model migrations (schema changes)
   - Service migrations (service splits/merges)
2. For each migration, extract:
   - Start date (when migration began)
   - Completion date (when migration finished)
   - Migration duration
   - Migration type (pattern, technology, infrastructure, etc.)
   - Migration status (Completed, In Progress, Abandoned)
   - Migration rationale (why migration occurred)
3. Analyze migration patterns:
   - Successful migrations
   - Failed/abandoned migrations
   - Migration duration patterns
   - Migration frequency
4. Identify migration risks:
   - Long-running migrations
   - Abandoned migrations
   - Incomplete migrations
5. Calculate migration success rate

Format as migration timeline with status, duration, and outcomes.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include migration timeline visualization
3. Include success analysis
4. Include risk assessment
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Migration timeline
- Success analysis
- Risk assessment
- Status tracking (Completed, In Progress, Abandoned)




