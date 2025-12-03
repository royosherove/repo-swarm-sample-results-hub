---
description: Generate Architectural Decision Record (ADR) Timeline - Extract and document architectural decisions from commit history
---

# Architectural Decision Record (ADR) Timeline

## Prerequisites
1. Read `tools/report-types.md` section "4. Architectural Decision Record (ADR) Timeline"
2. Select appropriate git history sampling strategy (Significant Commits Only recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Significant Commits Only (commits with major changes):
```bash
# Find commits with "add", "remove", "migrate" in message or >100 lines changed
git log --format="%H|%s" --grep="add\|remove\|migrate\|refactor" -- [ARCH_FILE].arch.md | \
  cut -d'|' -f1
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md using significant commits only (commits with "add", "remove", "migrate", "refactor" in message or >100 lines changed) and extract architectural decisions:

1. Identify architectural decisions from commit messages and architecture changes:
   - Pattern changes (e.g., "Added Temporal workflow orchestration")
   - Technology additions/removals
   - Component architecture changes
   - Infrastructure changes
2. For each decision, extract:
   - Decision date (commit date)
   - Decision description (what was decided)
   - Rationale (inferred from changes or commit messages)
   - Alternatives considered (if mentioned)
   - Consequences (what changed as result)
   - Status (Implemented, Reversed, Modified)
3. Identify decision reversals (when decisions were undone)
4. Create ADR format entries for each major decision
5. Analyze decision impact (how much changed after decision)

Format as ADR entries with dates, context, decision, consequences, and status.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Format as ADR entries (one per decision)
3. Include decision timeline visualization
4. Include impact analysis
5. Add report metadata with prompt used and commits analyzed

## Output Format
- ADR entries (date, context, decision, consequences, status)
- Decision timeline
- Impact analysis
- Reversal tracking




