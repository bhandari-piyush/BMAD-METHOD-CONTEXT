# Micro-Chunk Analyzer Utility

## Purpose

Core utility for analyzing task complexity and breaking down tasks into optimal micro-chunks for efficient agent execution.

## Usage Instructions

[[LLM: This utility provides functions that agents can call to analyze and break down their tasks]]

### Basic Usage

```javascript
// Load the utility
const analyzer = require('./micro-chunk-analyzer');

// Analyze a task
const task = "Implement user authentication system";
const breakdown = await analyzer.analyzeAndBreakdown(task, 'dev');

// Use the breakdown
console.log(breakdown.chunks);
console.log(breakdown.totalEstimate);
```

## Core Functions

### 1. analyzeAndBreakdown(taskDescription, agentType, options = {})

**Purpose**: Main function that analyzes task and returns complete breakdown

**Parameters**:
- `taskDescription` (string): The task to analyze
- `agentType` (string): Agent type ('dev', 'pm', 'sm', 'analyst', etc.)
- `options` (object): Optional configuration

**Returns**: Breakdown object with chunks, estimates, and metadata

**Implementation**:
```javascript
async function analyzeAndBreakdown(taskDescription, agentType, options = {}) {
    // Step 1: Analyze task complexity
    const complexity = analyzeComplexity(taskDescription, agentType);
    
    // Step 2: Select appropriate pattern
    const pattern = selectBestPattern(taskDescription, agentType, complexity);
    
    // Step 3: Generate micro-chunks
    const chunks = generateChunks(taskDescription, pattern, complexity, agentType);
    
    // Step 4: Estimate timing
    const estimatedChunks = estimateTiming(chunks, agentType, complexity);
    
    // Step 5: Validate and optimize
    const optimizedChunks = validateAndOptimize(estimatedChunks);
    
    return {
        task: taskDescription,
        agentType: agentType,
        complexity: complexity,
        pattern: pattern.id,
        chunks: optimizedChunks,
        totalEstimate: optimizedChunks.reduce((sum, chunk) => sum + chunk.estimate, 0),
        metadata: {
            analysisTime: Date.now(),
            confidence: pattern.confidence,
            recommendations: generateRecommendations(optimizedChunks)
        }
    };
}
```

### 2. analyzeComplexity(taskDescription, agentType)

**Purpose**: Analyze task complexity and return complexity score

**Implementation**:
```javascript
function analyzeComplexity(taskDescription, agentType) {
    const keywords = extractKeywords(taskDescription.toLowerCase());
    let score = 1; // Base score
    
    // Complexity indicators
    const complexityKeywords = {
        high: ['architecture', 'system', 'integration', 'complete', 'comprehensive', 'multiple', 'complex'],
        medium: ['implement', 'create', 'build', 'feature', 'api', 'database'],
        low: ['update', 'fix', 'modify', 'simple', 'basic']
    };
    
    // Check for high complexity indicators
    if (keywords.some(k => complexityKeywords.high.includes(k))) {
        score += 4;
    }
    
    // Check for medium complexity indicators
    if (keywords.some(k => complexityKeywords.medium.includes(k))) {
        score += 2;
    }
    
    // Check for low complexity indicators
    if (keywords.some(k => complexityKeywords.low.includes(k))) {
        score += 0;
    }
    
    // Adjust for task length (longer descriptions often more complex)
    if (taskDescription.length > 100) score += 1;
    if (taskDescription.length > 200) score += 1;
    
    // Agent-specific adjustments
    const agentComplexityModifiers = {
        'dev': { 'testing': +1, 'deployment': +1, 'security': +2 },
        'pm': { 'research': +1, 'analysis': +1, 'stakeholder': +1 },
        'sm': { 'epic': +1, 'multiple': +1, 'dependencies': +1 }
    };
    
    if (agentComplexityModifiers[agentType]) {
        Object.entries(agentComplexityModifiers[agentType]).forEach(([keyword, modifier]) => {
            if (taskDescription.toLowerCase().includes(keyword)) {
                score += modifier;
            }
        });
    }
    
    // Cap score between 1-10
    score = Math.max(1, Math.min(10, score));
    
    return {
        score: score,
        level: getComplexityLevel(score),
        indicators: identifyComplexityIndicators(taskDescription, keywords),
        adjustments: agentType
    };
}

function getComplexityLevel(score) {
    if (score <= 2) return 'LOW';
    if (score <= 5) return 'MEDIUM';
    if (score <= 8) return 'HIGH';
    return 'VERY_HIGH';
}
```

### 3. selectBestPattern(taskDescription, agentType, complexity)

**Purpose**: Select the most appropriate breakdown pattern

**Implementation**:
```javascript
function selectBestPattern(taskDescription, agentType, complexity) {
    const patterns = getAvailablePatterns();
    const keywords = extractKeywords(taskDescription.toLowerCase());
    
    let bestPattern = null;
    let highestScore = 0;
    
    for (const pattern of patterns) {
        let score = 0;
        
        // Match pattern keywords
        const keywordMatches = pattern.keywords.filter(k => keywords.includes(k));
        score += keywordMatches.length * 2;
        
        // Agent type compatibility
        if (pattern.agentTypes.includes(agentType)) {
            score += 3;
        }
        
        // Complexity compatibility
        if (pattern.complexityRange.includes(complexity.level)) {
            score += 2;
        }
        
        // Task type matching
        if (pattern.taskTypes.some(type => taskDescription.toLowerCase().includes(type))) {
            score += 2;
        }
        
        if (score > highestScore) {
            highestScore = score;
            bestPattern = pattern;
        }
    }
    
    // Fallback to generic pattern if no good match
    if (!bestPattern || highestScore < 3) {
        bestPattern = getGenericPattern(agentType);
        highestScore = 1;
    }
    
    return {
        ...bestPattern,
        confidence: Math.min(100, (highestScore / 10) * 100)
    };
}
```

### 4. generateChunks(taskDescription, pattern, complexity, agentType)

**Purpose**: Generate micro-chunks based on selected pattern

**Implementation**:
```javascript
function generateChunks(taskDescription, pattern, complexity, agentType) {
    let baseChunks = [...pattern.chunks]; // Copy pattern chunks
    
    // Adjust chunks based on complexity
    if (complexity.level === 'LOW') {
        // Combine some chunks for simpler tasks
        baseChunks = combineChunks(baseChunks, 0.7);
    } else if (complexity.level === 'HIGH') {
        // Split chunks for more complex tasks
        baseChunks = expandChunks(baseChunks, 1.3);
    } else if (complexity.level === 'VERY_HIGH') {
        // Significantly expand chunks
        baseChunks = expandChunks(baseChunks, 1.6);
    }
    
    // Agent-specific customizations
    baseChunks = applyAgentCustomizations(baseChunks, agentType, taskDescription);
    
    // Add unique IDs and metadata
    return baseChunks.map((chunk, index) => ({
        id: `chunk-${index + 1}`,
        sequence: index + 1,
        description: chunk.description,
        type: chunk.type,
        dependencies: chunk.dependencies || [],
        estimate: 0, // Will be filled by estimateTiming
        status: 'pending',
        metadata: {
            pattern: pattern.id,
            complexity: complexity.level,
            agentType: agentType
        }
    }));
}
```

### 5. estimateTiming(chunks, agentType, complexity)

**Purpose**: Estimate time requirements for each chunk

**Implementation**:
```javascript
function estimateTiming(chunks, agentType, complexity) {
    const baseEstimates = {
        'setup': { dev: 5, pm: 3, sm: 2 },
        'implementation': { dev: 12, pm: 15, sm: 8 },
        'testing': { dev: 8, pm: 5, sm: 3 },
        'documentation': { dev: 5, pm: 10, sm: 6 },
        'review': { dev: 6, pm: 8, sm: 4 },
        'analysis': { dev: 8, pm: 12, sm: 10 }
    };
    
    const complexityMultipliers = {
        'LOW': 0.8,
        'MEDIUM': 1.0,
        'HIGH': 1.3,
        'VERY_HIGH': 1.6
    };
    
    return chunks.map(chunk => {
        const baseTime = baseEstimates[chunk.type]?.[agentType] || 8;
        const complexityMultiplier = complexityMultipliers[complexity.level] || 1.0;
        const estimate = Math.round(baseTime * complexityMultiplier);
        
        // Ensure estimates are within bounds (5-15 minutes)
        const boundedEstimate = Math.max(5, Math.min(15, estimate));
        
        return {
            ...chunk,
            estimate: boundedEstimate,
            originalEstimate: estimate,
            confidence: calculateEstimateConfidence(chunk, agentType)
        };
    });
}
```

## Pattern Library

### Available Patterns

```javascript
const PATTERNS = {
    'feature-implementation': {
        id: 'feature-implementation',
        name: 'Feature Implementation',
        agentTypes: ['dev'],
        complexityRange: ['MEDIUM', 'HIGH', 'VERY_HIGH'],
        keywords: ['implement', 'feature', 'build', 'create'],
        taskTypes: ['feature', 'functionality', 'component'],
        chunks: [
            { description: 'Set up development environment', type: 'setup' },
            { description: 'Create core implementation', type: 'implementation' },
            { description: 'Add error handling and validation', type: 'implementation' },
            { description: 'Write comprehensive unit tests', type: 'testing' },
            { description: 'Integration testing', type: 'testing' },
            { description: 'Update documentation', type: 'documentation' }
        ]
    },
    
    'bug-fix': {
        id: 'bug-fix',
        name: 'Bug Fix',
        agentTypes: ['dev'],
        complexityRange: ['LOW', 'MEDIUM'],
        keywords: ['fix', 'bug', 'issue', 'error', 'problem'],
        taskTypes: ['bug', 'fix', 'issue'],
        chunks: [
            { description: 'Reproduce and analyze the issue', type: 'analysis' },
            { description: 'Identify root cause', type: 'analysis' },
            { description: 'Implement fix', type: 'implementation' },
            { description: 'Test fix thoroughly', type: 'testing' },
            { description: 'Verify no regression', type: 'testing' }
        ]
    },
    
    'story-creation': {
        id: 'story-creation',
        name: 'Story Creation',
        agentTypes: ['sm'],
        complexityRange: ['LOW', 'MEDIUM', 'HIGH'],
        keywords: ['story', 'create', 'draft', 'epic'],
        taskTypes: ['story', 'user story'],
        chunks: [
            { description: 'Load configuration and context', type: 'setup' },
            { description: 'Identify story position and number', type: 'analysis' },
            { description: 'Analyze epic requirements', type: 'analysis' },
            { description: 'Extract technical context', type: 'analysis' },
            { description: 'Generate story content', type: 'implementation' },
            { description: 'Validate and save story file', type: 'review' }
        ]
    },
    
    'prd-creation': {
        id: 'prd-creation',
        name: 'PRD Creation',
        agentTypes: ['pm'],
        complexityRange: ['MEDIUM', 'HIGH', 'VERY_HIGH'],
        keywords: ['prd', 'requirements', 'product', 'specification'],
        taskTypes: ['prd', 'document', 'requirements'],
        chunks: [
            { description: 'Market research and analysis', type: 'analysis' },
            { description: 'Competitive analysis', type: 'analysis' },
            { description: 'Define user personas', type: 'analysis' },
            { description: 'Create feature structure', type: 'implementation' },
            { description: 'Write detailed requirements', type: 'implementation' },
            { description: 'Define acceptance criteria', type: 'implementation' },
            { description: 'Review and refine document', type: 'review' },
            { description: 'Format and finalize', type: 'documentation' }
        ]
    },
    
    'generic-task': {
        id: 'generic-task',
        name: 'Generic Task',
        agentTypes: ['dev', 'pm', 'sm', 'analyst', 'qa', 'architect'],
        complexityRange: ['LOW', 'MEDIUM', 'HIGH', 'VERY_HIGH'],
        keywords: [],
        taskTypes: [],
        chunks: [
            { description: 'Analyze task requirements', type: 'analysis' },
            { description: 'Plan implementation approach', type: 'setup' },
            { description: 'Execute main task activities', type: 'implementation' },
            { description: 'Validate and test results', type: 'testing' },
            { description: 'Finalize and document', type: 'documentation' }
        ]
    }
};
```

## Helper Functions

### Keyword Extraction

```javascript
function extractKeywords(text) {
    // Remove common words and extract meaningful keywords
    const commonWords = ['the', 'a', 'an', 'and', 'or', 'but', 'in', 'on', 'at', 'to', 'for', 'of', 'with', 'by'];
    return text
        .split(/\s+/)
        .map(word => word.replace(/[^\w]/g, '').toLowerCase())
        .filter(word => word.length > 2 && !commonWords.includes(word));
}
```

### Chunk Optimization

```javascript
function validateAndOptimize(chunks) {
    // Ensure chunks are within time bounds
    let optimizedChunks = chunks.map(chunk => {
        if (chunk.estimate < 5) {
            // Try to combine with next chunk
            return { ...chunk, needsCombining: true };
        }
        if (chunk.estimate > 15) {
            // Try to split chunk
            return { ...chunk, needsSplitting: true };
        }
        return chunk;
    });
    
    // Apply optimizations
    optimizedChunks = applyCombinations(optimizedChunks);
    optimizedChunks = applySplitting(optimizedChunks);
    
    // Ensure logical sequence
    optimizedChunks = ensureLogicalSequence(optimizedChunks);
    
    return optimizedChunks;
}
```

## Integration Instructions

### For Agent Integration

Add this to your agent's dependencies:
```yaml
dependencies:
  utils:
    - micro-chunk-analyzer
```

### Usage in Agent Code

```javascript
// At the start of task execution
const analyzer = loadUtility('micro-chunk-analyzer');
const breakdown = await analyzer.analyzeAndBreakdown(taskDescription, 'dev');

// Use breakdown for progress display
console.log(`🎯 **Task**: ${breakdown.task}`);
console.log(`📅 **Estimated Duration**: ${breakdown.totalEstimate} minutes`);
console.log(`📋 **Micro-Chunks Identified**:`);

breakdown.chunks.forEach(chunk => {
    console.log(`⏳ ${chunk.sequence}. ${chunk.description} (${chunk.estimate} min)`);
});
```

## Configuration Options

### Default Configuration

```javascript
const DEFAULT_CONFIG = {
    chunkSizeTarget: { min: 5, max: 15 }, // minutes
    complexityThresholds: { low: 2, medium: 5, high: 8 },
    estimateConfidence: 0.8,
    enableOptimization: true,
    enablePatternLearning: true
};
```

### Agent-Specific Overrides

```javascript
const AGENT_CONFIGS = {
    'dev': {
        chunkSizeTarget: { min: 5, max: 15 },
        focusAreas: ['implementation', 'testing', 'documentation']
    },
    'pm': {
        chunkSizeTarget: { min: 8, max: 20 },
        focusAreas: ['analysis', 'research', 'documentation']
    },
    'sm': {
        chunkSizeTarget: { min: 3, max: 12 },
        focusAreas: ['analysis', 'implementation', 'review']
    }
};
```

## Performance Optimization

### Caching Strategy

```javascript
// Cache pattern selections and complexity analysis
const analysisCache = new Map();
const patternCache = new Map();

function getCachedAnalysis(taskDescription, agentType) {
    const key = `${taskDescription}-${agentType}`;
    return analysisCache.get(key);
}

function cacheAnalysis(taskDescription, agentType, result) {
    const key = `${taskDescription}-${agentType}`;
    analysisCache.set(key, result);
}
```

### Async Processing

```javascript
// Process complex analysis asynchronously
async function analyzeComplexityAsync(taskDescription, agentType) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve(analyzeComplexity(taskDescription, agentType));
        }, 0);
    });
}
```

## Error Handling

### Graceful Fallbacks

```javascript
function safeAnalyzeAndBreakdown(taskDescription, agentType, options = {}) {
    try {
        return analyzeAndBreakdown(taskDescription, agentType, options);
    } catch (error) {
        console.warn('Micro-chunk analysis failed, using fallback:', error.message);
        
        // Return simple fallback breakdown
        return {
            task: taskDescription,
            agentType: agentType,
            complexity: { score: 5, level: 'MEDIUM' },
            pattern: 'generic-task',
            chunks: generateFallbackChunks(taskDescription),
            totalEstimate: 30,
            metadata: {
                fallback: true,
                error: error.message
            }
        };
    }
}
```

## Exports

```javascript
module.exports = {
    analyzeAndBreakdown,
    analyzeComplexity,
    selectBestPattern,
    generateChunks,
    estimateTiming,
    safeAnalyzeAndBreakdown,
    getAvailablePatterns: () => Object.values(PATTERNS),
    updatePattern,
    addCustomPattern
};
``` 