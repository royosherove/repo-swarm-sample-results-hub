- report types over time
# Architecture Evolution Report Types & Generation Prompts

**Purpose:** This document contains descriptions and prompts for generating various architecture evolution reports based on git commit history analysis of architecture documentation files.

**Usage:** Use these prompts with an AI assistant or analysis tool to generate specific reports from architecture file commit history.

---

## 1. Architecture Evolution Timeline Report

**Purpose:** Visualize how architecture patterns and components change over time

**Contents:**
- Timeline of architecture pattern changes
- Component addition/removal dates
- Technology stack evolution
- Major architectural decisions with dates
- Migration patterns (e.g., moving from one pattern to another)

**Value:**
- Understand architectural maturity journey
- Identify inflection points in architecture evolution
- Track architectural decision velocity

**Example Insights:**
- "Temporal was introduced in August 2025, marking shift from stateless to stateful architecture"
- "Architecture pattern changed 3 times in 5 months, indicating experimentation phase"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md using time-based sampling (one commit per month) and create a comprehensive timeline report showing:

1. Architecture pattern changes over time (identify when patterns changed and what they changed to)
2. Major component additions/removals with dates
3. Technology stack evolution timeline
4. Key architectural decisions with dates and rationale
5. Migration patterns (e.g., moving from one architecture pattern to another)

For each change, include:
- Date of change (from commit date)
- What changed (before → after)
- Commit hash for reference
- Brief description of the change

Format as a chronological timeline with visual indicators for major architectural shifts.
```

**Output Format:** Timeline with dates, before/after comparisons, commit references

---

## 2. Technology Adoption & Deprecation Report

**Purpose:** Track which technologies are added, removed, or replaced over time

**Contents:**
- Technology adoption timeline
- Technology removal/deprecation dates
- Replacement patterns (e.g., `requests` → `httpx`)
- Technology lifecycle analysis
- Dependency version evolution

**Value:**
- Identify technology churn
- Understand technology migration patterns
- Track dependency management maturity
- Identify potential technical debt from outdated tech

**Example Insights:**
- "HTTP client library changed from `requests` to `httpx` in October 2025"
- "Temporal SDK adoption took 1 month from first mention to full integration"
- "No technologies deprecated in 5-month period, indicating stable stack"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and create a technology adoption/deprecation report:

1. List all technologies mentioned in the architecture file across all commits
2. For each technology, identify:
   - First appearance date (commit)
   - Last appearance date (if removed)
   - Version changes over time (if version numbers tracked)
   - Replacement patterns (e.g., Technology A replaced by Technology B)
3. Create a timeline showing technology lifecycle
4. Identify technologies that were:
   - Added but never removed (stable)
   - Added then removed (deprecated)
   - Replaced by alternatives (migrated)
5. Calculate technology churn rate (additions + removals per month)

Include a summary table with technology status (Active, Deprecated, Replaced) and dates.
```

**Output Format:** Technology lifecycle table, adoption timeline, churn metrics

---

## 3. Component Growth & Decay Analysis

**Purpose:** Track which architectural components grow, shrink, or disappear

**Contents:**
- Component addition timeline
- Component removal timeline
- Component complexity evolution (measured by mentions/details)
- Service proliferation patterns
- Component dependency changes

**Value:**
- Identify architectural bloat
- Understand service proliferation
- Track component lifecycle
- Identify consolidation opportunities

**Example Insights:**
- "Trackable entities system added in August, expanded in October"
- "Feature flags infrastructure mentioned in August, fully documented by November"
- "No components removed, only additions - potential architectural growth"

**Prompt:**
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

**Output Format:** Component inventory, growth charts, lifecycle analysis

---

## 4. Architectural Decision Record (ADR) Timeline

**Purpose:** Extract and document architectural decisions from commit history

**Contents:**
- Decision dates from commit messages/descriptions
- Decision rationale (inferred from changes)
- Decision outcomes (what changed as result)
- Decision reversals (when decisions were undone)
- Decision impact analysis

**Value:**
- Understand why architecture evolved
- Learn from past decisions
- Avoid repeating mistakes
- Document architectural rationale

**Example Insights:**
- "Decision to add Temporal (August 2025) - Rationale: Need long-running processes"
- "Decision to remove Hexagonal Architecture terminology (September 2025) - Rationale: Too theoretical"
- "Decision to enhance pattern documentation (October 2025) - Rationale: Improve clarity"

**Prompt:**
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

**Output Format:** ADR entries, decision timeline, impact analysis

---

## 5. Architecture Pattern Maturity Report

**Purpose:** Track how architectural patterns mature and stabilize over time

**Contents:**
- Pattern introduction dates
- Pattern refinement timeline
- Pattern stabilization indicators
- Pattern abandonment (if any)
- Pattern consistency metrics

**Value:**
- Understand architectural maturity curve
- Identify when patterns stabilize
- Track pattern adoption success
- Identify patterns that didn't work

**Example Insights:**
- "Event-Driven pattern introduced in July, stabilized by September"
- "Repository Pattern explicitly documented in October, indicating maturity"
- "Hexagonal Architecture pattern attempted in August, abandoned in September"

**Prompt:**
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

**Output Format:** Pattern maturity matrix, stability timeline, pattern lifecycle

---

## 6. Technical Debt Identification Report

**Purpose:** Identify architectural technical debt from commit patterns

**Contents:**
- Rapid architecture changes (indicating instability)
- Experimental patterns that were abandoned
- Incomplete migrations (started but not finished)
- Architecture description inconsistencies
- Missing architectural concerns

**Value:**
- Identify areas needing architectural attention
- Track technical debt accumulation
- Prioritize architectural improvements
- Understand architectural risk areas

**Example Insights:**
- "Architecture pattern changed 3 times in 2 months - potential instability"
- "Temporal integration started in August but not fully documented until November"
- "Security concerns not addressed until August - 1 month gap"

**Prompt:**
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

**Output Format:** Technical debt inventory, severity matrix, recommendations

---

## 7. Dependency Evolution Report

**Purpose:** Track how external dependencies change over time

**Contents:**
- Dependency addition timeline
- Dependency version updates
- Dependency removal timeline
- Dependency replacement patterns
- Dependency risk analysis (outdated versions)

**Value:**
- Understand dependency management maturity
- Identify dependency churn
- Track security updates
- Plan dependency upgrades

**Example Insights:**
- "5 new dependencies added in August (Temporal, Terraform, etc.)"
- "HTTP client dependency replaced: requests → httpx in October"
- "No dependency removals in 5-month period"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and create a dependency evolution report:

1. Extract all dependencies mentioned in architecture descriptions:
   - Python packages
   - JavaScript packages
   - Infrastructure services
   - External APIs
   - Database systems
2. For each dependency, track:
   - First appearance date
   - Version changes (if tracked)
   - Last appearance date (if removed)
   - Replacement patterns (if replaced)
3. Identify dependencies that:
   - Were added and remain (stable)
   - Were added then removed (deprecated)
   - Were replaced by alternatives
   - Had version updates
4. Calculate dependency metrics:
   - Total dependencies over time
   - Dependency addition rate
   - Dependency removal rate
   - Dependency churn rate
5. Identify dependency risks:
   - Outdated versions
   - Abandoned dependencies
   - Security concerns

Create a dependency timeline and risk assessment.
```

**Output Format:** Dependency timeline, version tracking, risk assessment

---

## 8. Architecture Complexity Metrics

**Purpose:** Measure architectural complexity evolution over time

**Contents:**
- Component count over time
- Service count over time
- Pattern count over time
- Dependency count over time
- Architecture description length/complexity

**Value:**
- Track architectural growth
- Identify complexity trends
- Understand architectural evolution rate
- Identify simplification opportunities

**Example Insights:**
- "Component count increased from 5 to 12 over 5 months"
- "Architecture description grew from 1,389 to 4,300+ lines"
- "Complexity growth rate: 210% in first month, then stabilized"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md using adaptive sampling (more commits during high-change periods) and calculate architecture complexity metrics:

1. Extract complexity indicators from each commit:
   - Component count (services, handlers, modules mentioned)
   - Service count (number of distinct services)
   - Pattern count (number of architecture patterns)
   - Dependency count (number of dependencies)
   - Architecture description length (lines/words)
   - Sub-component depth (layers, hierarchies)
2. Calculate metrics over time:
   - Component growth rate
   - Service proliferation rate
   - Pattern adoption rate
   - Complexity trend (increasing/decreasing/stable)
3. Identify complexity milestones:
   - When complexity increased significantly
   - When complexity decreased (simplification)
   - Complexity stabilization points
4. Calculate complexity scores:
   - Overall complexity score per commit
   - Component complexity score
   - Pattern complexity score
5. Identify complexity trends and predict future complexity

Create charts showing complexity metrics over time and trend analysis.
```

**Output Format:** Complexity metrics charts, trend analysis, predictions

---

## 9. Migration & Transformation Report

**Purpose:** Track architectural migrations and transformations

**Contents:**
- Architecture pattern migrations
- Technology migrations
- Infrastructure migrations
- Data model migrations
- Service migrations

**Value:**
- Understand migration patterns
- Learn from migration experiences
- Plan future migrations
- Track migration success/failure

**Example Insights:**
- "Migration from serverless-only to serverless + Temporal (August 2025)"
- "Infrastructure migration: Serverless Framework → Serverless + Terraform"
- "No failed migrations identified in commit history"

**Prompt:**
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

**Output Format:** Migration timeline, success analysis, risk assessment

---

## 10. Architecture Stability Report

**Purpose:** Measure architectural stability and change frequency

**Contents:**
- Change frequency metrics
- Architecture description volatility
- Component stability scores
- Pattern stability scores
- Stability trends over time

**Value:**
- Understand architectural maturity
- Identify stable vs. volatile areas
- Plan architectural work
- Measure architectural health

**Example Insights:**
- "Architecture stabilized after August (high change month)"
- "Pattern descriptions stable after September"
- "Component additions slowed after initial expansion phase"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and measure architectural stability:

1. Calculate stability metrics:
   - Commit frequency (commits per month)
   - Architecture description change rate
   - Component change frequency
   - Pattern change frequency
   - Technology change frequency
2. Identify stability periods:
   - High change periods (unstable)
   - Low change periods (stable)
   - Stabilization points (when changes slowed)
3. Calculate stability scores:
   - Overall architecture stability score
   - Component stability score
   - Pattern stability score
   - Technology stability score
4. Track stability trends:
   - Stability over time
   - Stability improvement/degradation
   - Current stability status
5. Identify factors affecting stability:
   - What caused instability
   - What led to stabilization
   - Stability patterns

Create stability trend charts and identify stable vs. volatile periods.
```

**Output Format:** Stability metrics, trend charts, stability periods

---

## 11. Cross-Service Architecture Comparison Report

**Purpose:** Compare architectural evolution across multiple services

**Contents:**
- Architecture pattern adoption across services
- Technology adoption patterns
- Component similarity analysis
- Evolution velocity comparison
- Best practice identification

**Value:**
- Identify architectural consistency
- Share architectural learnings
- Standardize patterns
- Understand architectural diversity

**Example Insights:**
- "Temporal adoption: ai-service (August), other-service (September)"
- "Common pattern: Event-driven microservices across 80% of services"
- "ai-service architecture more mature than average"

**Prompt:**
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

**Output Format:** Comparison matrix, best practices, standardization recommendations

---

## 12. Architecture Risk Assessment Report

**Purpose:** Identify architectural risks from evolution patterns

**Contents:**
- Rapid change indicators (risk)
- Abandoned patterns (risk)
- Incomplete migrations (risk)
- Dependency risks
- Complexity risks

**Value:**
- Proactive risk identification
- Prioritize risk mitigation
- Understand architectural health
- Plan risk reduction

**Example Insights:**
- "High change rate in August indicates architectural experimentation risk"
- "No abandoned patterns - low architectural risk"
- "Dependency growth rate acceptable - low risk"

**Prompt:**
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

**Output Format:** Risk matrix, risk timeline, mitigation recommendations

---

## 13. Architecture Compliance & Standards Report

**Purpose:** Track adherence to architectural standards over time

**Contents:**
- Pattern compliance timeline
- Standard adoption dates
- Compliance gaps
- Standard evolution
- Compliance trends

**Value:**
- Ensure architectural consistency
- Track standards adoption
- Identify compliance gaps
- Measure standards effectiveness

**Example Insights:**
- "Repository Pattern adopted in October - compliance improvement"
- "Layered Architecture consistently maintained"
- "No compliance violations detected"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and assess compliance with architectural standards:

1. Define architectural standards to check:
   - Pattern standards (e.g., must use Repository Pattern)
   - Technology standards (approved technology list)
   - Structure standards (required components)
   - Documentation standards (required sections)
   - Security standards (security considerations)
2. For each standard, track:
   - First compliance date (when standard was met)
   - Compliance status over time (Compliant/Non-Compliant)
   - Compliance gaps (when standards not met)
   - Compliance improvements (when gaps were filled)
3. Calculate compliance metrics:
   - Overall compliance score
   - Compliance trend (improving/degrading)
   - Compliance gaps count
   - Time to compliance (how long to meet standards)
4. Identify:
   - Standards consistently met
   - Standards inconsistently met
   - Standards never met
   - Standards abandoned
5. Create compliance recommendations:
   - Gaps to address
   - Standards to adopt
   - Compliance improvement plan

Format as compliance matrix with dates and status for each standard.
```

**Output Format:** Compliance matrix, gap analysis, improvement plan

---

## 14. Architecture Performance & Scale Evolution

**Purpose:** Track how architecture evolves to support performance/scale

**Contents:**
- Scalability pattern additions
- Performance optimization indicators
- Caching strategy evolution
- Database optimization patterns
- Infrastructure scaling patterns

**Value:**
- Understand scalability evolution
- Track performance improvements
- Plan for future scale
- Learn from scaling decisions

**Example Insights:**
- "Temporal added to support long-running processes (scale requirement)"
- "Redis caching consistently maintained"
- "No performance-related architectural changes identified"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and track performance/scale-related architectural changes:

1. Identify scale/performance indicators:
   - Scalability patterns (e.g., horizontal scaling mentions)
   - Caching strategies (Redis, CDN, etc.)
   - Database optimization patterns
   - Load balancing mentions
   - Performance optimization indicators
   - Infrastructure scaling patterns
2. Track evolution of:
   - Caching strategies (when added, how evolved)
   - Database patterns (optimization, scaling)
   - Infrastructure scaling (auto-scaling, etc.)
   - Performance optimizations
3. Identify scale-related decisions:
   - When scaling concerns were addressed
   - What scaling solutions were adopted
   - Scaling pattern evolution
4. Calculate scale maturity:
   - Scale readiness score
   - Performance optimization score
   - Infrastructure scalability score
5. Identify:
   - Scaling milestones
   - Performance improvements
   - Scale-related risks
   - Future scaling needs

Format as scale evolution timeline with scaling decisions and patterns.
```

**Output Format:** Scale evolution timeline, scaling patterns, maturity assessment

---

## 15. Architecture Team Velocity Report

**Purpose:** Understand architectural change velocity and team activity

**Contents:**
- Commit frequency over time
- Architecture change velocity
- Team activity patterns
- Architectural work distribution
- Velocity trends

**Value:**
- Understand team productivity
- Track architectural work pace
- Identify busy periods
- Plan architectural work

**Example Insights:**
- "42 architecture commits in 5 months - high activity"
- "Peak activity in August (major expansion)"
- "Activity stabilized after September"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and measure architectural change velocity:

1. Calculate velocity metrics:
   - Commit frequency (commits per month/week)
   - Architecture change rate (changes per commit)
   - Component addition rate (components per month)
   - Pattern adoption rate (patterns per month)
   - Documentation growth rate (lines per month)
2. Identify velocity patterns:
   - High velocity periods (busy periods)
   - Low velocity periods (quiet periods)
   - Velocity trends (increasing/decreasing)
   - Velocity stability
3. Correlate velocity with:
   - Major architectural changes
   - Team activity patterns
   - Project phases
4. Calculate:
   - Average velocity
   - Peak velocity
   - Velocity consistency
   - Velocity trends
5. Identify:
   - Velocity drivers (what causes high velocity)
   - Velocity blockers (what causes low velocity)
   - Optimal velocity range

Format as velocity charts and activity patterns over time.
```

**Output Format:** Velocity metrics, activity charts, trend analysis

---

## 16. Architecture Documentation Quality Report

**Purpose:** Track architectural documentation completeness and quality

**Contents:**
- Documentation completeness timeline
- Section addition dates
- Documentation depth evolution
- Quality metrics over time
- Documentation gaps

**Value:**
- Track documentation maturity
- Identify documentation gaps
- Plan documentation improvements
- Measure documentation quality

**Example Insights:**
- "Documentation expanded from 8 to 20+ sections in August"
- "Security documentation added in August - quality improvement"
- "Documentation stabilized after October"

**Prompt:**
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

**Output Format:** Quality metrics, completeness analysis, gap identification

---

## 17. Architecture Innovation & Experimentation Report

**Purpose:** Track architectural experimentation and innovation

**Contents:**
- Experimental pattern attempts
- Innovation timeline
- Experimentation success/failure
- Innovation adoption patterns
- Experimentation velocity

**Value:**
- Understand innovation culture
- Learn from experiments
- Track innovation success
- Identify innovation opportunities

**Example Insights:**
- "Hexagonal Architecture experimented in August, abandoned in September"
- "Temporal innovation successful - adopted permanently"
- "High experimentation rate indicates innovative culture"

**Prompt:**
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

**Output Format:** Innovation timeline, success analysis, lessons learned

---

## 18. Architecture Health Score Report

**Purpose:** Overall architectural health metrics over time

**Contents:**
- Health score calculation
- Health trend analysis
- Health component breakdown
- Health improvement recommendations
- Health comparison over time

**Value:**
- Overall architectural assessment
- Track architectural health trends
- Identify improvement areas
- Measure architectural maturity

**Example Insights:**
- "Architecture health score: 65% (July) → 85% (November)"
- "Health improved significantly after Temporal addition"
- "Stability improvements after September"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and calculate architecture health scores:

1. Define health components:
   - Stability (low change rate = healthy)
   - Completeness (all required components = healthy)
   - Consistency (consistent patterns = healthy)
   - Maturity (stable patterns = healthy)
   - Documentation (complete docs = healthy)
   - Standards compliance (meets standards = healthy)
2. Calculate component scores:
   - Stability score (inverse of change rate)
   - Completeness score (components present / required)
   - Consistency score (pattern consistency)
   - Maturity score (pattern stability)
   - Documentation score (doc quality)
   - Compliance score (standards met)
3. Calculate overall health score:
   - Weighted average of component scores
   - Health trend over time
   - Health milestones
4. Identify health factors:
   - What improves health
   - What degrades health
   - Health patterns
5. Create health recommendations:
   - Areas to improve
   - Health maintenance strategies
   - Health monitoring

Format as health score dashboard with component breakdowns and trends.
```

**Output Format:** Health score dashboard, component scores, trend analysis

---

## 19. Architecture Cost Evolution Report

**Purpose:** Track how architectural changes affect costs

**Contents:**
- Infrastructure cost indicators
- Technology cost changes
- Service proliferation costs
- Optimization opportunities
- Cost trend analysis

**Value:**
- Understand cost implications
- Track cost optimization
- Plan cost management
- Measure cost efficiency

**Example Insights:**
- "Temporal addition may increase infrastructure costs"
- "Serverless architecture maintained - cost-efficient"
- "No cost-reduction architectural changes identified"

**Prompt:**
```
Analyze the git commit history of [ARCH_FILE].arch.md and identify cost-related architectural changes:

1. Identify cost indicators:
   - Infrastructure changes (may affect costs)
   - Technology additions (licensing costs)
   - Service proliferation (more services = more cost)
   - Scaling patterns (affects infrastructure cost)
   - Optimization patterns (may reduce costs)
2. Track cost-related changes:
   - Infrastructure additions (Terraform, new services)
   - Technology additions (new dependencies)
   - Service additions (more microservices)
   - Optimization additions (caching, etc.)
3. Identify cost implications:
   - Changes that likely increase costs
   - Changes that likely decrease costs
   - Changes with unclear cost impact
4. Calculate cost indicators:
   - Infrastructure complexity (proxy for cost)
   - Service count (proxy for cost)
   - Technology count (proxy for licensing)
5. Identify:
   - Cost optimization opportunities
   - Cost-increasing changes
   - Cost trends
   - Cost efficiency improvements

Format as cost impact analysis with cost indicators and optimization opportunities.
```

**Output Format:** Cost impact analysis, optimization opportunities, trend analysis

---

## 20. Architecture Future Prediction Report

**Purpose:** Predict future architectural evolution based on patterns

**Contents:**
- Trend extrapolation
- Pattern continuation predictions
- Technology adoption predictions
- Component growth predictions
- Risk predictions

**Value:**
- Plan future architecture
- Anticipate changes
- Prepare for evolution
- Strategic planning

**Example Insights:**
- "Based on trends, expect continued Temporal expansion"
- "Pattern suggests architecture stabilization phase"
- "Technology stack likely to remain stable"

**Prompt:**
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

**Output Format:** Prediction timeline, trend extrapolation, confidence levels

---

## Git History Sampling Strategies for LLM Optimization

**Important:** Different report types require different sampling strategies to optimize token usage while maintaining report quality. Choose the appropriate strategy based on your report type and analysis needs.

### Strategy 1: Time-Based Sampling (Recommended for Most Reports)

**Best For:** Timeline reports, evolution tracking, pattern maturity, stability analysis

**Approach:** Select one representative commit per time period (e.g., monthly, quarterly)

**Implementation:**
```bash
# Get one commit per month
git log --format="%H|%cd" --date=format:"%Y-%m" -- [ARCH_FILE].arch.md | \
  awk -F'|' '{if (!seen[$2]++) print $1}' | \
  head -12  # Last 12 months
```

**Token Usage:** Low-Medium (~500-2000 tokens per commit × number of periods)

**Pros:**
- Predictable token usage
- Captures major changes over time
- Good for trend analysis
- Works well for LLM context windows

**Cons:**
- May miss rapid changes between samples
- Less detail on specific changes

**When to Use:**
- Reports covering long time periods (6+ months)
- Reports focused on trends and patterns
- When token budget is limited
- Reports 1, 2, 5, 10, 11, 14, 15, 18, 19, 20

---

### Strategy 2: Significant Commits Only (Recommended for Decision Tracking)

**Best For:** ADR timeline, technical debt, risk assessment, innovation tracking

**Approach:** Filter commits by:
- Commit message keywords (e.g., "add", "remove", "migrate", "refactor")
- File size changes (significant additions/deletions)
- Commit frequency (commits that break patterns)

**Implementation:**
```bash
# Find commits with significant changes (>100 lines added/removed)
git log --format="%H" -- [ARCH_FILE].arch.md | \
  while read commit; do
    lines=$(git show $commit --stat -- [ARCH_FILE].arch.md | tail -1 | awk '{print $4}')
    if [ "$lines" -gt 100 ]; then echo $commit; fi
  done
```

**Token Usage:** Medium (~1000-3000 tokens per significant commit)

**Pros:**
- Focuses on meaningful changes
- Captures architectural decisions
- Reduces noise from minor updates
- Good for decision-focused reports

**Cons:**
- Requires filtering logic
- May miss subtle but important changes
- Filtering criteria need tuning

**When to Use:**
- Reports focused on decisions and changes
- Reports 4, 6, 12, 17
- When you want to focus on major shifts

---

### Strategy 3: Adaptive Sampling (Recommended for Detailed Analysis)

**Best For:** Complexity metrics, migration tracking, component analysis

**Approach:** More commits during high-change periods, fewer during stable periods

**Implementation:**
```bash
# Identify high-change periods (many commits in short time)
# Then sample more frequently during those periods
git log --format="%H|%cd" --date=format:"%Y-%m-%d" -- [ARCH_FILE].arch.md | \
  # Group by week, count commits
  # Sample more commits from weeks with high activity
```

**Token Usage:** Medium-High (~2000-5000 tokens total)

**Pros:**
- Captures important periods in detail
- Reduces sampling during stable periods
- Better balance of detail vs. efficiency
- Adaptive to actual change patterns

**Cons:**
- More complex to implement
- Requires change rate analysis first
- May still miss some changes

**When to Use:**
- Reports needing detailed change tracking
- Reports 3, 7, 8, 9
- When you have moderate token budget

---

### Strategy 4: Incremental Diff Approach (Recommended for Token Efficiency)

**Best For:** All reports when token budget is very limited

**Approach:** Instead of full file content, use git diffs between selected commits

**Implementation:**
```bash
# Get diffs between monthly commits instead of full file content
git log --format="%H|%cd" --date=format:"%Y-%m" -- [ARCH_FILE].arch.md | \
  awk -F'|' '{if (!seen[$2]++) print $1}' | \
  while read commit; do
    git diff $commit^..$commit -- [ARCH_FILE].arch.md
  done
```

**Token Usage:** Very Low (~200-800 tokens per diff)

**Pros:**
- Most token-efficient approach
- Shows only what changed
- Good for understanding evolution
- Works well for large files

**Cons:**
- Requires understanding of diffs
- May lose context
- Harder to understand full state at each point
- LLMs may struggle with large diffs

**When to Use:**
- Very large architecture files (>5000 lines)
- Limited token budget
- Reports focused on changes rather than state
- All report types when token-constrained

---

### Strategy 5: All Commits (Use Sparingly)

**Best For:** Comprehensive analysis, small files, short time periods

**Approach:** Process every commit

**Token Usage:** High-Very High (depends on file size and commit count)

**Pros:**
- Complete picture
- No missed changes
- Most accurate analysis

**Cons:**
- Very high token usage
- May exceed LLM context limits
- Expensive for long histories
- May include noise

**When to Use:**
- Small architecture files (<1000 lines)
- Short time periods (<3 months)
- When completeness is critical
- Reports requiring full detail (rare)

---

## Recommended Strategy by Report Type

| Report Type | Recommended Strategy | Alternative Strategy | Token Budget |
|------------|---------------------|---------------------|--------------|
| 1. Evolution Timeline | Time-Based (monthly) | Adaptive | Low-Medium |
| 2. Technology Adoption | Time-Based (monthly) | Significant Commits | Low-Medium |
| 3. Component Growth | Adaptive | Time-Based (monthly) | Medium |
| 4. ADR Timeline | Significant Commits | Time-Based (monthly) | Medium |
| 5. Pattern Maturity | Time-Based (monthly) | Adaptive | Low-Medium |
| 6. Technical Debt | Significant Commits | Adaptive | Medium |
| 7. Dependency Evolution | Time-Based (monthly) | Incremental Diff | Low-Medium |
| 8. Complexity Metrics | Adaptive | Time-Based (monthly) | Medium |
| 9. Migration Report | Significant Commits | Adaptive | Medium |
| 10. Stability Report | Time-Based (monthly) | Adaptive | Low-Medium |
| 11. Cross-Service Comparison | Time-Based (monthly) | Incremental Diff | Low-Medium |
| 12. Risk Assessment | Significant Commits | Adaptive | Medium |
| 13. Compliance Report | Time-Based (quarterly) | Significant Commits | Low |
| 14. Performance/Scale | Time-Based (monthly) | Significant Commits | Low-Medium |
| 15. Team Velocity | Time-Based (weekly) | All Commits (if short period) | Medium |
| 16. Documentation Quality | Time-Based (monthly) | Incremental Diff | Low-Medium |
| 17. Innovation Report | Significant Commits | Adaptive | Medium |
| 18. Health Score | Time-Based (monthly) | Adaptive | Low-Medium |
| 19. Cost Evolution | Time-Based (monthly) | Significant Commits | Low-Medium |
| 20. Future Prediction | Time-Based (monthly) | Adaptive | Low-Medium |

---

## Token Budget Guidelines

### Low Budget (<5000 tokens)
- Use **Time-Based Sampling** with quarterly or bi-monthly intervals
- Use **Incremental Diff Approach** for change-focused reports
- Limit to 6-12 commits total
- Focus on summary-level reports

### Medium Budget (5000-15000 tokens)
- Use **Time-Based Sampling** with monthly intervals
- Use **Significant Commits** for decision-focused reports
- Limit to 12-24 commits total
- Can handle most report types

### High Budget (15000+ tokens)
- Use **Adaptive Sampling** for detailed analysis
- Use **Significant Commits** with more commits
- Can process 24-48 commits
- Can use **All Commits** for short periods (<3 months)

---

## Implementation Examples

### Example 1: Monthly Sampling for Evolution Timeline

```bash
# Get one commit per month for last 12 months
COMMITS=$(git log --format="%H|%cd" --date=format:"%Y-%m" -- ai-service.arch.md | \
  awk -F'|' '{if (!seen[$2]++) print $1}' | head -12)

# Process each commit
for commit in $COMMITS; do
  git show $commit:ai-service.arch.md > "arch-snapshot-$(git log -1 --format=%cd --date=format:%Y-%m $commit).md"
done
```

### Example 2: Significant Commits for ADR Timeline

```bash
# Find commits with "add", "remove", "migrate" in message
git log --format="%H|%s" --grep="add\|remove\|migrate\|refactor" -- ai-service.arch.md | \
  cut -d'|' -f1
```

### Example 3: Adaptive Sampling

```bash
# Group commits by week, sample more from high-activity weeks
git log --format="%H|%cd" --date=format:"%Y-%W" -- ai-service.arch.md | \
  awk -F'|' '{count[$2]++; commits[$2] = commits[$2] " " $1} END {
    for (week in count) {
      if (count[week] > 3) {
        # High activity: sample 2 commits
        print commits[week] | "head -2"
      } else {
        # Low activity: sample 1 commit
        print commits[week] | "head -1"
      }
    }
  }'
```

---

## Best Practices

1. **Start with Time-Based Sampling** - It's the safest default for most reports
2. **Adjust Based on Results** - If important changes are missed, use Adaptive or Significant Commits
3. **Use Incremental Diffs for Large Files** - When files exceed 3000 lines, prefer diffs
4. **Limit Time Range** - For very long histories (>2 years), consider analyzing in chunks
5. **Pre-filter Commits** - Remove merge commits and formatting-only commits when possible
6. **Cache Results** - Store processed commit snapshots to avoid reprocessing
7. **Monitor Token Usage** - Track actual token usage and adjust strategy accordingly

---

## Usage Instructions

### Git History Sampling

**Before generating any report**, first select the appropriate sampling strategy from the "Git History Sampling Strategies" section above. The strategy depends on:
- Your token budget
- The report type you're generating
- The size of your architecture file
- The time period you're analyzing

**Quick Reference:**
- **Most reports:** Use Time-Based Sampling (monthly)
- **Decision-focused reports:** Use Significant Commits Only
- **Detailed analysis:** Use Adaptive Sampling
- **Large files or tight budget:** Use Incremental Diff Approach

### Basic Usage

1. **Select sampling strategy** based on report type and token budget
2. **Extract commits** using the strategy's implementation script
3. **Replace `[ARCH_FILE]`** with the actual architecture file name (e.g., `ai-service`)
4. **Use the prompt** with your sampled commits

Example:
```
# Step 1: Sample commits (monthly)
COMMITS=$(git log --format="%H|%cd" --date=format:"%Y-%m" -- ai-service.arch.md | \
  awk -F'|' '{if (!seen[$2]++) print $1}' | head -12)

# Step 2: Use prompt with sampled commits
Analyze the git commit history of ai-service.arch.md (using the following commits: $COMMITS) and create...
```

### Advanced Usage

For cross-service analysis, replace `[SERVICE1]`, `[SERVICE2]` with actual service names:

```
Analyze git commit history of ai-service.arch.md, ordering-service.arch.md, and payment-service.arch.md...
```

### Customization

Each prompt can be customized by:
- Adding specific date ranges: "from July 2025 to November 2025"
- Focusing on specific aspects: "focus on Temporal-related changes"
- Adding comparison points: "compare with industry standards"
- Including specific metrics: "calculate complexity scores using cyclomatic complexity"

### Output Formatting

All prompts assume markdown output format. To request specific formats, add:
- "Format as JSON"
- "Format as CSV"
- "Format as HTML dashboard"
- "Include visualizations/charts"

---

## Report Generation Workflow

1. **Select Report Type** - Choose from the 20 report types above
2. **Customize Prompt** - Replace placeholders and add specific requirements
3. **Execute Analysis** - Run git analysis on architecture file commits
4. **Generate Report** - Use prompt with AI assistant or analysis tool
5. **Review & Refine** - Review output and refine if needed
6. **Save Report** - Store in appropriate reports directory

---

## Automation Opportunities

These prompts can be automated by:
- Creating a script that takes report type and architecture file as input
- Automatically extracting git commit history
- Generating the customized prompt
- Executing analysis
- Formatting and saving the report

Example automation:
```bash
./generate-report.sh --type "architecture-evolution-timeline" --file "ai-service"
```

---

## Report Combinations

Multiple reports can be combined for comprehensive analysis:

- **Architecture Health Dashboard** = Health Score + Stability + Risk Assessment
- **Architecture Maturity Assessment** = Pattern Maturity + Complexity + Documentation Quality
- **Architecture Roadmap** = Future Prediction + Migration Report + Technology Adoption
- **Architecture Audit** = Compliance + Technical Debt + Risk Assessment

---

## Notes

- All prompts assume architecture files follow naming convention: `[service-name].arch.md`
- Commits should have meaningful commit messages for better analysis
- Date-based analysis requires commit dates to be accurate
- Cross-service analysis requires multiple architecture files to exist
- Some reports may require additional context beyond git history

