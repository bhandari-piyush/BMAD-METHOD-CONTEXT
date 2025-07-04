# Micro-Chunk Analyzer Utility

## Purpose

Core engine for analyzing task complexity and breaking down tasks into optimal micro-chunks for agent execution efficiency.

## Core Functions

### 1. Task Complexity Analysis

**Function**: `analyzeTaskComplexity(taskDescription, agentType)`

**Purpose**: Assess task difficulty and determine optimal breakdown strategy

**Complexity Indicators**:
- **Keywords**: "implement", "create", "build", "integrate", "test"
- **Scope**: File count, feature count, integration points
- **Dependencies**: External systems, other tasks, user input
- **Technology**: Complexity of tech stack, new vs. familiar tools

**Complexity Scoring**:
```
LOW (1-2): Simple tasks, single file, no dependencies
MEDIUM (3-5): Multiple files, some integration, standard patterns
HIGH (6-8): Complex logic, multiple systems, custom implementation
VERY HIGH (9-10): Architecture changes, multiple agents, research required
```

**Implementation Logic**:
```
1. Parse task description for complexity keywords
2. Identify technical requirements and constraints
3. Assess agent-specific factors (Dev vs PM vs SM)
4. Calculate base complexity score
5. Adjust for agent experience and context
6. Return complexity level and breakdown strategy
```

### 2. Micro-Chunk Generation

**Function**: `generateMicroChunks(task, complexity, agentType)`

**Purpose**: Create optimized breakdown of task into executable micro-chunks

**Chunk Generation Rules**:
- **Size Target**: 5-15 minutes per chunk
- **Dependency Order**: Logical sequence based on requirements
- **Agent Specialization**: Tailored to agent capabilities
- **Clear Boundaries**: Distinct start/end points for each chunk

**Chunk Generation Patterns**:

#### Development Tasks
```
Pattern: Setup → Implementation → Testing → Integration
1. Environment setup (5 min)
2. Core implementation (10 min)
3. Unit testing (8 min)
4. Integration testing (7 min)
5. Documentation (5 min)
```

#### Documentation Tasks
```
Pattern: Research → Draft → Review → Finalize
1. Gather requirements (8 min)
2. Research and outline (10 min)
3. Draft content (15 min)
4. Review and refine (7 min)
5. Format and save (3 min)
```

#### Analysis Tasks
```
Pattern: Collect → Process → Analyze → Report
1. Data collection (10 min)
2. Data cleaning (8 min)
3. Analysis execution (12 min)
4. Results interpretation (8 min)
5. Report generation (7 min)
```

**Implementation Algorithm**:
```
1. Select appropriate pattern based on task type
2. Identify specific requirements and constraints
3. Generate base chunk sequence
4. Adjust chunk sizes based on complexity
5. Optimize for agent-specific efficiency
6. Validate total time estimate
7. Return ordered chunk list
```

### 3. Time Estimation

**Function**: `estimateTimeRequirement(chunk, agentType, context)`

**Purpose**: Predict realistic completion time for each micro-chunk

**Estimation Factors**:
- **Chunk Type**: Setup, implementation, testing, documentation
- **Agent Experience**: Historical performance data
- **Context Complexity**: Project size, technology familiarity
- **External Dependencies**: File system, network, user input

**Base Time Estimates**:
```
File Operations:
- Create new file: 2-3 minutes
- Modify existing file: 3-5 minutes
- Complex file changes: 5-10 minutes

Code Implementation:
- Simple function: 5-8 minutes
- Complex logic: 10-15 minutes
- Integration code: 8-12 minutes

Testing:
- Unit tests: 5-10 minutes
- Integration tests: 8-15 minutes
- E2E tests: 10-20 minutes

Documentation:
- Simple docs: 3-5 minutes
- Detailed docs: 8-15 minutes
- Complex specs: 15-25 minutes
```

**Estimation Algorithm**:
```
1. Identify chunk type and category
2. Look up base time estimate
3. Apply complexity multiplier
4. Adjust for agent-specific factors
5. Consider context and dependencies
6. Apply historical accuracy corrections
7. Return time estimate with confidence level
```

### 4. Dependency Analysis

**Function**: `identifyDependencies(chunks, context)`

**Purpose**: Map relationships between micro-chunks and optimize execution order

**Dependency Types**:
- **Sequential**: Chunk B requires Chunk A output
- **Parallel**: Chunks can execute simultaneously
- **Conditional**: Chunk execution depends on results
- **Optional**: Chunk can be skipped if needed

**Dependency Mapping**:
```
1. Analyze each chunk's inputs and outputs
2. Identify data flow between chunks
3. Map external dependencies (files, systems)
4. Determine optimal execution sequence
5. Identify parallelization opportunities
6. Flag potential bottlenecks
```

## Agent-Specific Customization

### Dev Agent Optimization

**Specialization Focus**:
- Code structure and patterns
- Testing requirements
- File system operations
- Build and deployment steps

**Custom Patterns**:
```
Feature Implementation:
1. Set up development environment (3 min)
2. Create base files and structure (5 min)
3. Implement core logic (12 min)
4. Add error handling (5 min)
5. Write unit tests (8 min)
6. Integration testing (7 min)
7. Update documentation (3 min)
```

### SM Agent Optimization

**Specialization Focus**:
- Story structure and requirements
- Template processing
- Epic analysis
- Validation steps

**Custom Patterns**:
```
Story Creation:
1. Load configuration and context (2 min)
2. Identify story position (3 min)
3. Analyze epic requirements (5 min)
4. Extract technical context (6 min)
5. Generate story content (10 min)
6. Validate and save (2 min)
```

### PM Agent Optimization

**Specialization Focus**:
- Research and analysis
- Strategic thinking
- Stakeholder considerations
- Documentation quality

**Custom Patterns**:
```
PRD Creation:
1. Market research (15 min)
2. Competitor analysis (10 min)
3. User persona definition (8 min)
4. Feature prioritization (12 min)
5. Requirements documentation (15 min)
6. Review and refinement (8 min)
```

## Pattern Learning and Adaptation

### Historical Performance Tracking

**Data Collection**:
- Actual vs. estimated time for each chunk
- Agent performance patterns
- Task complexity accuracy
- User satisfaction metrics

**Pattern Refinement**:
- Adjust base time estimates based on actual performance
- Improve complexity scoring accuracy
- Refine agent-specific patterns
- Update dependency mapping logic

### Continuous Improvement

**Feedback Loop**:
```
1. Execute task with micro-chunks
2. Collect actual performance data
3. Compare against estimates
4. Identify patterns and deviations
5. Update algorithms and patterns
6. Improve future task breakdowns
```

## Integration with Chat Progress Display

### Data Flow

**Analysis to Display**:
1. Task analysis generates chunk breakdown
2. Chunk data passed to progress display system
3. Real-time updates flow back to display
4. Completion data updates historical patterns

**Information Exchange**:
- Chunk descriptions and estimates
- Status updates and progress
- File changes and accomplishments
- Error conditions and recovery

## Error Handling and Recovery

### Analysis Failures

**Fallback Strategies**:
- Use generic patterns if analysis fails
- Provide manual breakdown options
- Escalate to user for guidance
- Log issues for pattern improvement

### Execution Monitoring

**Chunk Execution Issues**:
- Detect chunks taking significantly longer
- Offer skip or retry options
- Adjust remaining time estimates
- Learn from execution patterns

## Performance Optimization

### Efficient Analysis

**Fast Processing**:
- Cache common patterns
- Optimize pattern matching
- Minimize computation overhead
- Parallel processing where possible

### Memory Management

**Resource Efficiency**:
- Limit concurrent analysis
- Clean up completed chunk data
- Optimize pattern storage
- Monitor memory usage

## Configuration and Customization

### Adjustable Parameters

**Chunk Sizing**:
- Minimum chunk time (default: 5 minutes)
- Maximum chunk time (default: 15 minutes)
- Complexity adjustment factors
- Agent-specific modifiers

**Pattern Customization**:
- Add custom task patterns
- Modify existing patterns
- Adjust time estimates
- Configure dependency rules

### User Preferences

**Breakdown Style**:
- Granular: More, smaller chunks
- Standard: Balanced chunk size
- Coarse: Fewer, larger chunks

**Agent Optimization**:
- Conservative: Longer time estimates
- Aggressive: Shorter time estimates
- Adaptive: Learn from performance 