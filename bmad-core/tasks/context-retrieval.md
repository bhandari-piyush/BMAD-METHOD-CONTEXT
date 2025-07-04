# Context Retrieval Task

## Overview
Advanced context retrieval system for planning agents with semantic search, intelligent retrieval algorithms, vector search capabilities, relevance scoring mechanisms, and real-time optimization.

**Target Agents**: Planning agents only (orchestrator, architect, pm, po, analyst, ux-expert, qa, sm)  
**Purpose**: Enable intelligent retrieval of relevant context from large knowledge bases  
**Complexity**: High - Rich context feature for advanced workflows  

---

## Task Configuration

```yaml
task_type: context_retrieval
agent_compatibility: planning_only
dependencies:
  utils:
    - semantic-search
    - context-filtering
    - context-compression
  tasks:
    - context-validation
complexity: high
estimated_time: 2-5_minutes
output_format: structured_context
```

---

## Core Retrieval Procedures

### 1. Semantic Search Initialization

**Purpose**: Set up intelligent search context for retrieval operations

**Process**:
1. **[[LLM: Initialize semantic search parameters based on query intent]]**
2. **Define search scope**: {{search_domain}} (project, documentation, code, historical)
3. **Set relevance threshold**: {{relevance_score_minimum}} (default: 0.75)
4. **Configure search depth**: {{search_depth_level}} (surface/deep/comprehensive)

**Input Parameters**:
- `{{query_context}}`: The specific information need driving retrieval
- `{{search_priority}}`: immediate/background/comprehensive
- `{{target_knowledge_domains}}`: Specific areas to focus search
- `{{exclusion_patterns}}`: Information types to avoid retrieving

### 2. Vector Search Implementation

**Purpose**: Execute semantic similarity-based content retrieval

**Vector Search Process**:
1. **[[LLM: Convert search query to semantic embeddings]]**
2. **Execute similarity matching**: Find content with similarity score > {{relevance_score_minimum}}
3. **Rank results by relevance**: Primary relevance, secondary freshness, tertiary completeness
4. **Apply domain filtering**: Focus on {{target_knowledge_domains}}

**Similarity Scoring Criteria**:
- **Semantic relevance**: 40% weight - Content meaning alignment
- **Contextual fit**: 30% weight - Situational appropriateness  
- **Information freshness**: 20% weight - Recency and currency
- **Source authority**: 10% weight - Information source quality

### 3. Intelligent Retrieval Algorithms

**Purpose**: Apply smart filtering and ranking to retrieval results

**Algorithm Stages**:

#### Stage 1: Content Discovery
```
FOR each potential_source IN knowledge_base:
  IF semantic_similarity(query_embeddings, source_embeddings) > {{relevance_score_minimum}}:
    ADD source TO candidate_results
    CALCULATE composite_score(semantic, contextual, freshness, authority)
```

#### Stage 2: Relevance Ranking
```
SORT candidate_results BY composite_score DESC
APPLY diversity_filter TO avoid_redundancy
LIMIT results TO {{max_retrieval_items}} (default: 10)
```

#### Stage 3: Quality Validation
```
FOR each result IN ranked_results:
  VALIDATE content_completeness > 0.8
  VALIDATE information_accuracy > 0.9  
  VALIDATE contextual_appropriateness > 0.7
```

### 4. Real-Time Retrieval Optimization

**Purpose**: Continuously improve retrieval effectiveness during operation

**Optimization Strategies**:

#### Performance Monitoring
- **Response time tracking**: Target <2000ms for semantic search
- **Relevance accuracy**: Monitor user satisfaction with retrieved content
- **Coverage assessment**: Ensure comprehensive domain coverage

#### Adaptive Learning
1. **[[LLM: Learn from retrieval feedback to improve future searches]]**
2. **Update similarity weights** based on successful retrievals
3. **Refine domain mappings** for better content categorization
4. **Optimize embedding strategies** for improved semantic matching

#### Cache Management
- **Cache frequent queries**: Store results for common search patterns
- **Invalidate stale content**: Remove outdated cached results
- **Preload anticipated needs**: Predictive retrieval for workflow patterns

---

## Retrieval Execution Workflow

### Step 1: Query Analysis and Preparation

**Input Processing**:
```
ANALYZE query_intent FROM {{user_request}}
IDENTIFY key_concepts AND domain_areas
DETERMINE search_strategy (broad/focused/hybrid)
SET optimization_parameters FOR current_context
```

**Query Enhancement**:
- **[[LLM: Expand query with related concepts and synonyms]]**
- **Add contextual tags**: Project phase, domain area, urgency level
- **Include negative terms**: What to specifically exclude
- **Set temporal bounds**: Information recency requirements

### Step 2: Multi-Source Retrieval Execution

**Source Prioritization**:
1. **Primary sources**: Project documentation, recent decisions, active specifications
2. **Secondary sources**: Templates, best practices, historical patterns
3. **Tertiary sources**: External references, general knowledge, examples

**Parallel Retrieval Strategy**:
```
EXECUTE semantic_search ON primary_sources PRIORITY=high
EXECUTE semantic_search ON secondary_sources PRIORITY=medium  
EXECUTE semantic_search ON tertiary_sources PRIORITY=low
MERGE results USING relevance_weighting
```

### Step 3: Result Synthesis and Presentation

**Content Organization**:
- **Group by relevance tier**: Critical (>0.9), Important (0.75-0.9), Contextual (0.6-0.75)
- **Organize by information type**: Decisions, specifications, examples, references
- **Apply temporal ordering**: Most recent first within relevance groups

**Output Formatting**:
```
## Retrieved Context: {{query_context}}

### Critical Information (Relevance >0.9)
{{high_relevance_results}}

### Important Context (Relevance 0.75-0.9)  
{{medium_relevance_results}}

### Additional References (Relevance 0.6-0.75)
{{contextual_references}}

### Search Metadata
- Sources searched: {{source_count}}
- Results found: {{total_results}}
- Processing time: {{retrieval_time}}ms
- Confidence score: {{overall_confidence}}/1.0
```

---

## Advanced Retrieval Features

### 1. Domain-Specific Retrieval

**Architecture Context Retrieval**:
- Focus on technical decisions, system designs, technology choices
- Prioritize recent architectural decisions and their rationales
- Include related patterns, anti-patterns, and constraints

**Product Management Retrieval**:
- Emphasize user stories, requirements, market analysis
- Prioritize recent product decisions and roadmap changes  
- Include user feedback, competitive analysis, success metrics

**Project Context Retrieval**:
- Focus on project status, blockers, decisions, team updates
- Prioritize recent status changes and milestone progress
- Include risk assessments, resource allocations, timeline updates

### 2. Contextual Learning and Adaptation

**Success Pattern Recognition**:
1. **[[LLM: Identify patterns in successful retrieval sessions]]**
2. **Learn domain-specific search preferences** from user interactions
3. **Adapt relevance scoring** based on domain and user feedback
4. **Optimize query expansion** for specific project contexts

**Failure Mode Learning**:
- **Track unsuccessful searches**: Low satisfaction, missing information
- **Analyze gap patterns**: What types of information are hard to find
- **Improve source mapping**: Better categorization and tagging
- **Enhanced query processing**: Better intent recognition and expansion

### 3. Cross-Agent Context Sharing

**Retrieval History Sharing**:
```
WHEN agent_A RETRIEVES context FOR workflow_step_X:
  STORE retrieval_pattern IN shared_context_memory
  ENABLE agent_B TO leverage_similar_patterns FOR related_workflow_steps
```

**Collaborative Filtering**:
- **Learn from agent interactions**: What context proves most useful
- **Share successful search patterns**: Cross-agent learning
- **Optimize for team workflows**: Multi-agent project patterns

---

## Error Handling and Fallbacks

### Retrieval Failure Scenarios

**Insufficient Results** (< 3 relevant items found):
1. **Expand search scope**: Reduce relevance threshold to 0.6
2. **Broaden query terms**: Add synonyms and related concepts  
3. **Search alternate sources**: Expand to tertiary knowledge bases
4. **Suggest alternative approaches**: Manual search, expert consultation

**Low Confidence Results** (average relevance < 0.7):
1. **[[LLM: Highlight uncertainty in retrieved context]]**
2. **Provide confidence scores** for each piece of information
3. **Suggest verification steps**: Expert review, additional sources
4. **Offer manual search guidance**: Where to look for better information

**Performance Issues** (retrieval time > 5000ms):
1. **Switch to cached results**: Use previously retrieved similar context
2. **Reduce search depth**: Focus on high-priority sources only
3. **Implement progressive disclosure**: Show initial results, continue searching
4. **Fallback to basic search**: Simple keyword matching as backup

### Quality Assurance

**Content Validation Checks**:
- **Completeness verification**: Ensure retrieved context addresses the query
- **Accuracy assessment**: Cross-reference with authoritative sources  
- **Freshness validation**: Check information currency and relevance
- **Coherence testing**: Ensure retrieved pieces work together logically

**User Feedback Integration**:
```
AFTER retrieval_session_completion:
  COLLECT user_satisfaction_rating (1-5)
  IDENTIFY most_useful_retrieved_items  
  NOTE any_missing_information_gaps
  UPDATE retrieval_algorithms BASED_ON feedback
```

---

## Integration with Other Context Tools

### Coordination with Context Filtering
- **Pre-filtering integration**: Use context-filtering to scope retrieval sources
- **Post-filtering enhancement**: Apply additional filtering to retrieved results
- **Relevance alignment**: Ensure filtering and retrieval use consistent criteria

### Context Compression Synergy  
- **Retrieve comprehensive content**: Get full context without initial compression
- **Apply targeted compression**: Compress retrieved context for specific use cases
- **Maintain retrieval links**: Keep references to full content for expansion

### Context Validation Partnership
- **Validate retrieved sources**: Ensure information quality and authority
- **Cross-reference checking**: Verify consistency across retrieved items
- **Quality scoring integration**: Use validation scores to improve future retrieval

---

## Success Metrics and Monitoring

### Retrieval Effectiveness Metrics
- **Relevance accuracy**: >85% of retrieved items rated as relevant
- **Coverage completeness**: >90% of information needs addressed
- **Response time performance**: <2000ms average retrieval time
- **User satisfaction**: >4.0/5.0 average usefulness rating

### Learning and Improvement Indicators
- **Query success rate improvement**: Increasing success over time
- **Reduced manual search needs**: Less fallback to manual methods
- **Cross-agent efficiency gains**: Shared learning benefits
- **Domain expertise development**: Better specialized retrieval

---

## Templates and Output Formats

### Standard Retrieval Output Template

```markdown
# Context Retrieval Results

**Query**: {{original_query}}  
**Domain**: {{search_domain}}  
**Confidence**: {{overall_confidence_score}}/1.0  
**Retrieval Time**: {{processing_time}}ms  

## Primary Results (High Relevance)
{{#each high_relevance_items}}
### {{title}} (Score: {{relevance_score}})
{{content_summary}}
**Source**: {{source_location}}  
**Last Updated**: {{modification_date}}  
{{/each}}

## Supporting Context (Medium Relevance)  
{{#each medium_relevance_items}}
- **{{title}}** ({{relevance_score}}): {{brief_summary}}
{{/each}}

## Additional References
{{#each low_relevance_items}}
- {{title}}: {{source_location}}
{{/each}}

---
*Retrieval performed by: {{agent_name}} at {{timestamp}}*
```

This context retrieval system enables planning agents to intelligently find and surface relevant information from large knowledge bases, significantly enhancing their ability to provide contextual, informed assistance for complex workflows and decision-making processes. 