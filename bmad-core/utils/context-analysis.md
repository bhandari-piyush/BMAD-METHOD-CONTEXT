# Context Analysis Utility

## Overview
Advanced context analysis utility providing context quality assessment, relevance scoring algorithms, freshness validation, and comprehensive quality metrics tracking for planning agents.

**Target Users**: Planning agents with rich context capabilities  
**Purpose**: Enable intelligent assessment and optimization of context quality and relevance  
**Complexity**: High - Multi-dimensional quality analysis and scoring  

---

## Utility Configuration

```yaml
utility_type: context_analysis
agent_compatibility: planning_only
dependencies:
  utils:
    - context-filtering
    - context-compression
complexity: high
processing_time: 300-1500ms
output_format: quality_analysis_report
```

---

## Core Analysis Functions

### 1. Context Quality Assessment

**Purpose**: Comprehensive evaluation of context information quality across multiple dimensions

**Quality Dimensions**:
```yaml
quality_metrics:
  accuracy: 0.0-1.0      # Factual correctness and reliability
  completeness: 0.0-1.0  # Information sufficiency and coverage
  relevance: 0.0-1.0     # Current applicability and usefulness
  freshness: 0.0-1.0     # Information currency and recency
  coherence: 0.0-1.0     # Internal consistency and logical flow
  authority: 0.0-1.0     # Source credibility and trustworthiness
```

**Quality Assessment Process**:
```
FUNCTION assess_context_quality(context_content, assessment_criteria):
  quality_scores = {}
  
  # Accuracy Assessment
  quality_scores.accuracy = evaluate_factual_accuracy(
    context_content,
    assessment_criteria.reference_sources,
    assessment_criteria.fact_checking_rules
  )
  
  # Completeness Assessment  
  quality_scores.completeness = evaluate_information_completeness(
    context_content,
    assessment_criteria.required_elements,
    assessment_criteria.coverage_expectations
  )
  
  # Relevance Assessment
  quality_scores.relevance = evaluate_current_relevance(
    context_content,
    assessment_criteria.current_context,
    assessment_criteria.use_case_requirements
  )
  
  # Freshness Assessment
  quality_scores.freshness = evaluate_information_freshness(
    context_content.timestamp,
    context_content.update_frequency,
    assessment_criteria.freshness_requirements
  )
  
  # Coherence Assessment
  quality_scores.coherence = evaluate_internal_coherence(
    context_content,
    assessment_criteria.logical_consistency_rules
  )
  
  # Authority Assessment
  quality_scores.authority = evaluate_source_authority(
    context_content.source_metadata,
    assessment_criteria.authority_criteria
  )
  
  # Calculate composite quality score
  composite_score = calculate_weighted_quality_score(
    quality_scores,
    assessment_criteria.dimension_weights
  )
  
  RETURN {
    individual_scores: quality_scores,
    composite_score: composite_score,
    quality_issues: identify_quality_issues(quality_scores),
    improvement_recommendations: suggest_quality_improvements(quality_scores)
  }
```

### 2. Relevance Scoring Algorithms

**Purpose**: Sophisticated algorithms to determine context relevance for specific use cases

**Multi-Factor Relevance Scoring**:
```
FUNCTION calculate_relevance_score(context, target_use_case, current_situation):
  relevance_factors = {}
  
  # Semantic Relevance (40% weight)
  relevance_factors.semantic = calculate_semantic_similarity(
    context.content_embedding,
    target_use_case.requirement_embedding
  )
  
  # Temporal Relevance (20% weight)  
  relevance_factors.temporal = calculate_temporal_relevance(
    context.creation_date,
    context.last_update,
    target_use_case.time_sensitivity
  )
  
  # Contextual Relevance (25% weight)
  relevance_factors.contextual = calculate_contextual_fit(
    context.domain_tags,
    context.project_phase,
    current_situation.active_domains,
    current_situation.workflow_phase
  )
  
  # Usage Pattern Relevance (15% weight)
  relevance_factors.usage_pattern = calculate_usage_relevance(
    context.historical_usage,
    target_use_case.agent_type,
    target_use_case.task_category
  )
  
  # Calculate weighted relevance score
  relevance_score = (
    relevance_factors.semantic * 0.40 +
    relevance_factors.temporal * 0.20 +
    relevance_factors.contextual * 0.25 +
    relevance_factors.usage_pattern * 0.15
  )
  
  RETURN {
    overall_relevance: relevance_score,
    factor_breakdown: relevance_factors,
    relevance_explanation: generate_relevance_explanation(relevance_factors),
    confidence_level: calculate_relevance_confidence(relevance_factors)
  }
```

### 3. Freshness Validation

**Purpose**: Evaluate and score information currency and temporal relevance

**Freshness Scoring Framework**:
```
FUNCTION evaluate_information_freshness(content_metadata, freshness_requirements):
  freshness_scores = {}
  
  # Absolute Age Score
  content_age_days = (current_date - content_metadata.last_update).days
  age_score = calculate_age_decay_score(
    content_age_days,
    freshness_requirements.half_life_days
  )
  
  # Update Frequency Score  
  update_frequency_score = evaluate_update_pattern(
    content_metadata.update_history,
    freshness_requirements.expected_update_frequency
  )
  
  # Domain-Specific Freshness
  domain_freshness_score = apply_domain_freshness_rules(
    content_metadata.domain,
    content_age_days,
    freshness_requirements.domain_specific_rules
  )
  
  # Source Freshness Reliability
  source_reliability_score = evaluate_source_freshness_reliability(
    content_metadata.source,
    content_metadata.source_update_patterns
  )
  
  # Calculate composite freshness score
  composite_freshness = (
    age_score * 0.4 +
    update_frequency_score * 0.3 +
    domain_freshness_score * 0.2 +
    source_reliability_score * 0.1
  )
  
  RETURN {
    freshness_score: composite_freshness,
    age_assessment: categorize_content_age(content_age_days),
    update_status: assess_update_currency(content_metadata),
    freshness_warnings: identify_freshness_issues(composite_freshness),
    refresh_recommendations: suggest_refresh_actions(composite_freshness)
  }
```

### 4. Quality Metrics Tracking

**Purpose**: Continuous monitoring and improvement of context quality over time

**Metrics Collection Framework**:
```
context_quality_tracking:
  real_time_metrics:
    - quality_score_distribution
    - relevance_accuracy_rate  
    - freshness_compliance_rate
    - user_satisfaction_scores
    
  trend_analysis:
    - quality_improvement_over_time
    - domain_specific_quality_patterns
    - agent_usage_impact_on_quality
    - context_lifecycle_quality_changes
    
  comparative_analysis:
    - quality_by_content_source
    - quality_by_context_type
    - quality_by_agent_interaction_patterns
    - quality_correlation_with_outcomes
```

---

## Advanced Analysis Features

### 1. Quality-Driven Context Operations

**Quality-Based Context Filtering**:
```
FUNCTION filter_by_quality_criteria(context_pool, quality_requirements):
  filtered_contexts = []
  
  FOR each context IN context_pool:
    quality_assessment = assess_context_quality(context)
    
    IF meets_quality_requirements(quality_assessment, quality_requirements):
      # Add quality metadata to context
      context.quality_metadata = quality_assessment
      filtered_contexts.append(context)
    ELSE:
      # Log quality failure for improvement
      log_quality_filter_rejection(context, quality_assessment, quality_requirements)
  
  # Sort by quality score
  RETURN sort_by_composite_quality(filtered_contexts)
```

### 2. Predictive Quality Assessment

**Purpose**: Predict future quality issues and optimization opportunities

**Quality Prediction Models**:
```
FUNCTION predict_quality_issues(context_metadata, usage_patterns, external_factors):
  predictions = {}
  
  # Freshness degradation prediction
  predictions.freshness_decline = predict_freshness_degradation(
    context_metadata.last_update,
    context_metadata.content_type,
    external_factors.domain_change_rate
  )
  
  # Relevance decay prediction
  predictions.relevance_decay = predict_relevance_decay(
    context_metadata.current_relevance,
    usage_patterns.access_frequency,
    external_factors.context_evolution_rate
  )
  
  # Quality intervention recommendations
  predictions.intervention_timing = calculate_optimal_intervention_timing(
    predictions.freshness_decline,
    predictions.relevance_decay,
    context_metadata.maintenance_cost
  )
  
  RETURN predictions
```

---

## Error Handling and Quality Assurance

### Analysis Failure Recovery

**Incomplete Analysis Handling**:
```
IF quality_analysis_fails_partially:
  # Identify which dimensions were successfully analyzed
  completed_dimensions = identify_completed_analysis_dimensions()
  
  # Provide partial quality assessment
  partial_assessment = {
    available_scores: completed_dimensions,
    missing_dimensions: identify_failed_dimensions(),
    confidence_adjustment: calculate_confidence_reduction(),
    analysis_limitations: document_analysis_limitations()
  }
  
  # Attempt alternative analysis methods
  alternative_results = attempt_fallback_analysis_methods()
  
  RETURN merge_partial_and_alternative_results(partial_assessment, alternative_results)
```

---

## Success Metrics and Monitoring

### Analysis Effectiveness Metrics
- **Analysis accuracy**: Correlation between predicted and actual quality outcomes (target: >85%)
- **Coverage completeness**: Percentage of quality dimensions successfully analyzed (target: >95%)
- **Analysis consistency**: Reproducibility of analysis results (target: >90%)
- **Prediction accuracy**: Accuracy of quality predictions over time (target: >75%)

---

## Output Templates

### Quality Analysis Report Template

```markdown
# Context Quality Analysis Report

**Context ID**: {{context_identifier}}  
**Analysis Date**: {{analysis_timestamp}}  
**Analyst**: {{analyzing_agent}}  
**Analysis Type**: {{analysis_scope}} (full/partial/focused)  

## Quality Score Summary
**Composite Quality Score**: {{composite_score}}/1.0 ({{quality_grade}})

### Individual Dimension Scores
- **Accuracy**: {{accuracy_score}}/1.0 {{accuracy_status_icon}}
- **Completeness**: {{completeness_score}}/1.0 {{completeness_status_icon}}  
- **Relevance**: {{relevance_score}}/1.0 {{relevance_status_icon}}
- **Freshness**: {{freshness_score}}/1.0 {{freshness_status_icon}}
- **Coherence**: {{coherence_score}}/1.0 {{coherence_status_icon}}
- **Authority**: {{authority_score}}/1.0 {{authority_status_icon}}

## Quality Assessment Details

### Strengths Identified
{{#each quality_strengths}}
- **{{dimension}}**: {{strength_description}} (Score: {{strength_score}})
{{/each}}

### Issues and Concerns  
{{#each quality_issues}}
- **{{dimension}}**: {{issue_description}} (Impact: {{impact_level}})
{{/each}}

## Improvement Recommendations
{{#each recommendations}}
### {{priority_level}} Priority: {{recommendation_title}}
{{recommendation_description}}
**Expected Impact**: {{expected_improvement}}  
**Effort Required**: {{effort_estimate}}
{{/each}}

---
*Analysis performed by: {{agent_name}} | Context Analysis Utility v{{version}}*
```

This context analysis utility provides planning agents with sophisticated capabilities to assess, monitor, and optimize context quality, enabling data-driven decisions about context usage and improvement. 