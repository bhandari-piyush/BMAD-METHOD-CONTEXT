# Semantic Search Utility

## Overview
Advanced semantic search utility providing vector embeddings, similarity matching algorithms, and contextual search capabilities for planning agents with rich context features.

**Target Users**: Planning agents with rich context capabilities  
**Purpose**: Enable intelligent semantic search and similarity matching across knowledge bases  
**Complexity**: High - Vector-based search and semantic analysis  

---

## Utility Configuration

```yaml
utility_type: semantic_search
agent_compatibility: planning_only
dependencies:
  utils:
    - context-filtering
    - context-compression
complexity: high
processing_time: 500-2000ms
output_format: ranked_search_results
```

---

## Core Semantic Search Functions

### 1. Vector Embedding Generation

**Purpose**: Convert text content into semantic vector representations for similarity matching

**Embedding Process**:
1. **[[LLM: Generate semantic embeddings for search queries and content]]**
2. **Normalize text input**: {{text_content}} → cleaned, tokenized format
3. **Apply embedding model**: Generate high-dimensional vector representation
4. **Store embedding vectors**: Cache for efficient similarity calculations

**Input Processing**:
```
FUNCTION generate_embeddings(text_content, embedding_type):
  PREPROCESS text_content:
    - Remove formatting artifacts
    - Normalize whitespace and punctuation
    - Extract key semantic elements
    
  APPLY embedding_model:
    - Use contextual word embeddings (e.g., BERT-based)
    - Generate {{embedding_dimensions}}-dimensional vectors
    - Apply domain-specific fine-tuning if available
    
  RETURN normalized_embedding_vector
```

**Embedding Types**:
- **Query embeddings**: Optimized for search queries and questions
- **Content embeddings**: Optimized for document content and knowledge
- **Context embeddings**: Optimized for contextual relationships
- **Domain embeddings**: Specialized for specific knowledge domains

### 2. Similarity Matching Algorithms

**Purpose**: Calculate semantic similarity between query and content embeddings

**Similarity Calculation Methods**:

#### Cosine Similarity (Primary Method)
```
FUNCTION cosine_similarity(vector_a, vector_b):
  dot_product = SUM(vector_a[i] * vector_b[i] for i in range(dimensions))
  magnitude_a = SQRT(SUM(vector_a[i]^2 for i in range(dimensions)))
  magnitude_b = SQRT(SUM(vector_b[i]^2 for i in range(dimensions)))
  
  similarity_score = dot_product / (magnitude_a * magnitude_b)
  RETURN similarity_score  # Range: -1.0 to 1.0
```

#### Euclidean Distance (Secondary Method)
```
FUNCTION euclidean_similarity(vector_a, vector_b):
  distance = SQRT(SUM((vector_a[i] - vector_b[i])^2 for i in range(dimensions)))
  similarity_score = 1.0 / (1.0 + distance)
  RETURN similarity_score  # Range: 0.0 to 1.0
```

#### Contextual Similarity (Advanced)
- **Weighted cosine similarity**: Apply domain-specific weights to dimensions
- **Multi-vector similarity**: Compare query against multiple content embeddings
- **Temporal similarity decay**: Reduce similarity scores based on content age
- **Authority-weighted similarity**: Boost scores for authoritative sources

### 3. Advanced Search Capabilities

**Purpose**: Sophisticated search functionality beyond basic vector matching

**Multi-Modal Search**:
```
FUNCTION semantic_search(query, search_options):
  # Generate query embedding
  query_embedding = generate_embeddings(query, "query")
  
  # Apply search scope filtering
  candidate_content = filter_by_scope(
    content_database, 
    search_options.domain,
    search_options.time_range,
    search_options.content_types
  )
  
  # Calculate similarities
  similarity_scores = []
  FOR each content IN candidate_content:
    content_embedding = get_or_generate_embedding(content)
    similarity = calculate_contextual_similarity(
      query_embedding, 
      content_embedding,
      search_options.similarity_method
    )
    similarity_scores.append((content, similarity))
  
  # Rank and filter results
  ranked_results = SORT(similarity_scores, key=similarity, reverse=True)
  filtered_results = FILTER(ranked_results, similarity > search_options.threshold)
  
  RETURN formatted_search_results(filtered_results)
```

**Fuzzy Search Integration**:
- **Concept expansion**: Include semantically related concepts in search
- **Synonym handling**: Automatically include synonyms and related terms
- **Typo tolerance**: Handle misspellings and variations in query terms
- **Context-aware expansion**: Expand search based on current project context

### 4. Contextual Search Features

**Purpose**: Enhanced search that understands context and intent

**Context-Aware Search**:
```
FUNCTION contextual_search(query, current_context, search_intent):
  # Analyze search intent
  intent_embedding = analyze_search_intent(query, current_context)
  
  # Enhance query with context
  enhanced_query = enhance_query_with_context(
    query, 
    current_context.project_domain,
    current_context.workflow_phase,
    current_context.recent_topics
  )
  
  # Apply contextual weights
  similarity_weights = calculate_contextual_weights(
    search_intent,
    current_context.priority_domains,
    current_context.time_sensitivity
  )
  
  # Execute weighted search
  results = weighted_semantic_search(
    enhanced_query,
    similarity_weights,
    current_context.search_scope
  )
  
  RETURN contextualized_results(results, current_context)
```

**Intent Recognition Patterns**:
- **Information seeking**: "What is...", "How does...", "When should..."
- **Problem solving**: "How to fix...", "Why isn't...", "What went wrong..."
- **Decision support**: "Should I...", "What are options for...", "Compare..."
- **Reference lookup**: "Find examples of...", "Show me...", "Locate..."

---

## Search Optimization Techniques

### 1. Performance Optimization

**Embedding Cache Management**:
```
embedding_cache:
  hot_embeddings:    # Frequently accessed content embeddings
    size_limit: {{hot_cache_size}}MB
    ttl: 24_hours
    
  query_cache:       # Recent query embeddings  
    size_limit: {{query_cache_size}}MB
    ttl: 1_hour
    
  computed_similarities:  # Cached similarity calculations
    size_limit: {{similarity_cache_size}}MB
    ttl: 6_hours
```

**Index Optimization**:
- **Hierarchical indexing**: Organize embeddings by domain and topic
- **Approximate nearest neighbor**: Use efficient ANN algorithms for large datasets
- **Batch processing**: Process multiple queries simultaneously
- **Incremental updates**: Update indexes efficiently as content changes

### 2. Quality Optimization

**Relevance Tuning**:
```
FUNCTION tune_relevance_scoring(search_results, user_feedback):
  FOR each result IN search_results:
    IF result.clicked AND result.useful:
      INCREASE similarity_weights_for_similar_content
    ELIF result.shown BUT NOT result.clicked:
      DECREASE similarity_weights_for_similar_content
      
  UPDATE embedding_model_weights BASED_ON feedback_patterns
  SAVE tuning_parameters FOR future_searches
```

**Domain Adaptation**:
- **Domain-specific embeddings**: Train embeddings on domain-specific content
- **Technical vocabulary handling**: Properly weight technical terms and jargon
- **Acronym and abbreviation expansion**: Handle domain-specific abbreviations
- **Concept hierarchy awareness**: Understand relationships between domain concepts

### 3. Search Result Enhancement

**Result Ranking and Presentation**:
```
FUNCTION enhance_search_results(raw_results, search_context):
  enhanced_results = []
  
  FOR each result IN raw_results:
    # Calculate composite score
    composite_score = (
      result.similarity_score * 0.6 +
      result.freshness_score * 0.2 + 
      result.authority_score * 0.1 +
      result.context_relevance * 0.1
    )
    
    # Generate result summary
    summary = generate_contextual_summary(
      result.content,
      search_context.query,
      search_context.highlight_terms
    )
    
    # Add metadata
    enhanced_result = {
      content: result.content,
      score: composite_score,
      similarity: result.similarity_score,
      summary: summary,
      relevance_explanation: explain_relevance(result, search_context),
      related_content: find_related_content(result, similarity_threshold=0.7)
    }
    
    enhanced_results.append(enhanced_result)
  
  RETURN sort_by_composite_score(enhanced_results)
```

**Content Highlighting**:
- **Semantic highlighting**: Highlight semantically relevant portions, not just keywords
- **Context-aware excerpts**: Show most relevant portions of content for current search
- **Relationship visualization**: Show how results relate to each other
- **Confidence indicators**: Display confidence levels for search results

---

## Integration and Workflow Support

### 1. Context Tool Integration

**Context Filtering Coordination**:
```
FUNCTION integrated_search(query, filter_criteria, context_options):
  # Apply pre-filtering to reduce search space
  filtered_content = apply_context_filtering(
    content_database,
    filter_criteria.domain_scope,
    filter_criteria.time_range,
    filter_criteria.content_types
  )
  
  # Execute semantic search on filtered content
  search_results = semantic_search(
    query,
    filtered_content,
    context_options.similarity_threshold
  )
  
  # Apply post-search filtering for refinement
  refined_results = apply_post_search_filtering(
    search_results,
    filter_criteria.quality_threshold,
    filter_criteria.relevance_filters
  )
  
  RETURN refined_results
```

**Context Compression Synergy**:
- **Search compressed content**: Ability to search through compressed archives
- **Progressive detail retrieval**: Get summaries first, full content on demand
- **Compression-aware ranking**: Account for information loss in compressed content
- **Decompression on demand**: Automatically decompress relevant archived content

### 2. Multi-Agent Search Coordination

**Shared Search Learning**:
```
shared_search_intelligence:
  query_patterns:
    successful_queries: # Queries that led to useful results
      - query_text
      - context_domain  
      - result_quality_score
      - user_satisfaction
      
  content_preferences:
    by_agent_type:
      architect: [technical_docs, design_patterns, system_specs]
      pm: [requirements, user_stories, project_status]
      ux: [user_research, design_guidelines, usability_patterns]
      
  search_optimization:
    domain_weights: # Learned weights for different domains
    query_expansions: # Successful query enhancement patterns
    result_preferences: # Agent-specific result ranking preferences
```

**Cross-Agent Search Sharing**:
- **Search result broadcasting**: Share useful results with relevant agents
- **Query suggestion sharing**: Suggest related searches based on agent interactions
- **Collaborative filtering**: Improve search based on what other agents found useful
- **Knowledge gap identification**: Identify areas where search frequently fails

---

## Error Handling and Fallbacks

### Search Failure Recovery

**No Results Found**:
```
IF search_results.length == 0:
  # Try progressively broader searches
  ATTEMPT expanded_query_search(original_query + domain_synonyms)
  IF still_no_results:
    ATTEMPT fuzzy_keyword_search(extract_keywords(original_query))
    IF still_no_results:
      RETURN no_results_guidance(
        suggested_alternative_searches,
        manual_search_recommendations,
        expert_consultation_options
      )
```

**Low Quality Results**:
```
IF average_similarity_score < quality_threshold:
  # Analyze search quality issues
  quality_issues = analyze_search_problems(query, results)
  
  # Apply appropriate fixes
  IF quality_issues.includes("ambiguous_query"):
    SUGGEST query_clarification_options
  ELIF quality_issues.includes("domain_mismatch"):
    SUGGEST domain_specific_search_adjustments
  ELIF quality_issues.includes("insufficient_content"):
    SUGGEST content_expansion_or_alternative_sources
```

**Performance Issues**:
- **Timeout handling**: Return partial results if search takes too long
- **Memory pressure**: Switch to less memory-intensive search methods
- **Index corruption**: Fall back to simpler search mechanisms
- **Cache invalidation**: Handle cache corruption gracefully

---

## Success Metrics and Monitoring

### Search Effectiveness Metrics
- **Precision**: Relevant results / Total results returned (target: >80%)
- **Recall**: Relevant results found / Total relevant results available (target: >70%)  
- **Response time**: Average search completion time (target: <2000ms)
- **User satisfaction**: Rating of search result usefulness (target: >4.0/5.0)

### Learning and Improvement Metrics
- **Query success rate**: Percentage of searches that find useful results (target: >85%)
- **Search refinement rate**: How often users need to refine searches (target: <30%)
- **Cross-agent search reuse**: How often agents benefit from each other's searches
- **Domain expertise development**: Improvement in domain-specific search accuracy over time

---

## Output Templates

### Search Results Template

```markdown
# Semantic Search Results

**Query**: {{search_query}}  
**Domain Scope**: {{search_domain}}  
**Results Found**: {{total_results}} (showing top {{displayed_results}})  
**Search Time**: {{processing_time}}ms  
**Confidence**: {{overall_confidence}}/1.0  

## Primary Results (Similarity >0.8)
{{#each high_similarity_results}}
### {{title}} ({{similarity_score}})
{{contextual_summary}}
**Source**: {{content_source}} | **Updated**: {{last_modified}}  
**Relevance**: {{relevance_explanation}}
{{/each}}

## Secondary Results (Similarity 0.6-0.8)
{{#each medium_similarity_results}}
- **{{title}}** ({{similarity_score}}): {{brief_summary}}
{{/each}}

## Related Searches
{{#each suggested_related_queries}}
- {{query_text}} ({{relevance_reason}})
{{/each}}

---
*Search powered by semantic embeddings | Agent: {{agent_name}}*
```

This semantic search utility provides planning agents with sophisticated search capabilities that go far beyond keyword matching, enabling intelligent discovery of relevant information through semantic understanding and contextual awareness. 