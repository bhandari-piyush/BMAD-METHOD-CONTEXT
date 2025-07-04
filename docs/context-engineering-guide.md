# BMAD Context Engineering Guide

**Master AI Context Management for Optimal Development Workflows**

## Table of Contents

1. [Overview](#overview)
2. [Core Concepts](#core-concepts)
3. [Context Tools Reference](#context-tools-reference)
4. [Real-World Scenarios](#real-world-scenarios)
5. [Advanced Techniques](#advanced-techniques)
6. [Troubleshooting](#troubleshooting)
7. [Performance Optimization](#performance-optimization)
8. [Best Practices](#best-practices)

## Overview

Context Engineering in BMAD v4+ represents a sophisticated approach to AI collaboration that automatically manages information flow between agents while maintaining optimal performance for each agent type.

### Why Context Engineering Matters

- **Efficiency**: Reduces token usage by up to 60% while maintaining information quality
- **Focus**: Keeps development agents lean for faster coding cycles
- **Intelligence**: Enables planning agents to access comprehensive context for better decisions
- **Collaboration**: Seamless information handoff between specialized agents
- **Quality**: Ensures relevant, validated information reaches the right agents

### Agent Classification

**💻 Development Agents (Lean Context - 2000 tokens)**
- `dev` - Optimized for fast, focused implementation

**📱 Planning Agents (Rich Context - 8000 tokens)**
- `pm`, `architect`, `analyst`, `ux-expert`, `qa`, `sm`, `po` - Full context for strategic decisions

**🎭 Universal Orchestrator**
- `bmad-orchestrator` - Adaptive context based on current task

## Core Concepts

### Context Compression Ratios

Context engineering uses intelligent compression to maintain information quality:

- **Development Context**: 90% compression (aggressive filtering for code focus)
- **Planning Context**: 70% compression (balanced detail for analysis)
- **Universal Context**: 80% compression (moderate filtering for flexibility)

### Information Prioritization

Context tools prioritize information based on:

1. **Recency** - Recent decisions and changes take priority
2. **Relevance** - Agent-specific information filtering
3. **Impact** - Critical decisions and requirements preserved
4. **Dependency** - Related information bundled together

### Automatic vs Manual Context Management

**Automatic (Default)**:
- Triggered when switching between agents
- Uses predefined optimization rules
- Maintains agent-specific token limits
- No user intervention required

**Manual (Advanced)**:
- Explicit context optimization commands
- Custom compression parameters
- Targeted context validation
- Debugging and troubleshooting

## Context Tools Reference

### Universal Tasks (All Agents)

#### `context-optimization`
**Purpose**: Compress and optimize current context for better performance
**When to Use**: Large documents, performance issues, focus problems

```bash
*task context-optimization
# Optional parameters:
# --target-ratio=0.8  (compression ratio)
# --focus="implementation"  (specific focus area)
# --preserve="requirements"  (sections to preserve)
```

**Output**:
- Optimized context summary
- Compression ratio achieved
- Key information preserved
- Items filtered out

#### `context-handoff`
**Purpose**: Transfer information between agents with optimization
**When to Use**: Agent switching, cross-functional collaboration

```bash
*task context-handoff
# Automatically optimizes for target agent type
# Planning → Dev: Heavy compression, code focus
# Dev → Planning: Detail expansion, context restoration
```

**Output**:
- Agent-optimized context summary
- Handoff quality score
- Information transfer log
- Validation results

#### `context-validation`
**Purpose**: Verify context quality and security
**When to Use**: Sensitive information, quality assurance, troubleshooting

```bash
*task context-validation
# Checks: completeness, relevance, security, accuracy
```

**Output**:
- Validation report
- Quality metrics
- Security clearance status
- Recommendations for improvement

### Planning Agent Tools (Rich Context Only)

#### `context-retrieval`
**Purpose**: Recover detailed context from compressed summaries
**When to Use**: Need historical detail, comprehensive analysis

```bash
*task context-retrieval --topic="architecture decisions"
```

#### `context-memory-management`
**Purpose**: Long-term context storage and retrieval
**When to Use**: Project continuity, knowledge preservation

```bash
*task context-memory-management --action="store" --tag="sprint-1"
```

### Utility Components

#### `context-compression`
**Purpose**: Core compression algorithms
**Features**: Semantic preservation, relevance scoring, intelligent summarization

#### `context-filtering`
**Purpose**: Relevance-based content filtering
**Features**: Agent-specific filters, priority ranking, noise reduction

## Real-World Scenarios

### Scenario 1: Large Enterprise Application

**Challenge**: Complex PRD (15,000 tokens) + Architecture (12,000 tokens) + Multiple agents

**Solution**:
```bash
# 1. Analyst completes market research (Large document)
*agent analyst
*task create-doc  # Creates 8,000 token market analysis

# 2. PM receives compressed market insights
*agent pm
*task context-handoff  # Gets 2,000 token summary for PRD creation
*task create-doc  # Builds PRD with focused market data

# 3. Architect gets PRD essentials
*agent architect  
*task context-handoff  # Receives 3,000 token PRD summary
*task create-doc  # Creates technical architecture

# 4. Dev gets lean implementation context
*agent dev
*task context-handoff  # Gets 1,500 token implementation guide
# Ready for fast development cycles
```

**Benefits**:
- 70% reduction in context size across workflow
- Maintained information quality at each stage
- Faster agent response times
- Clear decision traceability

### Scenario 2: Brownfield Legacy Integration

**Challenge**: Existing codebase analysis + New feature requirements + Multiple technical constraints

**Solution**:
```bash
# 1. Architect analyzes existing system
*agent architect
*task context-optimization --focus="legacy-integration"
# Compresses codebase analysis for architecture design

# 2. PM receives architecture constraints summary
*agent pm
*task context-handoff
# Gets technical limitations for product planning

# 3. Dev receives focused implementation context
*agent dev
*task context-handoff
# Gets only relevant legacy interfaces and new requirements
```

### Scenario 3: Multi-Sprint Project Continuity

**Challenge**: Maintaining context across sprints while avoiding information overload

**Solution**:
```bash
# End of Sprint 1: Store context
*agent sm
*task context-memory-management --action="store" --tag="sprint-1-complete"

# Start of Sprint 2: Retrieve relevant context
*agent sm  
*task context-memory-management --action="retrieve" --tag="sprint-1-complete"
*task context-optimization --preserve="user-feedback,architecture-decisions"

# Continue with optimized context for Sprint 2
```

### Scenario 4: Cross-Functional Design Validation

**Challenge**: UX decisions need technical validation while maintaining design focus

**Solution**:
```bash
# 1. UX Expert creates design system
*agent ux-expert
*task create-doc  # Comprehensive design guidelines

# 2. Architect receives design-focused technical context  
*agent architect
*task context-handoff
# Gets design requirements + technical constraints only

# 3. Architect validates technical feasibility
*task create-doc  # Technical validation with design considerations

# 4. UX Expert receives technical feedback summary
*agent ux-expert
*task context-handoff  
# Gets actionable technical feedback without implementation details
```

## Advanced Techniques

### Custom Compression Parameters

```bash
# High compression for performance
*task context-optimization --target-ratio=0.9 --focus="performance"

# Preserve specific content types
*task context-optimization --preserve="user-stories,acceptance-criteria"

# Agent-specific optimization
*task context-optimization --target-agent="dev" --focus="implementation"
```

### Context Quality Monitoring

```bash
# Check context health
*task context-validation --detailed

# Monitor compression effectiveness
*status --context-metrics

# Audit information flow
*task context-validation --audit-trail
```

### Selective Context Restoration

```bash
# Restore specific topic details
*task context-retrieval --topic="security-requirements" --detail-level="high"

# Recover filtered information
*task context-retrieval --restore="filtered-out" --reason="design-change"
```

## Troubleshooting

### Common Issues

#### Problem: Agent responses are too generic or unfocused

**Symptoms**:
- Agent asks for information you've already provided
- Responses don't reference previous decisions
- Generic answers to specific questions

**Solution**:
```bash
# Check current context state
*status --context-details

# Validate context quality
*task context-validation

# If issues found, optimize context
*task context-optimization --focus="recent-decisions"
```

#### Problem: Important information seems to be lost

**Symptoms**:
- Agent doesn't remember key requirements
- Previous design decisions ignored
- Inconsistent responses

**Solution**:
```bash
# Retrieve potentially filtered information
*task context-retrieval --topic="[specific topic]" --include-filtered

# Adjust compression to preserve more detail
*task context-optimization --target-ratio=0.6 --preserve="requirements,decisions"

# Validate information completeness
*task context-validation --check-completeness
```

#### Problem: Context handoff between agents fails

**Symptoms**:
- Information doesn't transfer properly
- Agent seems confused about project state
- Handoff summaries seem incomplete

**Solution**:
```bash
# Manual context handoff with validation
*task context-handoff --validate --detailed

# Check agent compatibility
*task context-validation --agent-compatibility

# If issues persist, use step-by-step handoff
*task context-optimization  # First optimize
*task context-validation    # Then validate
*task context-handoff      # Finally transfer
```

#### Problem: Performance is slow despite context optimization

**Symptoms**:
- Agent responses take longer than expected
- Context size seems large despite compression
- Memory usage issues

**Solution**:
```bash
# Check actual context size
*status --context-size

# Aggressive optimization
*task context-optimization --target-ratio=0.9 --aggressive

# Clear unnecessary context
*task context-filtering --remove-stale --threshold=7days
```

### Debugging Commands

```bash
# Show detailed context state
*status --context-debug

# Analyze context composition
*task context-validation --analyze-composition

# Show compression history
*task context-optimization --show-history

# Audit recent context operations
*task context-validation --audit-recent --days=3
```

## Performance Optimization

### Token Usage Guidelines

**Development Workflow Targets**:
- Dev Agent: <2000 tokens (optimal: 1500-1800)
- Context Handoff: <500 tokens overhead
- Total Development Context: <2500 tokens

**Planning Workflow Targets**:
- Planning Agents: <8000 tokens (optimal: 6000-7500)
- Cross-agent handoff: <1000 tokens overhead
- Total Planning Context: <9000 tokens

### Optimization Strategies

#### Strategy 1: Layered Context Architecture
```bash
# Base layer: Core requirements (always preserved)
*task context-optimization --preserve="core-requirements" --layer="base"

# Working layer: Current task context (regularly optimized)
*task context-optimization --focus="current-task" --layer="working"

# Archive layer: Historical context (compressed heavily)
*task context-optimization --target-ratio=0.95 --layer="archive"
```

#### Strategy 2: Role-Based Context Profiles
```bash
# Developer profile: Code-focused, minimal business context
*task context-optimization --profile="developer"

# Architect profile: Technical decisions, system constraints
*task context-optimization --profile="architect"

# PM profile: Business requirements, user needs, priorities
*task context-optimization --profile="product-manager"
```

#### Strategy 3: Dynamic Context Scaling
```bash
# Scale context based on task complexity
*task context-optimization --auto-scale --task-complexity="high"

# Adjust context for current development phase
*task context-optimization --phase="implementation" --focus="code"
```

## Best Practices

### For Development Teams

1. **Use automatic context handoff** for agent switching
2. **Keep dev agents lean** - under 2000 tokens always
3. **Optimize context regularly** during long development sessions
4. **Validate context quality** before critical decisions
5. **Use context memory** for sprint continuity

### For Planning Teams

1. **Leverage rich context** for comprehensive analysis
2. **Use context retrieval** when detailed history is needed
3. **Validate handoffs** between functional areas
4. **Preserve key decisions** through context optimization
5. **Monitor context quality** with regular validation

### For Project Management

1. **Track context health** across team workflows
2. **Establish context standards** for your organization
3. **Train teams** on context optimization techniques
4. **Monitor performance metrics** for context efficiency
5. **Implement context governance** for sensitive projects

### Universal Guidelines

- **Always validate context** before major decisions
- **Use manual optimization** when automatic isn't sufficient
- **Monitor token usage** to maintain performance
- **Preserve critical information** through compression settings
- **Test context handoffs** in complex workflows

---

## Quick Reference Card

### Essential Commands
```bash
*task context-optimization     # Optimize current context
*task context-handoff         # Transfer between agents  
*task context-validation      # Check context quality
*status --context-details     # Show context state
```

### Emergency Context Recovery
```bash
*task context-retrieval --restore-all --detail-level="high"
*task context-validation --check-completeness --fix-issues
```

### Performance Troubleshooting
```bash
*status --context-size
*task context-optimization --aggressive --target-ratio=0.9
*task context-filtering --remove-stale
```

---

*For additional support with context engineering, visit our [Discord Community](https://discord.gg/g6ypHytrCB) or check the [main documentation](../README.md).* 