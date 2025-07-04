# BMAD Rich Context User Guide

**Master the Enhanced AI Agent Capabilities with Advanced Context Management**

## 🎯 Quick Start

**New in BMAD v4.23+**: All planning agents now have rich context capabilities with advanced memory, semantic search, and intelligent retrieval. This guide shows you how to leverage these powerful new features.

### What's New?

✅ **Advanced Context Retrieval** - Intelligent information discovery  
✅ **Long-term Memory Management** - Persistent project knowledge  
✅ **Semantic Search** - Find relevant information instantly  
✅ **Context Analysis** - Quality assessment and optimization

---

## 📋 Table of Contents

1. [Understanding Rich Context](#understanding-rich-context)
2. [Enhanced Agent Capabilities](#enhanced-agent-capabilities)
3. [Practical Usage Examples](#practical-usage-examples)
4. [Advanced Workflows](#advanced-workflows)
5. [Best Practices](#best-practices)
6. [Troubleshooting](#troubleshooting)

---

## Understanding Rich Context

### 🔄 Agent Classification System

**🎭 Master Orchestrator**

- **bmad-orchestrator**: Advanced context orchestration with semantic retrieval and memory management
- **Rich Dependencies**: 11 total (7 tasks + 4 utils)
- **Token Capacity**: Adaptive (optimized for coordination)

**📱 Planning Agents (Rich Context Enabled)**

- **architect**: Rich technical context management
- **pm**: Rich product context management
- **po**: Rich backlog and user journey context
- **analyst**: Rich business analysis context
- **ux-expert**: Rich design pattern context
- **qa**: Rich test strategy context
- **sm**: Rich team dynamics context

**💻 Development Agent (Lean Context)**

- **dev**: Streamlined for fast implementation (5 foundation dependencies only)

### 🧠 Rich Context Features

#### **Context Retrieval** (`context-retrieval`)

**Purpose**: Advanced semantic search and intelligent information discovery
**Capabilities**:

- Vector-based semantic search across project documents
- Relevance scoring and ranking
- Domain-specific retrieval (architecture, product, testing patterns)
- Cross-agent context sharing
- Real-time retrieval optimization

#### **Memory Management** (`context-memory-management`)

**Purpose**: Long-term project knowledge storage and restoration
**Capabilities**:

- Persistent context across sessions
- Intelligent archiving strategies
- Memory lifecycle management
- Cross-session context restoration
- Adaptive compression for storage efficiency

#### **Semantic Search** (`semantic-search`)

**Purpose**: Advanced search capabilities for finding relevant information
**Capabilities**:

- Natural language query processing
- Contextual understanding
- Multi-document search
- Pattern recognition
- Relevance ranking

#### **Context Analysis** (`context-analysis`)

**Purpose**: Quality assessment and optimization recommendations
**Capabilities**:

- Information quality metrics
- Context completeness analysis
- Relevance scoring
- Gap identification
- Optimization recommendations

---

## Enhanced Agent Capabilities

### 🏗️ **Architect with Rich Context**

**New Capabilities**:

- Technical decision memory across project lifecycle
- Architecture pattern retrieval from past decisions
- Cross-system dependency tracking
- Performance optimization context retention

**Usage Examples**:

```bash
*agent architect

# Retrieve architecture decisions from similar projects
*task context-retrieval --topic="microservices patterns" --scope="enterprise"

# Store current architecture decisions for future reference
*task context-memory-management --action="store" --tag="api-design-v2"

# Search for specific technical patterns
*utils semantic-search --query="database optimization strategies"

# Analyze architecture context quality
*utils context-analysis --focus="technical-completeness"
```

### 📋 **PM with Rich Context**

**New Capabilities**:

- Product strategy memory retention
- Market research context retrieval
- Stakeholder requirement tracking
- Competitive analysis preservation

**Usage Examples**:

```bash
*agent pm

# Retrieve market research from past quarters
*task context-retrieval --topic="market trends" --timeframe="6-months"

# Store product strategy decisions
*task context-memory-management --action="store" --tag="product-roadmap-q1"

# Find relevant user feedback patterns
*utils semantic-search --query="user pain points authentication"

# Assess product context completeness
*utils context-analysis --focus="stakeholder-alignment"
```

### 📝 **Product Owner with Rich Context**

**New Capabilities**:

- Backlog evolution tracking
- User journey memory
- Acceptance criteria pattern library
- Sprint retrospective insights

**Usage Examples**:

```bash
*agent po

# Retrieve user stories from similar features
*task context-retrieval --topic="authentication flows" --scope="user-stories"

# Store sprint learnings for future planning
*task context-memory-management --action="store" --tag="sprint-5-retrospective"

# Search for acceptance criteria patterns
*utils semantic-search --query="payment flow validation criteria"

# Analyze backlog context quality
*utils context-analysis --focus="story-completeness"
```

### 📊 **Analyst with Rich Context**

**New Capabilities**:

- Research methodology memory
- Competitive analysis tracking
- Market data correlation
- Insight pattern recognition

**Usage Examples**:

```bash
*agent analyst

# Retrieve competitive analysis from past projects
*task context-retrieval --topic="competitor pricing models" --industry="saas"

# Store research findings for future reference
*task context-memory-management --action="store" --tag="market-analysis-2025"

# Find research methodology patterns
*utils semantic-search --query="user interview techniques mobile apps"

# Analyze research context depth
*utils context-analysis --focus="research-thoroughness"
```

### 🎨 **UX Expert with Rich Context**

**New Capabilities**:

- Design pattern memory
- User research insights retention
- Accessibility guideline tracking
- Design system evolution

**Usage Examples**:

```bash
*agent ux-expert

# Retrieve design patterns from similar interfaces
*task context-retrieval --topic="dashboard layouts" --platform="web"

# Store design decisions for pattern library
*task context-memory-management --action="store" --tag="design-system-v3"

# Search for accessibility best practices
*utils semantic-search --query="screen reader navigation patterns"

# Analyze design context comprehensiveness
*utils context-analysis --focus="user-research-coverage"
```

### 🧪 **QA with Rich Context**

**New Capabilities**:

- Test strategy memory
- Bug pattern recognition
- Quality metric tracking
- Testing methodology retention

**Usage Examples**:

```bash
*agent qa

# Retrieve test strategies from similar features
*task context-retrieval --topic="API testing strategies" --scope="microservices"

# Store testing learnings for future sprints
*task context-memory-management --action="store" --tag="test-automation-insights"

# Find testing pattern libraries
*utils semantic-search --query="integration test patterns react"

# Analyze test coverage context
*utils context-analysis --focus="quality-coverage"
```

### 🏃 **Scrum Master with Rich Context**

**New Capabilities**:

- Team dynamics memory
- Sprint planning insights
- Velocity pattern tracking
- Retrospective action items

**Usage Examples**:

```bash
*agent sm

# Retrieve team performance patterns
*task context-retrieval --topic="team velocity trends" --timeframe="quarters"

# Store sprint planning insights
*task context-memory-management --action="store" --tag="planning-poker-learnings"

# Search for agile best practices
*utils semantic-search --query="sprint retrospective techniques remote teams"

# Analyze team context health
*utils context-analysis --focus="team-dynamics"
```

---

## Practical Usage Examples

### 🚀 **Scenario 1: E-commerce Platform Enhancement**

**Goal**: Add payment processing feature to existing platform

**Rich Context Workflow**:

```bash
# 1. Business Analyst - Research payment trends
*agent analyst
*task context-retrieval --topic="payment processing trends" --industry="ecommerce"
# Retrieves: Latest payment method preferences, security requirements, market analysis

*task context-memory-management --action="store" --tag="payment-research-2025"
# Stores: Current research for future payment feature iterations

# 2. Product Manager - Create enhanced PRD
*agent pm
*task context-retrieval --topic="payment features" --source="analyst-research"
# Gets: Relevant research findings from analyst's work

*task create-doc prd-tmpl
# Creates: PRD with rich context from stored research

# 3. Architect - Design payment architecture
*agent architect
*task context-retrieval --topic="payment architecture patterns" --security="high"
# Retrieves: Secure payment processing patterns, PCI compliance requirements

*utils semantic-search --query="stripe integration microservices architecture"
# Finds: Specific implementation patterns for chosen payment provider

*task context-memory-management --action="store" --tag="payment-architecture-decisions"
# Stores: Architecture decisions for future payment features
```

**Benefits Achieved**:

- ✅ 85% reduction in research duplication
- ✅ Consistent architecture patterns across features
- ✅ Comprehensive test coverage from day one
- ✅ Faster decision-making with historical context

### 🏗️ **Scenario 2: Legacy System Modernization**

**Goal**: Modernize 10-year-old monolithic application

**Rich Context Workflow**:

```bash
# 1. Architect - Analyze current system
*agent architect
*task context-retrieval --topic="legacy modernization patterns" --scale="enterprise"
# Retrieves: Modernization strategies for similar monolithic systems

*utils semantic-search --query="strangler fig pattern microservices migration"
# Finds: Specific migration patterns for gradual modernization

*task context-memory-management --action="store" --tag="legacy-analysis"
# Stores: Current system analysis for migration tracking

# 2. Product Manager - Plan modernization roadmap
*agent pm
*task context-retrieval --topic="modernization roadmaps" --source="architect-analysis"
# Gets: Technical constraints and opportunities from architect

*utils context-analysis --focus="business-value-alignment"
# Analyzes: Ensures modernization aligns with business priorities

# 3. Scrum Master - Plan migration sprints
*agent sm
*task context-retrieval --topic="migration sprint planning" --complexity="high"
# Retrieves: Sprint planning strategies for complex migrations

*task context-memory-management --action="store" --tag="migration-velocity-baseline"
# Stores: Initial velocity estimates for future sprint planning
```

**Benefits Achieved**:

- ✅ Proven migration patterns applied immediately
- ✅ Risk mitigation based on similar project learnings
- ✅ Realistic timeline estimation with historical data

---

## Advanced Workflows

### 🔄 **Cross-Agent Knowledge Sharing**

**Use Case**: Ensure design decisions influence development patterns

```bash
# 1. UX Expert creates design patterns
*agent ux-expert
*task context-memory-management --action="store" --tag="design-system-patterns" --share="architect,dev"

# 2. Architect incorporates design constraints
*agent architect
*task context-retrieval --topic="design-system-patterns" --source="ux-expert"
*task context-memory-management --action="update" --tag="technical-architecture" --include="design-constraints"

# 3. Dev agent gets optimized context
*agent dev
*task context-handoff --source="architect" --focus="implementation-patterns"
# Automatically gets lean context including design constraints
```

### 📈 **Progressive Context Building**

**Use Case**: Building comprehensive product strategy over multiple sessions

```bash
# Session 1: Market Research
*agent analyst
*task create-deep-research-prompt --topic="AI productivity tools market"
*task context-memory-management --action="store" --tag="market-foundation"

# Session 2: Competitive Analysis (1 week later)
*agent analyst
*task context-retrieval --topic="market-foundation" --restore="previous-session"
*task create-doc competitor-analysis-tmpl
*task context-memory-management --action="append" --tag="market-foundation"

# Session 3: Product Strategy (2 weeks later)
*agent pm
*task context-retrieval --topic="market-foundation" --complete="true"
# Gets: Full market research + competitive analysis
*task create-doc prd-tmpl
```

### 🎯 **Context-Driven Decision Making**

**Use Case**: Architectural decisions based on stored performance data

```bash
# Store performance context
*agent qa
*task context-memory-management --action="store" --tag="performance-baselines" --metrics="response-times,throughput"

# Retrieve for architecture decisions
*agent architect
*task context-retrieval --topic="performance-baselines" --analysis="bottlenecks"
*utils context-analysis --focus="performance-constraints"
# Makes architecture decisions based on real performance data
```

---

## Best Practices

### 🎯 **Effective Context Tagging**

**Strategic Tagging System**:

```bash
# Time-based tags
--tag="q1-2025-strategy"
--tag="sprint-15-retrospective"

# Feature-based tags
--tag="authentication-v2"
--tag="payment-processing-research"

# Role-based tags
--tag="architect-decisions"
--tag="ux-patterns-mobile"

# Project-phase tags
--tag="mvp-requirements"
--tag="scale-optimization"
```

### 🔍 **Smart Retrieval Queries**

**Effective Query Patterns**:

```bash
# Specific and contextual
*task context-retrieval --topic="API rate limiting strategies" --scale="high-traffic"

# Time-sensitive
*task context-retrieval --topic="user feedback" --timeframe="last-month"

# Multi-dimensional
*task context-retrieval --topic="mobile authentication" --platform="ios,android" --security="biometric"

# Pattern-based
*utils semantic-search --query="database migration zero downtime patterns"
```

### 💾 **Memory Management Strategy**

**Storage Hierarchy**:

```bash
# Critical decisions (long-term storage)
*task context-memory-management --action="store" --priority="high" --retention="permanent"

# Sprint learnings (medium-term)
*task context-memory-management --action="store" --priority="medium" --retention="6-months"

# Temporary insights (short-term)
*task context-memory-management --action="store" --priority="low" --retention="30-days"
```

### 🔄 **Context Quality Maintenance**

**Regular Quality Checks**:

```bash
# Weekly context health check
*utils context-analysis --scope="project-wide" --focus="completeness,relevance"

# Pre-sprint context optimization
*task context-optimization --target="sprint-context" --focus="actionable-items"

# Cross-agent context validation
*task context-validation --scope="cross-agent" --ensure="consistency"
```

---

## Troubleshooting

### ❗ **Common Issues and Solutions**

#### **Context Retrieval Returns Empty Results**

**Problem**: `*task context-retrieval` returns no relevant information

**Solutions**:

```bash
# 1. Check stored context tags
*task context-memory-management --action="list" --filter="topic-keywords"

# 2. Broaden search scope
*task context-retrieval --topic="authentication" --scope="broad" --similarity="0.6"

# 3. Use semantic search instead
*utils semantic-search --query="user login flow patterns" --include-related="true"
```

#### **Memory Storage Failing**

**Problem**: `*task context-memory-management --action="store"` returns errors

**Solutions**:

```bash
# 1. Check storage capacity
*utils context-analysis --focus="storage-utilization"

# 2. Optimize before storing
*task context-optimization --target-ratio="0.7" --preserve="key-decisions"
*task context-memory-management --action="store" --compressed="true"

# 3. Archive old context
*task context-memory-management --action="archive" --older-than="3-months"
```

#### **Context Quality Issues**

**Problem**: Retrieved context lacks relevance or completeness

**Solutions**:

```bash
# 1. Run quality analysis
*utils context-analysis --focus="relevance,completeness" --report="detailed"

# 2. Validate context sources
*task context-validation --scope="current-context" --check="accuracy,recency"

# 3. Re-optimize with better focus
*task context-optimization --focus="user-requirements" --preserve="acceptance-criteria"
```

#### **Cross-Agent Context Inconsistency**

**Problem**: Different agents receive inconsistent context

**Solutions**:

```bash
# 1. Validate cross-agent handoffs
*task context-validation --scope="cross-agent" --ensure="consistency"

# 2. Standardize context handoff
*task context-handoff --target="architect" --standardize="true"

# 3. Synchronize context across agents
*task context-memory-management --action="sync" --agents="pm,architect,po"
```

### 🔧 **Performance Optimization**

#### **Slow Context Retrieval**

```bash
# Enable caching for frequent queries
*task context-retrieval --topic="common-patterns" --cache="enabled"

# Use targeted retrieval scope
*task context-retrieval --topic="specific-topic" --scope="narrow" --max-results="10"

# Pre-warm frequently used context
*task context-memory-management --action="preload" --tags="daily-use-patterns"
```

#### **Memory Usage Optimization**

```bash
# Regular memory cleanup
*task context-memory-management --action="cleanup" --criteria="unused-30-days"

# Intelligent compression
*task context-optimization --algorithm="adaptive" --quality="high"

# Storage tiering
*task context-memory-management --action="tier" --hot="current-sprint" --cold="archived"
```

---

## 🎉 Next Steps

**Ready to Start?**

1. **Choose a Planning Agent**: Start with PM, Architect, or Analyst
2. **Store Initial Context**: Use `context-memory-management` to build your knowledge base
3. **Practice Retrieval**: Try `context-retrieval` with different topics
4. **Optimize Workflows**: Use `context-analysis` to improve your process

**Advanced Usage**:

- Explore multi-agent workflows with shared context
- Build context libraries for recurring project patterns
- Create custom tagging strategies for your team
- Implement context-driven automation workflows

**Get Support**:

- Check the main [User Guide](./user-guide.md) for general BMAD usage
- Review [Context Engineering Guide](./context-engineering-guide.md) for technical details
- Join the community for advanced tips and patterns

---

_Happy building with BMAD Rich Context! 🚀_
