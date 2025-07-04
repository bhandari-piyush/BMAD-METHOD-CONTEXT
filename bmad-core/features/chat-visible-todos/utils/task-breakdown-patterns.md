# Task Breakdown Patterns

## Purpose

Library of proven task breakdown patterns for different categories of work, enabling consistent and efficient micro-chunk generation across all agents.

## Core Pattern Categories

### 1. Development Task Patterns

#### Basic Feature Implementation
**Pattern**: Setup → Core → Testing → Integration → Documentation
**Typical Duration**: 30-45 minutes
**Chunk Breakdown**:
```
1. Environment setup and file structure (5 min)
2. Implement core functionality (12 min)
3. Add error handling and validation (6 min)
4. Write unit tests (8 min)
5. Integration testing (5 min)
6. Update documentation (3 min)
```

#### Bug Fix Pattern
**Pattern**: Investigate → Fix → Test → Verify
**Typical Duration**: 20-30 minutes
**Chunk Breakdown**:
```
1. Reproduce and analyze bug (8 min)
2. Identify root cause (5 min)
3. Implement fix (7 min)
4. Test fix thoroughly (5 min)
5. Verify no regression (3 min)
```

#### API Development Pattern
**Pattern**: Design → Implement → Test → Document
**Typical Duration**: 35-50 minutes
**Chunk Breakdown**:
```
1. Define API specification (6 min)
2. Create endpoint handlers (12 min)
3. Add input validation (5 min)
4. Implement business logic (10 min)
5. Write API tests (8 min)
6. Update API documentation (4 min)
```

#### Database Schema Pattern
**Pattern**: Design → Create → Populate → Test
**Typical Duration**: 25-35 minutes
**Chunk Breakdown**:
```
1. Design schema structure (7 min)
2. Create migration files (6 min)
3. Add indexes and constraints (5 min)
4. Create seed data (4 min)
5. Test migrations (3 min)
```

### 2. Documentation Task Patterns

#### PRD Creation Pattern
**Pattern**: Research → Structure → Content → Review → Finalize
**Typical Duration**: 60-90 minutes
**Chunk Breakdown**:
```
1. Market research and analysis (15 min)
2. Competitor analysis (10 min)
3. Define user personas (8 min)
4. Create feature structure (5 min)
5. Write requirements (20 min)
6. Define acceptance criteria (10 min)
7. Review and refine (8 min)
8. Format and finalize (4 min)
```

#### Story Creation Pattern
**Pattern**: Analyze → Extract → Structure → Validate
**Typical Duration**: 20-30 minutes
**Chunk Breakdown**:
```
1. Load configuration and context (2 min)
2. Identify story position (3 min)
3. Analyze epic requirements (5 min)
4. Extract technical context (6 min)
5. Generate story content (10 min)
6. Validate and save (2 min)
```

#### Architecture Documentation Pattern
**Pattern**: Analyze → Design → Document → Review
**Typical Duration**: 45-60 minutes
**Chunk Breakdown**:
```
1. Analyze current architecture (10 min)
2. Identify design patterns (8 min)
3. Document system components (12 min)
4. Create diagrams (10 min)
5. Document interfaces (8 min)
6. Review for completeness (5 min)
```

#### Technical Specification Pattern
**Pattern**: Requirements → Design → Details → Review
**Typical Duration**: 40-55 minutes
**Chunk Breakdown**:
```
1. Gather technical requirements (8 min)
2. Design system architecture (12 min)
3. Specify implementation details (15 min)
4. Add testing requirements (6 min)
5. Review and validate (5 min)
```

### 3. Analysis Task Patterns

#### Data Analysis Pattern
**Pattern**: Collect → Clean → Analyze → Report
**Typical Duration**: 35-50 minutes
**Chunk Breakdown**:
```
1. Gather data sources (8 min)
2. Clean and normalize data (10 min)
3. Perform statistical analysis (12 min)
4. Identify patterns and insights (8 min)
5. Generate analysis report (7 min)
```

#### Code Review Pattern
**Pattern**: Understand → Analyze → Feedback → Summary
**Typical Duration**: 25-35 minutes
**Chunk Breakdown**:
```
1. Understand changes and context (8 min)
2. Analyze code quality (10 min)
3. Check for security issues (5 min)
4. Verify tests and coverage (4 min)
5. Generate feedback report (5 min)
```

#### Performance Analysis Pattern
**Pattern**: Baseline → Test → Analyze → Recommend
**Typical Duration**: 40-55 minutes
**Chunk Breakdown**:
```
1. Establish performance baseline (8 min)
2. Run performance tests (12 min)
3. Analyze bottlenecks (10 min)
4. Identify optimization opportunities (8 min)
5. Create recommendations (7 min)
```

### 4. Project Management Patterns

#### Sprint Planning Pattern
**Pattern**: Review → Estimate → Prioritize → Plan
**Typical Duration**: 45-60 minutes
**Chunk Breakdown**:
```
1. Review backlog items (10 min)
2. Estimate story points (15 min)
3. Prioritize based on value (8 min)
4. Create sprint plan (10 min)
5. Validate capacity (5 min)
```

#### Epic Creation Pattern
**Pattern**: Define → Structure → Stories → Validate
**Typical Duration**: 50-70 minutes
**Chunk Breakdown**:
```
1. Define epic scope and goals (10 min)
2. Identify key features (8 min)
3. Break down into stories (15 min)
4. Define acceptance criteria (12 min)
5. Estimate effort (6 min)
6. Validate completeness (5 min)
```

#### Risk Assessment Pattern
**Pattern**: Identify → Analyze → Mitigate → Monitor
**Typical Duration**: 35-45 minutes
**Chunk Breakdown**:
```
1. Identify potential risks (10 min)
2. Analyze impact and probability (8 min)
3. Develop mitigation strategies (12 min)
4. Create monitoring plan (6 min)
```

### 5. Quality Assurance Patterns

#### Test Plan Creation Pattern
**Pattern**: Analyze → Design → Document → Review
**Typical Duration**: 40-55 minutes
**Chunk Breakdown**:
```
1. Analyze requirements (8 min)
2. Design test scenarios (12 min)
3. Create test cases (15 min)
4. Document test data needs (6 min)
5. Review test coverage (5 min)
```

#### Bug Verification Pattern
**Pattern**: Reproduce → Validate → Test → Report
**Typical Duration**: 20-30 minutes
**Chunk Breakdown**:
```
1. Reproduce reported issue (8 min)
2. Validate fix implementation (5 min)
3. Test fix thoroughly (7 min)
4. Verify no regression (4 min)
5. Update bug report (3 min)
```

#### Automated Testing Pattern
**Pattern**: Plan → Implement → Execute → Maintain
**Typical Duration**: 45-60 minutes
**Chunk Breakdown**:
```
1. Plan test automation strategy (8 min)
2. Set up test framework (10 min)
3. Implement test scripts (20 min)
4. Execute and validate (8 min)
5. Document maintenance (4 min)
```

## Pattern Selection Logic

### Task Type Identification

**Keywords to Pattern Mapping**:
```
Development Keywords:
- "implement", "build", "create", "develop" → Feature Implementation
- "fix", "bug", "issue", "error" → Bug Fix
- "api", "endpoint", "service" → API Development
- "database", "schema", "migration" → Database Schema

Documentation Keywords:
- "prd", "requirements", "product" → PRD Creation
- "story", "user story", "epic" → Story Creation
- "architecture", "design", "system" → Architecture Documentation
- "spec", "specification", "technical" → Technical Specification

Analysis Keywords:
- "analyze", "data", "metrics", "report" → Data Analysis
- "review", "code", "quality" → Code Review
- "performance", "benchmark", "optimize" → Performance Analysis

Management Keywords:
- "plan", "sprint", "roadmap" → Sprint Planning
- "epic", "feature", "milestone" → Epic Creation
- "risk", "assessment", "mitigation" → Risk Assessment

Quality Keywords:
- "test", "qa", "quality" → Test Plan Creation
- "bug", "verify", "validate" → Bug Verification
- "automation", "ci/cd", "testing" → Automated Testing
```

### Pattern Adaptation Rules

**Complexity Adjustments**:
```
LOW Complexity (1-2):
- Reduce chunk count by 20-30%
- Simplify validation steps
- Combine related micro-chunks

MEDIUM Complexity (3-5):
- Use standard pattern as-is
- Add optional verification steps
- Include error handling

HIGH Complexity (6-8):
- Increase chunk count by 30-40%
- Add additional validation
- Include integration testing
- Add documentation updates

VERY HIGH Complexity (9-10):
- Break into sub-patterns
- Add research and analysis phases
- Include stakeholder reviews
- Add comprehensive testing
```

**Agent-Specific Adaptations**:
```
Dev Agent:
- Emphasize testing and code quality
- Add build and deployment steps
- Include performance considerations

PM Agent:
- Add stakeholder communication
- Include market research
- Emphasize user value

SM Agent:
- Focus on story structure
- Add epic analysis
- Include validation steps

Analyst Agent:
- Add data validation
- Include statistical analysis
- Emphasize insights generation

QA Agent:
- Add comprehensive testing
- Include regression testing
- Focus on quality metrics
```

## Pattern Customization

### Custom Pattern Creation

**Steps to Create New Pattern**:
1. **Identify Pattern Category**: Development, Documentation, Analysis, etc.
2. **Define Core Phases**: High-level workflow stages
3. **Break Down Micro-Chunks**: 5-15 minute executable pieces
4. **Estimate Timing**: Based on historical data
5. **Define Dependencies**: Sequence and relationships
6. **Test Pattern**: Validate with real tasks
7. **Refine Based on Results**: Improve accuracy

**Pattern Template**:
```
### {Pattern Name}
**Pattern**: {Phase 1} → {Phase 2} → {Phase 3} → {Phase 4}
**Typical Duration**: {X}-{Y} minutes
**Chunk Breakdown**:
1. {Description} ({time} min)
2. {Description} ({time} min)
3. {Description} ({time} min)
4. {Description} ({time} min)
5. {Description} ({time} min)

**Complexity Adjustments**:
- LOW: {adjustments}
- MEDIUM: {adjustments}
- HIGH: {adjustments}

**Agent Adaptations**:
- {Agent}: {specific modifications}
```

### Pattern Optimization

**Performance Metrics**:
- **Accuracy**: How close estimates are to actual time
- **Completeness**: Whether all necessary steps are included
- **Efficiency**: Optimal ordering and chunking
- **Flexibility**: Adaptability to different contexts

**Improvement Process**:
1. **Collect Usage Data**: Track actual vs. estimated times
2. **Identify Patterns**: Common deviations and issues
3. **Analyze Root Causes**: Why estimates are off
4. **Adjust Patterns**: Modify timing and steps
5. **Test Improvements**: Validate changes
6. **Update Documentation**: Keep patterns current

## Integration with Micro-Chunk Analyzer

### Pattern Selection API

**Function**: `selectOptimalPattern(taskDescription, agentType, complexity)`
**Returns**: Best matching pattern with confidence score

**Selection Algorithm**:
```
1. Extract keywords from task description
2. Match keywords to pattern categories
3. Consider agent type and specialization
4. Adjust for complexity level
5. Return highest confidence pattern
6. Provide fallback options
```

### Pattern Application

**Function**: `applyPattern(selectedPattern, taskContext)`
**Returns**: Customized chunk breakdown

**Application Process**:
```
1. Load base pattern structure
2. Apply complexity adjustments
3. Customize for agent type
4. Adjust for task context
5. Validate chunk sizing
6. Return optimized breakdown
```

## Quality Assurance

### Pattern Validation

**Validation Criteria**:
- **Chunk Size**: All chunks between 5-15 minutes
- **Dependencies**: Logical sequence maintained
- **Completeness**: All necessary steps included
- **Clarity**: Clear, actionable descriptions

**Validation Process**:
```
1. Check chunk timing boundaries
2. Verify logical dependencies
3. Validate against task requirements
4. Test with sample tasks
5. Collect feedback from agents
6. Refine based on results
```

### Pattern Testing

**Testing Strategy**:
- **Unit Tests**: Individual pattern components
- **Integration Tests**: Pattern application with real tasks
- **Performance Tests**: Timing accuracy validation
- **User Acceptance Tests**: Agent and user satisfaction

**Success Metrics**:
- 90% of chunks complete within estimated time ±20%
- 95% of patterns selected are appropriate for task
- 100% of generated chunks are actionable
- User satisfaction score > 4.0/5.0

## Maintenance and Evolution

### Pattern Updates

**Update Triggers**:
- New task types identified
- Agent feedback on pattern effectiveness
- Performance data showing inaccuracies
- Technology or process changes

**Update Process**:
1. **Analyze Feedback**: Review agent and user input
2. **Identify Improvements**: Specific changes needed
3. **Update Patterns**: Modify timing, steps, or structure
4. **Test Changes**: Validate improvements
5. **Deploy Updates**: Push to production
6. **Monitor Results**: Track improvement effectiveness

### Pattern Expansion

**Growth Strategy**:
- **Domain-Specific Patterns**: Add specialized patterns for new domains
- **Agent-Specific Patterns**: Create agent-optimized variations
- **Project-Specific Patterns**: Customize for specific project types
- **Technology-Specific Patterns**: Adapt for new technologies

**Expansion Process**:
1. **Identify Needs**: Gaps in current pattern coverage
2. **Research Requirements**: Understand new domain needs
3. **Develop Patterns**: Create and test new patterns
4. **Validate Effectiveness**: Ensure patterns work well
5. **Document Patterns**: Add to pattern library
6. **Train Agents**: Update agent capabilities 