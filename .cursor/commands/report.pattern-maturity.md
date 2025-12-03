---
description: Generate Architecture Pattern Maturity Report - Track how architectural patterns mature and stabilize over time
---

# Architecture Pattern Maturity Report

## Prerequisites
1. Read `tools/report-types.md` section "5. Architecture Pattern Maturity Report"
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
Analyze the git commit history of [ARCH_FILE].arch.md and create an architecture pattern maturity report:

1. Identify all architecture patterns mentioned across commits:
   - Event-Driven Architecture
   - Microservices
   - Layered Architecture
   - Repository Pattern
   - Hexagonal Architecture
   - CQRS
   - etc.
2. For each pattern, track:
   - First mention date
   - Last mention date
   - Frequency of mentions
   - Pattern refinement timeline (how description evolved)
   - Pattern stability indicators (consistent mentions = stable)
3. Identify patterns that:
   - Were introduced and maintained (mature)
   - Were introduced then abandoned (failed)
   - Were refined over time (maturing)
   - Were experimental (mentioned briefly)
4. Calculate pattern stability score (consistency of mentions)
5. Identify when patterns stabilized (stopped changing)

Create a pattern maturity matrix showing introduction date, stability date, and current status.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include pattern maturity matrix
3. Include stability timeline visualization
4. Include pattern lifecycle analysis
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Pattern maturity matrix
- Stability timeline
- Pattern lifecycle
- Status indicators (Mature, Maturing, Failed, Experimental)




