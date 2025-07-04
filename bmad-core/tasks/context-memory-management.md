# Context Memory Management Task

## Overview
Advanced context memory management system for planning agents with long-term context storage, intelligent archiving strategies, retrieval optimization, memory lifecycle management, and cross-session context persistence.

**Target Agents**: Planning agents only (orchestrator, architect, pm, po, analyst, ux-expert, qa, sm)  
**Purpose**: Enable persistent context storage and intelligent memory management across sessions  
**Complexity**: High - Rich context feature for advanced workflows  

---

## Task Configuration

```yaml
task_type: context_memory_management
agent_compatibility: planning_only
dependencies:
  utils:
    - context-compression
    - context-filtering
    - context-analysis
  tasks:
    - context-validation
    - context-retrieval
complexity: high
estimated_time: 3-7_minutes
output_format: memory_operations
```

---

## Core Memory Management Procedures

### 1. Long-Term Context Storage

**Purpose**: Persistent storage of important context across agent sessions

**Storage Architecture**:
```
memory_store/
├── active_context/          # Current session context
├── session_archives/        # Historical session data
├── persistent_knowledge/    # Long-term project knowledge
├── shared_memory/          # Cross-agent shared context
└── compressed_archives/    # Optimized historical storage
```

**Storage Process**:
1. **[[LLM: Analyze context importance for storage decisions]]**
2. **Categorize context type**: {{context_category}} (decisions, learnings, patterns, references)
3. **Determine storage duration**: {{retention_period}} (session/short-term/long-term/permanent)
4. **Apply compression strategy**: {{compression_level}} based on access frequency

**Storage Criteria**:
- **Permanent storage**: Critical decisions, key learnings, project foundations
- **Long-term storage**: Important patterns, successful approaches, reference materials  
- **Short-term storage**: Session context, temporary work, draft materials
- **Ephemeral storage**: Transient data, cache, temporary calculations

### 2. Context Archiving Strategies

**Purpose**: Intelligent archiving to optimize memory usage while preserving access

**Archiving Triggers**:
- **Time-based**: Archive context older than {{archive_threshold}} days
- **Usage-based**: Archive context with access frequency < {{min_access_frequency}}
- **Size-based**: Archive when active memory > {{memory_size_limit}}
- **Relevance-based**: Archive context with declining relevance scores

**Archiving Process**:

#### Stage 1: Archive Candidate Selection
```
FOR each context_item IN active_memory:
  CALCULATE archive_score = (
    time_factor * 0.3 +
    usage_factor * 0.4 +  
    relevance_factor * 0.2 +
    size_factor * 0.1
  )
  IF archive_score > {{archive_threshold}}:
    ADD context_item TO archive_candidates
```

#### Stage 2: Compression and Storage
```
FOR each candidate IN archive_candidates:
  APPLY context_compression WITH level={{archive_compression_level}}
  GENERATE metadata_summary
  STORE compressed_context IN session_archives/{{session_id}}/
  UPDATE memory_index WITH archived_location
```

#### Stage 3: Active Memory Cleanup
```
REMOVE archived_items FROM active_memory
UPDATE cross_references TO archived_locations
OPTIMIZE remaining_memory_structure
```

### 3. Memory Lifecycle Management

**Purpose**: Systematic management of context from creation to disposal

**Lifecycle Stages**:

#### Creation and Initial Storage
- **Context ingestion**: Receive and process new context
- **Initial classification**: Categorize by type, importance, expected lifespan
- **Storage allocation**: Place in appropriate memory tier
- **Metadata generation**: Create searchable metadata and tags

#### Active Memory Phase
- **Access tracking**: Monitor usage patterns and frequency
- **Relevance updates**: Continuously assess current relevance
- **Cross-linking**: Establish connections with related context
- **Compression optimization**: Apply progressive compression as access decreases

#### Archive Transition Phase  
- **Archive eligibility assessment**: Evaluate archiving criteria
- **Dependency checking**: Ensure no active references prevent archiving
- **Compression application**: Apply appropriate compression level
- **Metadata preservation**: Maintain searchability in archived state

#### Long-Term Storage Phase
- **Periodic relevance review**: Reassess long-term value
- **Compression optimization**: Increase compression as access further decreases
- **Integrity maintenance**: Verify stored context remains accessible
- **Disposal consideration**: Evaluate for eventual removal

#### Disposal Phase (if applicable)
- **Final relevance check**: Confirm context no longer needed
- **Dependency verification**: Ensure no remaining references
- **Secure disposal**: Remove context while preserving audit trail
- **Metadata cleanup**: Update indexes and references

### 4. Cross-Session Context Persistence

**Purpose**: Maintain context continuity across agent restart and project phases

**Persistence Strategies**:

#### Session Context Preservation
```
ON session_end:
  IDENTIFY persistent_context_elements
  COMPRESS session_context TO optimal_size
  STORE session_summary IN persistent_storage
  UPDATE global_context_index
```

#### Cross-Session Context Restoration
```
ON session_start:
  LOAD relevant_persistent_context FOR current_project
  RESTORE active_work_context FROM last_session
  ESTABLISH context_continuity_links
  OPTIMIZE memory_layout FOR current_workflow
```

#### Multi-Agent Context Sharing
- **Shared context pools**: Common knowledge accessible to all agents
- **Agent-specific context**: Personal working memory and preferences
- **Project context inheritance**: New agents inherit relevant project context
- **Context handoff protocols**: Structured transfer between agents

---

## Advanced Memory Features

### 1. Intelligent Context Compression

**Purpose**: Optimize memory usage while preserving information value

**Compression Strategies**:

#### Lossless Compression (High-Value Context)
- **Reference compression**: Replace repeated information with references
- **Structure optimization**: Reorganize data for space efficiency  
- **Redundancy elimination**: Remove duplicate information across contexts
- **Format optimization**: Use efficient encoding for structured data

#### Lossy Compression (Lower-Value Context)
- **Summary generation**: Create condensed versions of detailed content
- **Key point extraction**: Preserve only essential information elements
- **Progressive detail loss**: Gradually reduce detail level over time
- **Relevance-based filtering**: Remove least relevant information first

#### Adaptive Compression
```
FUNCTION adaptive_compress(context_item, access_frequency, importance_score):
  IF importance_score > 0.8:
    APPLY lossless_compression
  ELIF access_frequency > weekly:
    APPLY moderate_lossy_compression  
  ELSE:
    APPLY aggressive_lossy_compression
  RETURN compressed_context
```

### 2. Context Retrieval Optimization

**Purpose**: Fast and accurate retrieval from memory stores

**Optimization Techniques**:

#### Indexing Strategies
- **Semantic indexing**: Enable concept-based search across memory
- **Temporal indexing**: Time-based organization for chronological access
- **Agent-specific indexing**: Optimize for individual agent access patterns
- **Cross-reference indexing**: Map relationships between context items

#### Caching Mechanisms
```
memory_cache:
  hot_cache:     # Frequently accessed context (in-memory)
    size_limit: {{hot_cache_size}}MB
    eviction_policy: LRU_with_importance_weighting
  
  warm_cache:    # Occasionally accessed context (fast storage)  
    size_limit: {{warm_cache_size}}MB
    eviction_policy: time_and_frequency_based
    
  cold_storage:  # Archived context (slower retrieval)
    compression_level: high
    access_method: on_demand_decompression
```

#### Predictive Pre-loading
- **Workflow pattern recognition**: Learn common context access patterns
- **Predictive retrieval**: Pre-load likely-needed context into cache
- **Agent behavior learning**: Adapt to individual agent working styles
- **Project phase optimization**: Adjust pre-loading for current project phase

### 3. Memory Quality Management

**Purpose**: Ensure stored context maintains high quality and usefulness

**Quality Assurance Processes**:

#### Content Validation
- **Accuracy verification**: Cross-check stored information for correctness
- **Completeness assessment**: Ensure context contains sufficient detail
- **Consistency checking**: Verify consistency with related stored context
- **Currency validation**: Ensure information remains current and relevant

#### Quality Metrics Tracking
```
context_quality_metrics:
  accuracy_score: 0.0-1.0    # Factual correctness assessment
  completeness_score: 0.0-1.0 # Information sufficiency rating  
  relevance_score: 0.0-1.0   # Current applicability assessment
  freshness_score: 0.0-1.0   # Information currency rating
  coherence_score: 0.0-1.0   # Internal consistency rating
```

#### Quality Improvement Actions
- **Context enrichment**: Add missing information to incomplete context
- **Accuracy corrections**: Update incorrect or outdated information
- **Relevance updates**: Adjust relevance scores based on current needs
- **Structure optimization**: Reorganize context for better usability

---

## Memory Management Workflows

### Workflow 1: Context Storage Decision

**Input**: New context requiring storage decision
**Output**: Stored context with appropriate classification and metadata

**Process Steps**:
1. **Context Analysis**
   - **[[LLM: Analyze context importance, type, and expected lifespan]]**
   - **Determine storage tier**: {{storage_tier}} (active/short-term/long-term/permanent)
   - **Calculate retention period**: {{retention_days}} based on context type
   - **Assess compression needs**: {{compression_strategy}}

2. **Storage Execution**
   ```
   CLASSIFY context_type FROM {decision, learning, pattern, reference, temporary}
   CALCULATE importance_score USING content_analysis
   SELECT storage_location BASED_ON tier_and_type
   APPLY compression_strategy IF needed
   GENERATE metadata_tags FOR searchability
   STORE context_with_metadata
   UPDATE memory_indexes
   ```

3. **Storage Validation**
   - **Verify successful storage**: Confirm context is retrievable
   - **Validate metadata accuracy**: Ensure searchable information is correct
   - **Check storage optimization**: Confirm appropriate compression applied
   - **Update usage tracking**: Initialize access monitoring

### Workflow 2: Memory Cleanup and Optimization

**Input**: Memory optimization trigger (size, time, or performance-based)
**Output**: Optimized memory structure with maintained functionality

**Process Steps**:
1. **Memory Analysis**
   ```
   ANALYZE current_memory_usage:
     total_size: {{current_memory_size}}MB
     active_items: {{active_context_count}}
     archive_candidates: {{archivable_items_count}}
     compression_opportunities: {{compressible_items_count}}
   ```

2. **Optimization Strategy Selection**
   - **Archiving focus**: When memory size > {{size_threshold}}
   - **Compression focus**: When access patterns suggest under-utilization  
   - **Cleanup focus**: When quality metrics indicate stale content
   - **Reorganization focus**: When retrieval performance degrades

3. **Optimization Execution**
   ```
   FOR each optimization_action IN selected_strategy:
     EXECUTE optimization_action WITH safety_checks
     VALIDATE memory_integrity_maintained  
     UPDATE performance_metrics
     LOG optimization_results
   ```

### Workflow 3: Cross-Session Context Restoration

**Input**: Agent session start with project context requirements
**Output**: Restored context environment ready for agent operation

**Process Steps**:
1. **Context Requirements Analysis**
   - **[[LLM: Determine necessary context for current agent and workflow]]**
   - **Identify required context types**: {{required_context_categories}}
   - **Calculate context priority levels**: Critical/important/helpful/optional
   - **Estimate memory requirements**: {{estimated_memory_needs}}MB

2. **Context Restoration Process**
   ```
   LOAD critical_context FROM persistent_storage
   RESTORE agent_specific_preferences AND working_memory
   ESTABLISH context_continuity_links FROM previous_sessions
   APPLY context_updates FROM other_agents IF relevant
   OPTIMIZE memory_layout FOR current_workflow_requirements
   ```

3. **Restoration Validation**
   - **Verify context completeness**: Ensure all required context loaded
   - **Check context currency**: Validate information is up-to-date
   - **Test context accessibility**: Confirm retrieval systems functional
   - **Validate agent readiness**: Ensure agent can operate effectively

---

## Error Handling and Recovery

### Memory Corruption Scenarios

**Corrupted Context Data**:
1. **Detection**: Checksum validation, access errors, inconsistent metadata
2. **Recovery actions**: Restore from backup, reconstruct from related context
3. **Prevention**: Regular integrity checks, redundant storage for critical context

**Storage System Failures**:
1. **Immediate response**: Switch to backup storage systems
2. **Data recovery**: Attempt recovery from multiple storage copies
3. **Graceful degradation**: Continue operation with reduced memory capabilities

**Index Corruption**:
1. **Symptom detection**: Slow retrieval, missing search results, access errors
2. **Index reconstruction**: Rebuild indexes from stored context metadata
3. **Service continuity**: Maintain basic functionality during reconstruction

### Memory Management Failures

**Insufficient Storage Space**:
```
IF available_storage < {{minimum_storage_threshold}}:
  TRIGGER emergency_cleanup_procedures
  ARCHIVE oldest_non_critical_context
  INCREASE compression_levels_temporarily
  ALERT memory_management_system
```

**Context Retrieval Failures**:
1. **Cache miss handling**: Attempt retrieval from deeper storage layers
2. **Corruption recovery**: Use backup copies or reconstruct from related context
3. **Performance degradation**: Switch to simpler retrieval methods temporarily

**Cross-Session Context Loss**:
1. **Session restoration failure**: Attempt recovery from archived sessions
2. **Partial context availability**: Continue with available context, note limitations
3. **Context reconstruction**: Use agent knowledge to rebuild missing context

---

## Integration with Context Ecosystem

### Context Validation Integration
- **Storage validation**: Validate context before long-term storage
- **Retrieval validation**: Verify retrieved context quality and accuracy
- **Cross-reference validation**: Ensure stored context maintains consistency

### Context Compression Synergy
- **Progressive compression**: Apply increasing compression over time
- **Retrieval decompression**: Decompress archived context for active use
- **Compression quality monitoring**: Ensure compression doesn't degrade usefulness

### Context Retrieval Coordination
- **Memory-based retrieval**: Use stored context to enhance retrieval operations
- **Pattern learning**: Store successful retrieval patterns for future use
- **Cross-session learning**: Improve retrieval based on stored interaction patterns

---

## Success Metrics and Monitoring

### Memory Efficiency Metrics
- **Storage utilization**: {{current_usage}}/{{total_capacity}} ratio
- **Compression effectiveness**: {{space_saved}}/{{original_size}} ratio
- **Retrieval performance**: Average retrieval time <1000ms
- **Memory hit rate**: >90% of requests served from memory

### Context Preservation Metrics  
- **Context survival rate**: >95% of important context preserved across sessions
- **Information accuracy**: >98% accuracy maintained in stored context
- **Cross-session continuity**: >90% of relevant context successfully restored
- **Quality degradation rate**: <5% quality loss over time for active context

### User Experience Metrics
- **Context availability**: >99% uptime for memory systems
- **Restoration time**: <30 seconds for full context restoration
- **Search effectiveness**: >85% successful context retrieval rate
- **Agent productivity**: Measurable improvement in agent effectiveness with memory

---

## Memory Management Templates

### Context Storage Template

```markdown
# Context Storage Record

**Storage Date**: {{storage_timestamp}}  
**Context ID**: {{unique_context_id}}  
**Agent**: {{storing_agent_name}}  
**Project**: {{project_identifier}}  

## Context Classification
- **Type**: {{context_type}} (decision/learning/pattern/reference/temporary)
- **Importance**: {{importance_score}}/1.0  
- **Storage Tier**: {{storage_tier}} (active/short-term/long-term/permanent)
- **Retention Period**: {{retention_days}} days
- **Compression Level**: {{compression_level}}

## Context Summary
{{context_summary}}

## Full Context
{{#if compression_applied}}
*[Compressed content - use context retrieval to access full detail]*
{{else}}
{{full_context_content}}
{{/if}}

## Metadata
- **Tags**: {{context_tags}}
- **Related Contexts**: {{related_context_ids}}
- **Access Count**: {{access_frequency}}
- **Last Accessed**: {{last_access_timestamp}}
- **Quality Score**: {{quality_metrics}}

---
*Stored by: {{agent_name}} | System: Context Memory Management*
```

This context memory management system enables planning agents to maintain sophisticated, persistent memory across sessions, supporting complex long-term projects and multi-agent collaboration with intelligent storage, retrieval, and optimization capabilities. 