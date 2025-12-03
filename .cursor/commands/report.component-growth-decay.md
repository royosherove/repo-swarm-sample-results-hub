---
description: Generate Component Growth & Decay Analysis - Track which architectural components grow, shrink, or disappear
---

# Component Growth & Decay Analysis

## Prerequisites
1. Read `tools/report-types.md` section "3. Component Growth & Decay Analysis"
2. Select appropriate git history sampling strategy (Adaptive Sampling recommended)
3. Identify target architecture file: `[SERVICE].arch.md`

## Execution Process

### Phase 1: Git History Sampling
Use Adaptive Sampling (more commits during high-change periods):
```bash
# Group commits by week, sample more from high-activity weeks
git log --format="%H|%cd" --date=format:"%Y-%W" -- [ARCH_FILE].arch.md | \
  awk -F'|' '{count[$2]++; commits[$2] = commits[$2] " " $1} END {
    for (week in count) {
      if (count[week] > 3) {
        print commits[week] | "head -2"
      } else {
        print commits[week] | "head -1"
      }
    }
  }'
```

### Phase 2: Analysis Prompt
Use this prompt with the sampled commits:

```
Analyze the git commit history of [ARCH_FILE].arch.md using adaptive sampling (more commits during high-change periods) and create a component growth/decay analysis:

1. Extract all architectural components mentioned (services, handlers, layers, modules, etc.)
2. For each component, track:
   - First mention date
   - Last mention date (if removed)
   - Frequency of mentions over time
   - Complexity indicators (sub-components, dependencies)
3. Identify components that:
   - Were added and remain (growing)
   - Were added then removed (decayed)
   - Were mentioned but never fully implemented
   - Grew in complexity over time
4. Calculate component addition rate and removal rate
5. Identify component proliferation patterns (e.g., many similar services added)

Create visualizations showing component count over time and component lifecycle.
```

### Phase 3: Report Generation
1. Create report in `reports/[report-title]/README.md`
2. Include component inventory table
3. Include growth charts (component count over time)
4. Include lifecycle analysis
5. Add report metadata with prompt used and commits analyzed

## Output Format
- Component inventory
- Growth charts
- Lifecycle analysis
- Proliferation patterns




