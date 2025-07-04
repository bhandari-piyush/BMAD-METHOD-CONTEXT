# Universal Agent Pattern for Micro-Chunk Integration

## Purpose

Standard pattern that all BMAD agents must implement to support chat-visible TODO micro-chunking functionality. This ensures consistent user experience and efficient task execution across all agents.

## Core Integration Requirements

### 1. Pre-Task Analysis Phase

**Function**: `analyzeTasks(taskDescription, agentContext)`
**Purpose**: Analyze incoming task and prepare micro-chunk breakdown

**Implementation Steps**:
```
1. Load task complexity analyzer
2. Identify task type and category
3. Select appropriate breakdown pattern
4. Generate micro-chunk sequence
5. Estimate timing for each chunk
6. Validate chunk structure
7. Prepare progress display
```

**Code Integration Point**:
```yaml
# In agent startup section, add:
startup:
  - Load micro-chunk analyzer utility
  - Initialize progress display system
  - Configure agent-specific patterns
```

### 2. Task Initiation Display

**Function**: `displayTaskBreakdown(task, chunks)`
**Purpose**: Show user the micro-chunk breakdown before execution

**Display Implementation**:
```
1. Show task header with metadata
2. Display "Breaking down task..." message
3. Present micro-chunk list with estimates
4. Show total estimated duration
5. Initialize progress tracking
6. Display "Starting execution..." message
```

**Chat Output Format**:
```
🎯 **Task**: {task_name}
📅 **Estimated Duration**: {total_time}
🤖 **Agent**: {agent_name}

**Breaking down task into micro-chunks...**

📋 **Micro-Chunks Identified**:
⏳ 1. {chunk1_description} ({estimate})
⏳ 2. {chunk2_description} ({estimate})
⏳ 3. {chunk3_description} ({estimate})
⏳ 4. {chunk4_description} ({estimate})
⏳ 5. {chunk5_description} ({estimate})

**Starting execution...**
```

### 3. Real-Time Progress Updates

**Function**: `updateProgress(chunkId, status, details)`
**Purpose**: Update chat display as chunks complete

**Update Triggers**:
- Chunk status change (pending → in progress → complete)
- Significant progress within chunk
- File modifications detected
- Error conditions encountered

**Progress Display Format**:
```
📊 **Progress Update**:
✅ 1. {description} ({estimate}) - **COMPLETE**
   └── 📄 {accomplishment}
   └── 📁 {file_changes}
🟡 2. {description} ({estimate}) - **IN PROGRESS**
   └── 🔄 {current_activity}
⏳ 3. {description} ({estimate})
⏳ 4. {description} ({estimate})
⏳ 5. {description} ({estimate})
```

### 4. Completion Celebration

**Function**: `celebrateCompletion(taskSummary)`
**Purpose**: Provide satisfying completion display

**Completion Format**:
```
🎉 **{X} of {Y} Done** - View All Details

**✅ {TASK_NAME} COMPLETED SUCCESSFULLY!**

📊 **Summary**:
   └── 📄 {primary_accomplishment}
   └── 📁 {total_file_changes} +{total_added} -{total_removed}
   └── ⏱️ {actual_time} (estimated: {estimated_time})
   └── 🎯 {key_outcomes}

**🎊 Excellent work! Task completed efficiently.**
```

## Agent-Specific Implementation

### Development Agent (dev.md)

**Enhanced Task Execution**:
```yaml
task-execution:
  flow: "Analyze task → Generate chunks → Display breakdown → Execute sequentially → Update progress → Celebrate completion"
  micro-chunking:
    patterns:
      - feature-implementation
      - bug-fix
      - testing-workflow
      - code-review
    focus:
      - File change tracking
      - Code quality metrics
      - Test coverage
      - Build/deployment steps
```

**Example Enhancement**:
```yaml
# Add to dev.md dependencies:
dependencies:
  utils:
    - micro-chunk-analyzer
    - chat-progress-display
    - task-breakdown-patterns
```

### Scrum Master Agent (sm.md)

**Enhanced Story Creation**:
```yaml
story-creation:
  flow: "Analyze epic → Generate chunks → Display breakdown → Execute sequentially → Update progress → Celebrate completion"
  micro-chunking:
    patterns:
      - story-creation
      - epic-analysis
      - template-processing
      - validation-workflow
    focus:
      - Epic analysis breakdown
      - Story structure validation
      - Template processing steps
      - Configuration loading
```

### Product Manager Agent (pm.md)

**Enhanced Document Creation**:
```yaml
document-creation:
  flow: "Analyze requirements → Generate chunks → Display breakdown → Execute sequentially → Update progress → Celebrate completion"
  micro-chunking:
    patterns:
      - prd-creation
      - market-research
      - competitive-analysis
      - feature-definition
    focus:
      - Research phases
      - Analysis steps
      - Documentation generation
      - Review cycles
```

## Implementation Template

### 1. Agent Configuration Enhancement

**Add to Agent YAML**:
```yaml
# Add to existing agent configuration
micro-chunking:
  enabled: true
  patterns:
    - {agent-specific-pattern-1}
    - {agent-specific-pattern-2}
    - {agent-specific-pattern-3}
  preferences:
    chunk-size: standard  # granular, standard, coarse
    time-estimation: adaptive  # conservative, standard, aggressive
    display-style: standard  # minimal, standard, detailed
```

### 2. Utility Dependencies

**Add to Agent Dependencies**:
```yaml
dependencies:
  utils:
    - micro-chunk-analyzer
    - chat-progress-display
    - task-breakdown-patterns
```

### 3. Task Execution Enhancement

**Modified Task Flow**:
```yaml
task-execution:
  flow: |
    1. Receive task request
    2. Analyze task with micro-chunk analyzer
    3. Generate chunk breakdown
    4. Display breakdown to user
    5. Execute chunks sequentially
    6. Update progress in real-time
    7. Celebrate completion
    8. Continue with next task
```

### 4. Progress Callback Integration

**Add Progress Callbacks**:
```yaml
progress-callbacks:
  onTaskStart: "Initialize progress display"
  onChunkStart: "Update chunk to IN PROGRESS"
  onChunkProgress: "Show current activity"
  onChunkComplete: "Mark chunk COMPLETE, show accomplishment"
  onChunkFailed: "Mark chunk FAILED, show error options"
  onTaskComplete: "Show completion celebration"
```

## Standard Implementation Functions

### 1. Task Analysis Function

**Function Signature**: `analyzeAndBreakdownTask(taskDescription, agentType)`

**Implementation**:
```javascript
function analyzeAndBreakdownTask(taskDescription, agentType) {
    // 1. Load micro-chunk analyzer
    const analyzer = loadMicroChunkAnalyzer();
    
    // 2. Analyze task complexity
    const complexity = analyzer.analyzeComplexity(taskDescription, agentType);
    
    // 3. Select appropriate pattern
    const pattern = analyzer.selectPattern(taskDescription, agentType, complexity);
    
    // 4. Generate micro-chunks
    const chunks = analyzer.generateChunks(taskDescription, pattern, complexity);
    
    // 5. Estimate timing
    const estimatedChunks = chunks.map(chunk => ({
        ...chunk,
        estimate: analyzer.estimateTime(chunk, agentType)
    }));
    
    // 6. Return breakdown
    return {
        task: taskDescription,
        complexity: complexity,
        pattern: pattern,
        chunks: estimatedChunks,
        totalEstimate: estimatedChunks.reduce((sum, chunk) => sum + chunk.estimate, 0)
    };
}
```

### 2. Progress Display Function

**Function Signature**: `displayProgressBreakdown(breakdown)`

**Implementation**:
```javascript
function displayProgressBreakdown(breakdown) {
    // 1. Load progress display system
    const display = loadProgressDisplay();
    
    // 2. Show task initiation
    display.showTaskInitiation(breakdown.task, breakdown.totalEstimate);
    
    // 3. Display chunk breakdown
    display.showChunkBreakdown(breakdown.chunks);
    
    // 4. Initialize progress tracking
    display.initializeProgressTracking(breakdown.chunks);
    
    // 5. Show execution start
    display.showExecutionStart();
}
```

### 3. Chunk Execution Function

**Function Signature**: `executeChunksSequentially(chunks, executionContext)`

**Implementation**:
```javascript
async function executeChunksSequentially(chunks, executionContext) {
    const display = loadProgressDisplay();
    const results = [];
    
    for (let i = 0; i < chunks.length; i++) {
        const chunk = chunks[i];
        
        try {
            // 1. Update chunk to IN PROGRESS
            display.updateChunkStatus(chunk.id, 'IN_PROGRESS');
            
            // 2. Execute chunk
            const result = await executeChunk(chunk, executionContext);
            
            // 3. Update chunk to COMPLETE
            display.updateChunkStatus(chunk.id, 'COMPLETE', result);
            
            // 4. Track file changes
            if (result.fileChanges) {
                display.trackFileChanges(result.fileChanges);
            }
            
            results.push(result);
            
        } catch (error) {
            // Handle chunk failure
            display.updateChunkStatus(chunk.id, 'FAILED', error);
            
            // Offer recovery options
            const recovery = await handleChunkFailure(chunk, error);
            if (recovery.retry) {
                i--; // Retry this chunk
                continue;
            } else if (recovery.skip) {
                continue; // Skip this chunk
            } else {
                throw error; // Abort task
            }
        }
    }
    
    // Show completion celebration
    display.celebrateCompletion(results);
    
    return results;
}
```

### 4. Completion Celebration Function

**Function Signature**: `celebrateTaskCompletion(taskName, results)`

**Implementation**:
```javascript
function celebrateTaskCompletion(taskName, results) {
    const display = loadProgressDisplay();
    
    // 1. Calculate summary metrics
    const summary = {
        taskName: taskName,
        totalChunks: results.length,
        completedChunks: results.filter(r => r.status === 'complete').length,
        totalFileChanges: results.reduce((sum, r) => sum + (r.fileChanges?.length || 0), 0),
        totalLinesAdded: results.reduce((sum, r) => sum + (r.linesAdded || 0), 0),
        totalLinesRemoved: results.reduce((sum, r) => sum + (r.linesRemoved || 0), 0),
        actualTime: results.reduce((sum, r) => sum + (r.actualTime || 0), 0),
        estimatedTime: results.reduce((sum, r) => sum + (r.estimatedTime || 0), 0),
        keyOutcomes: results.map(r => r.accomplishment).filter(Boolean)
    };
    
    // 2. Show completion celebration
    display.showCompletionCelebration(summary);
    
    // 3. Log performance data
    logPerformanceMetrics(summary);
    
    return summary;
}
```

## Error Handling and Recovery

### Chunk Failure Handling

**Function**: `handleChunkFailure(chunk, error)`

**Recovery Options**:
- **Retry**: Attempt the chunk again
- **Skip**: Mark as skipped and continue
- **Manual**: Pause for user intervention
- **Abort**: Stop task execution

**Implementation**:
```javascript
async function handleChunkFailure(chunk, error) {
    const display = loadProgressDisplay();
    
    // 1. Display error state
    display.showChunkError(chunk, error);
    
    // 2. Analyze error type
    const errorType = analyzeError(error);
    
    // 3. Provide recovery options
    const options = determineRecoveryOptions(errorType);
    
    // 4. Get user input (if needed)
    if (options.requiresUserInput) {
        const userChoice = await getUserRecoveryChoice(options);
        return userChoice;
    }
    
    // 5. Auto-recovery for known issues
    if (options.autoRecovery) {
        return { retry: true, attempts: 1 };
    }
    
    // 6. Default to skip for non-critical chunks
    return { skip: true };
}
```

### Warning State Handling

**Function**: `handleSlowProgress(chunk, actualTime, estimatedTime)`

**Implementation**:
```javascript
function handleSlowProgress(chunk, actualTime, estimatedTime) {
    const display = loadProgressDisplay();
    
    // 1. Check if significantly over estimate
    if (actualTime > estimatedTime * 1.5) {
        // 2. Show warning to user
        display.showSlowProgressWarning(chunk, actualTime, estimatedTime);
        
        // 3. Update remaining estimates
        updateRemainingEstimates(chunk, actualTime);
        
        // 4. Log performance data
        logPerformanceDeviation(chunk, actualTime, estimatedTime);
    }
}
```

## Performance Monitoring

### Metrics Collection

**Function**: `collectPerformanceMetrics(task, chunks, results)`

**Metrics to Track**:
- Chunk completion times vs. estimates
- Overall task completion time
- Error rates and recovery success
- User engagement with progress display
- File change tracking accuracy

**Implementation**:
```javascript
function collectPerformanceMetrics(task, chunks, results) {
    const metrics = {
        taskId: generateTaskId(task),
        agentType: getCurrentAgentType(),
        totalChunks: chunks.length,
        completedChunks: results.filter(r => r.status === 'complete').length,
        failedChunks: results.filter(r => r.status === 'failed').length,
        totalEstimatedTime: chunks.reduce((sum, c) => sum + c.estimate, 0),
        totalActualTime: results.reduce((sum, r) => sum + r.actualTime, 0),
        accuracyScore: calculateAccuracyScore(chunks, results),
        timestamp: Date.now()
    };
    
    // Store metrics for analysis
    storeMetrics(metrics);
    
    return metrics;
}
```

## Integration Testing

### Test Requirements

**Test Categories**:
1. **Unit Tests**: Individual function testing
2. **Integration Tests**: Agent enhancement testing
3. **End-to-End Tests**: Complete task execution
4. **Performance Tests**: Timing and resource usage

**Test Implementation**:
```javascript
// Example test for Dev Agent enhancement
describe('Dev Agent Micro-Chunking', () => {
    test('should break down feature implementation task', async () => {
        const task = 'Implement user authentication';
        const breakdown = await analyzeAndBreakdownTask(task, 'dev');
        
        expect(breakdown.chunks.length).toBeGreaterThan(3);
        expect(breakdown.chunks.length).toBeLessThan(8);
        expect(breakdown.totalEstimate).toBeGreaterThan(20);
        expect(breakdown.totalEstimate).toBeLessThan(60);
    });
    
    test('should update progress in real-time', async () => {
        const mockDisplay = mockProgressDisplay();
        const chunks = generateTestChunks();
        
        await executeChunksSequentially(chunks, {});
        
        expect(mockDisplay.updateChunkStatus).toHaveBeenCalledTimes(chunks.length * 2);
        expect(mockDisplay.celebrateCompletion).toHaveBeenCalledTimes(1);
    });
});
```

## Deployment and Rollout

### Rollout Strategy

**Phase 1**: Core Agent Enhancement
- Enhance Dev Agent first (highest complexity)
- Test with real development tasks
- Gather feedback and refine

**Phase 2**: Secondary Agent Enhancement
- Enhance SM and PM agents
- Test with documentation tasks
- Validate pattern effectiveness

**Phase 3**: Complete Integration
- Enhance remaining agents
- Full system testing
- Performance optimization

### Deployment Checklist

**Pre-Deployment**:
- [ ] All utility functions implemented
- [ ] Agent configurations updated
- [ ] Progress display system tested
- [ ] Error handling validated
- [ ] Performance benchmarks met

**During Deployment**:
- [ ] Gradual rollout to agents
- [ ] Monitor performance metrics
- [ ] Collect user feedback
- [ ] Address any issues quickly

**Post-Deployment**:
- [ ] Performance analysis
- [ ] User satisfaction survey
- [ ] Pattern optimization
- [ ] Documentation updates 