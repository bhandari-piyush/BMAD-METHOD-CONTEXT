# Chat Progress Display System

## Purpose

Real-time progress visualization system for displaying micro-chunk progress directly in the chat interface, providing immediate feedback and transparency across all platforms (Cursor, VS Code, CLI, Web).

## Usage Instructions

[[LLM: This utility provides functions to display and update micro-chunk progress in real-time within the chat interface]]

### Basic Usage

```javascript
// Initialize progress display
const progressDisplay = require('./chat-progress-display');

// Start tracking task progress
const taskId = progressDisplay.startTask({
    taskName: "Implement user authentication",
    chunks: breakdownChunks,
    agentType: 'dev'
});

// Update progress as chunks complete
progressDisplay.updateChunk(taskId, chunkId, 'in-progress');
progressDisplay.updateChunk(taskId, chunkId, 'complete', { 
    filesChanged: ['auth.js', 'login.html'],
    linesAdded: 45 
});
```

## Core Functions

### 1. startTask(taskConfig)

**Purpose**: Initialize task tracking and display initial progress overview

**Parameters**:
- `taskConfig` (object): Task configuration with chunks and metadata

**Returns**: Unique task ID for tracking

**Implementation**:
```javascript
function startTask(taskConfig) {
    const taskId = generateTaskId();
    const startTime = Date.now();
    
    // Store task data
    activeTasks.set(taskId, {
        id: taskId,
        name: taskConfig.taskName,
        agentType: taskConfig.agentType,
        chunks: taskConfig.chunks,
        startTime: startTime,
        status: 'active',
        progress: {
            completed: 0,
            total: taskConfig.chunks.length,
            percentage: 0
        }
    });
    
    // Display initial task overview
    displayTaskOverview(taskId);
    
    return taskId;
}
```

### 2. displayTaskOverview(taskId)

**Purpose**: Display the initial task breakdown with all micro-chunks

**Implementation**:
```javascript
function displayTaskOverview(taskId) {
    const task = activeTasks.get(taskId);
    if (!task) return;
    
    const totalEstimate = task.chunks.reduce((sum, chunk) => sum + chunk.estimate, 0);
    
    console.log(`
🎯 **Task**: ${task.name}
👨‍💻 **Agent**: ${task.agentType.toUpperCase()} 
📅 **Estimated Duration**: ${totalEstimate} minutes
📋 **Micro-Chunks Identified**:
`);
    
    // Display all chunks with pending status
    task.chunks.forEach((chunk, index) => {
        const statusIcon = getStatusIcon('pending');
        const progressBar = getProgressBar(0);
        
        console.log(`${statusIcon} ${chunk.sequence}. ${chunk.description} (${chunk.estimate} min)`);
    });
    
    console.log(`
📊 **Progress**: ${task.progress.completed}/${task.progress.total} chunks (${task.progress.percentage}%)
⏰ **Started**: ${formatTimestamp(task.startTime)}
─────────────────────────────────────────────────────────
`);
}
```

### 3. updateChunk(taskId, chunkId, status, metadata = {})

**Purpose**: Update individual chunk status and refresh display

**Parameters**:
- `taskId` (string): Task identifier
- `chunkId` (string): Chunk identifier
- `status` (string): New status ('pending', 'in-progress', 'complete', 'failed')
- `metadata` (object): Additional progress data

**Implementation**:
```javascript
function updateChunk(taskId, chunkId, status, metadata = {}) {
    const task = activeTasks.get(taskId);
    if (!task) return;
    
    // Find and update chunk
    const chunk = task.chunks.find(c => c.id === chunkId);
    if (!chunk) return;
    
    const previousStatus = chunk.status;
    chunk.status = status;
    chunk.updatedAt = Date.now();
    
    // Add metadata
    if (metadata.filesChanged) chunk.filesChanged = metadata.filesChanged;
    if (metadata.linesAdded) chunk.linesAdded = metadata.linesAdded;
    if (metadata.linesRemoved) chunk.linesRemoved = metadata.linesRemoved;
    if (metadata.duration) chunk.actualDuration = metadata.duration;
    
    // Update task progress
    updateTaskProgress(taskId);
    
    // Display real-time update
    displayChunkUpdate(task, chunk, previousStatus, status);
    
    // Check if task is complete
    if (isTaskComplete(task)) {
        displayTaskCompletion(taskId);
    }
}
```

### 4. displayChunkUpdate(task, chunk, previousStatus, newStatus)

**Purpose**: Show real-time chunk status update

**Implementation**:
```javascript
function displayChunkUpdate(task, chunk, previousStatus, newStatus) {
    const statusIcon = getStatusIcon(newStatus);
    const timestamp = formatTimestamp(chunk.updatedAt);
    
    // Status change announcement
    const statusMessage = getStatusMessage(previousStatus, newStatus);
    
    console.log(`
${statusIcon} **${chunk.sequence}. ${chunk.description}** ${statusMessage}
   ${getProgressDetails(chunk)}
   ⏰ ${timestamp}
`);
    
    // Show file changes if available
    if (chunk.filesChanged && chunk.filesChanged.length > 0) {
        console.log(`   📁 Files: ${chunk.filesChanged.join(', ')}`);
    }
    
    // Show line changes if available
    if (chunk.linesAdded || chunk.linesRemoved) {
        const additions = chunk.linesAdded ? `+${chunk.linesAdded}` : '';
        const deletions = chunk.linesRemoved ? `-${chunk.linesRemoved}` : '';
        console.log(`   📝 Changes: ${additions} ${deletions}`);
    }
    
    // Show duration if completed
    if (newStatus === 'complete' && chunk.actualDuration) {
        const efficiency = calculateEfficiency(chunk.estimate, chunk.actualDuration);
        console.log(`   ⏱️ Duration: ${chunk.actualDuration} min (${efficiency})`);
    }
    
    // Update overall progress
    displayProgressUpdate(task);
}
```

### 5. displayProgressUpdate(task)

**Purpose**: Show updated overall task progress

**Implementation**:
```javascript
function displayProgressUpdate(task) {
    const progressBar = generateProgressBar(task.progress.percentage);
    const eta = calculateETA(task);
    
    console.log(`
📊 **Progress**: ${task.progress.completed}/${task.progress.total} chunks (${task.progress.percentage}%)
${progressBar}
⏰ **ETA**: ${eta}
─────────────────────────────────────────────────────────
`);
}
```

### 6. displayTaskCompletion(taskId)

**Purpose**: Show comprehensive task completion summary

**Implementation**:
```javascript
function displayTaskCompletion(taskId) {
    const task = activeTasks.get(taskId);
    if (!task) return;
    
    const completionTime = Date.now();
    const totalDuration = Math.round((completionTime - task.startTime) / 1000 / 60);
    const estimatedDuration = task.chunks.reduce((sum, chunk) => sum + chunk.estimate, 0);
    
    console.log(`
🎉 **TASK COMPLETED!** 🎉
═══════════════════════════════════════════════════════════

🎯 **Task**: ${task.name}
👨‍💻 **Agent**: ${task.agentType.toUpperCase()}
✅ **Status**: All ${task.chunks.length} micro-chunks completed successfully

⏰ **Timing Summary**:
   • Estimated: ${estimatedDuration} minutes
   • Actual: ${totalDuration} minutes
   • Efficiency: ${calculateOverallEfficiency(estimatedDuration, totalDuration)}

📁 **Files Modified**: ${getUniqueFiles(task.chunks).length} files
📝 **Code Changes**: ${getTotalLineChanges(task.chunks)}

🚀 **Chunk Breakdown**:
`);
    
    // Show each completed chunk
    task.chunks.forEach(chunk => {
        const duration = chunk.actualDuration || chunk.estimate;
        const efficiency = chunk.actualDuration ? 
            calculateEfficiency(chunk.estimate, chunk.actualDuration) : 'estimated';
        
        console.log(`   ✅ ${chunk.description} (${duration} min - ${efficiency})`);
    });
    
    console.log(`
💡 **Key Achievements**:
${generateAchievements(task)}

🎯 **Next Steps**: ${generateNextSteps(task)}
═══════════════════════════════════════════════════════════
`);
    
    // Archive completed task
    archiveTask(taskId);
}
```

## Status Icons and Indicators

### Status Icon System

```javascript
function getStatusIcon(status) {
    const icons = {
        'pending': '⏳',
        'in-progress': '🟡',
        'complete': '✅',
        'failed': '❌',
        'blocked': '🚫',
        'skipped': '⏭️'
    };
    
    return icons[status] || '❓';
}
```

### Progress Bar Generation

```javascript
function generateProgressBar(percentage, width = 20) {
    const filled = Math.round((percentage / 100) * width);
    const empty = width - filled;
    
    const filledBar = '█'.repeat(filled);
    const emptyBar = '░'.repeat(empty);
    
    return `[${filledBar}${emptyBar}] ${percentage}%`;
}
```

### Status Messages

```javascript
function getStatusMessage(previousStatus, newStatus) {
    const messages = {
        'pending->in-progress': '🚀 **STARTED**',
        'in-progress->complete': '✅ **COMPLETED**',
        'in-progress->failed': '❌ **FAILED**',
        'pending->complete': '⚡ **COMPLETED**',
        'complete->in-progress': '🔄 **RESTARTED**'
    };
    
    const key = `${previousStatus}->${newStatus}`;
    return messages[key] || `➡️ **${newStatus.toUpperCase()}**`;
}
```

## Progress Calculation

### Task Progress Updates

```javascript
function updateTaskProgress(taskId) {
    const task = activeTasks.get(taskId);
    if (!task) return;
    
    const completed = task.chunks.filter(c => c.status === 'complete').length;
    const total = task.chunks.length;
    const percentage = Math.round((completed / total) * 100);
    
    task.progress = {
        completed: completed,
        total: total,
        percentage: percentage
    };
    
    // Update task status
    if (completed === total) {
        task.status = 'complete';
        task.completedAt = Date.now();
    } else if (completed > 0) {
        task.status = 'in-progress';
    }
}
```

### ETA Calculation

```javascript
function calculateETA(task) {
    const completedChunks = task.chunks.filter(c => c.status === 'complete');
    const remainingChunks = task.chunks.filter(c => c.status !== 'complete');
    
    if (completedChunks.length === 0) {
        // Use estimates for all remaining chunks
        const estimatedMinutes = remainingChunks.reduce((sum, chunk) => sum + chunk.estimate, 0);
        return formatDuration(estimatedMinutes);
    }
    
    // Calculate average actual duration for completed chunks
    const completedWithDuration = completedChunks.filter(c => c.actualDuration);
    if (completedWithDuration.length > 0) {
        const avgActualDuration = completedWithDuration.reduce((sum, chunk) => sum + chunk.actualDuration, 0) / completedWithDuration.length;
        const estimatedMinutes = remainingChunks.length * avgActualDuration;
        return formatDuration(estimatedMinutes);
    }
    
    // Fallback to estimates
    const estimatedMinutes = remainingChunks.reduce((sum, chunk) => sum + chunk.estimate, 0);
    return formatDuration(estimatedMinutes);
}
```

## Efficiency Tracking

### Individual Chunk Efficiency

```javascript
function calculateEfficiency(estimated, actual) {
    if (!actual || !estimated) return 'N/A';
    
    const ratio = actual / estimated;
    
    if (ratio <= 0.8) return '🚀 Ahead of schedule';
    if (ratio <= 1.0) return '✅ On schedule';
    if (ratio <= 1.2) return '⚠️ Slightly behind';
    if (ratio <= 1.5) return '⚠️ Behind schedule';
    return '🚨 Significantly behind';
}
```

### Overall Task Efficiency

```javascript
function calculateOverallEfficiency(estimated, actual) {
    const ratio = actual / estimated;
    const percentage = Math.round(ratio * 100);
    
    if (ratio <= 0.8) return `🚀 ${percentage}% - Excellent performance!`;
    if (ratio <= 1.0) return `✅ ${percentage}% - Perfect timing!`;
    if (ratio <= 1.2) return `⚠️ ${percentage}% - Good performance`;
    return `⚠️ ${percentage}% - Room for improvement`;
}
```

## Advanced Features

### File Change Tracking

```javascript
function trackFileChanges(chunkId, filesChanged) {
    const chunk = findChunkById(chunkId);
    if (!chunk) return;
    
    chunk.filesChanged = filesChanged;
    chunk.fileChangeTimestamp = Date.now();
    
    // Analyze file changes
    const fileStats = analyzeFileChanges(filesChanged);
    chunk.codeMetrics = fileStats;
}

function analyzeFileChanges(filesChanged) {
    return filesChanged.map(file => ({
        path: file,
        type: getFileType(file),
        size: getFileSize(file),
        lastModified: Date.now()
    }));
}
```

### Real-time Progress Streaming

```javascript
function streamProgress(taskId, callback) {
    const task = activeTasks.get(taskId);
    if (!task) return;
    
    // Set up real-time callback
    task.progressCallback = callback;
    
    // Stream current state
    callback({
        type: 'progress-update',
        task: task,
        timestamp: Date.now()
    });
}
```

### Progress Persistence

```javascript
function saveProgress(taskId) {
    const task = activeTasks.get(taskId);
    if (!task) return;
    
    const progressData = {
        taskId: taskId,
        progress: task.progress,
        chunks: task.chunks.map(chunk => ({
            id: chunk.id,
            status: chunk.status,
            actualDuration: chunk.actualDuration,
            filesChanged: chunk.filesChanged
        })),
        savedAt: Date.now()
    };
    
    // Save to persistent storage
    saveToStorage('task-progress', taskId, progressData);
}
```

## Platform-Specific Adaptations

### Chat Interface Optimization

```javascript
function formatForChatInterface(content, platform = 'universal') {
    const adaptations = {
        'cursor': addCursorFormatting,
        'vscode': addVSCodeFormatting,
        'cli': addCLIFormatting,
        'web': addWebFormatting,
        'universal': addUniversalFormatting
    };
    
    const formatter = adaptations[platform] || adaptations['universal'];
    return formatter(content);
}
```

### Color and Emoji Support

```javascript
function addColorSupport(text, platform) {
    if (platform === 'cli') {
        // Add ANSI color codes
        return text
            .replace(/\*\*(.*?)\*\*/g, '\x1b[1m$1\x1b[0m') // Bold
            .replace(/🎯/g, '\x1b[36m🎯\x1b[0m') // Cyan
            .replace(/✅/g, '\x1b[32m✅\x1b[0m') // Green
            .replace(/❌/g, '\x1b[31m❌\x1b[0m'); // Red
    }
    
    return text; // Keep original for other platforms
}
```

## Error Handling and Fallbacks

### Graceful Degradation

```javascript
function safeDisplayUpdate(taskId, chunkId, status, metadata) {
    try {
        return updateChunk(taskId, chunkId, status, metadata);
    } catch (error) {
        console.warn('Progress display error:', error.message);
        
        // Fallback to simple update
        console.log(`[${status.toUpperCase()}] Chunk ${chunkId} updated`);
        
        // Log error for debugging
        logError('chat-progress-display', error, { taskId, chunkId, status });
    }
}
```

### Recovery Mechanisms

```javascript
function recoverProgress(taskId) {
    try {
        const savedProgress = loadFromStorage('task-progress', taskId);
        if (savedProgress) {
            const task = activeTasks.get(taskId);
            if (task) {
                // Restore progress state
                task.progress = savedProgress.progress;
                task.chunks.forEach(chunk => {
                    const saved = savedProgress.chunks.find(c => c.id === chunk.id);
                    if (saved) {
                        chunk.status = saved.status;
                        chunk.actualDuration = saved.actualDuration;
                        chunk.filesChanged = saved.filesChanged;
                    }
                });
                
                console.log('✅ Progress recovered from saved state');
                return true;
            }
        }
    } catch (error) {
        console.warn('Failed to recover progress:', error.message);
    }
    
    return false;
}
```

## Configuration and Customization

### Display Configuration

```javascript
const DISPLAY_CONFIG = {
    showProgressBar: true,
    showETA: true,
    showFileChanges: true,
    showEfficiency: true,
    showDetailedSummary: true,
    animateProgress: false,
    maxLineLength: 80,
    dateFormat: 'HH:mm:ss',
    colors: {
        pending: '#FFA500',
        inProgress: '#FFFF00',
        complete: '#00FF00',
        failed: '#FF0000'
    }
};
```

### Agent-Specific Customizations

```javascript
const AGENT_DISPLAY_CONFIGS = {
    'dev': {
        showFileChanges: true,
        showCodeMetrics: true,
        showTestResults: true,
        emphasizeImplementation: true
    },
    'pm': {
        showBusinessValue: true,
        showStakeholderUpdates: true,
        showMarketInsights: true,
        emphasizeAnalysis: true
    },
    'sm': {
        showStoryProgress: true,
        showEpicContext: true,
        showTeamUpdates: true,
        emphasizeDelivery: true
    }
};
```

## Integration Interface

### Agent Integration

```javascript
// Export interface for agent integration
module.exports = {
    // Core functions
    startTask,
    updateChunk,
    completeTask,
    failTask,
    
    // Progress tracking
    getTaskProgress,
    streamProgress,
    
    // Display functions
    displayTaskOverview,
    displayChunkUpdate,
    displayProgressUpdate,
    displayTaskCompletion,
    
    // Utilities
    formatDuration,
    calculateEfficiency,
    generateProgressBar,
    
    // Configuration
    setDisplayConfig,
    getDisplayConfig,
    
    // Error handling
    safeDisplayUpdate,
    recoverProgress
};
```

### Usage Example

```javascript
// Complete integration example
const progressDisplay = require('./chat-progress-display');

async function executeTaskWithProgress(taskDescription, agentType) {
    // Get task breakdown
    const breakdown = await analyzer.analyzeAndBreakdown(taskDescription, agentType);
    
    // Start progress tracking
    const taskId = progressDisplay.startTask({
        taskName: taskDescription,
        chunks: breakdown.chunks,
        agentType: agentType
    });
    
    // Execute each chunk
    for (const chunk of breakdown.chunks) {
        try {
            // Update status to in-progress
            progressDisplay.updateChunk(taskId, chunk.id, 'in-progress');
            
            // Execute chunk work
            const result = await executeChunk(chunk);
            
            // Update status to complete with metadata
            progressDisplay.updateChunk(taskId, chunk.id, 'complete', {
                filesChanged: result.filesChanged,
                linesAdded: result.linesAdded,
                duration: result.duration
            });
            
        } catch (error) {
            // Update status to failed
            progressDisplay.updateChunk(taskId, chunk.id, 'failed', {
                error: error.message
            });
            
            throw error;
        }
    }
    
    return taskId;
}
``` 