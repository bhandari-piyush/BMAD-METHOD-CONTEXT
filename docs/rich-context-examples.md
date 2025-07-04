# BMAD Rich Context - Practical Examples

**Real-world scenarios and workflows using enhanced context capabilities**

## 🎯 Overview

This guide provides practical, copy-paste examples for leveraging BMAD's rich context features in real development scenarios. Each example includes setup, execution, and expected outcomes.

---

## 📚 Table of Contents

1. [Quick Reference Commands](#quick-reference-commands)
2. [Startup Project Scenarios](#startup-project-scenarios)
3. [Enterprise Development](#enterprise-development)
4. [Legacy System Modernization](#legacy-system-modernization)
5. [Cross-Team Collaboration](#cross-team-collaboration)
6. [Performance & Optimization](#performance--optimization)
7. [Troubleshooting Examples](#troubleshooting-examples)

---

## Quick Reference Commands

### 🚀 **Essential Rich Context Commands**

```bash
# Context Retrieval
*task context-retrieval --topic="[topic]" --scope="[narrow|broad]"
*task context-retrieval --topic="authentication patterns" --platform="mobile"
*task context-retrieval --topic="database optimization" --scale="enterprise"

# Memory Management
*task context-memory-management --action="store" --tag="[memorable-tag]"
*task context-memory-management --action="retrieve" --tag="[tag]"
*task context-memory-management --action="list" --filter="[keyword]"

# Semantic Search
*utils semantic-search --query="[natural language query]"
*utils semantic-search --query="React performance optimization patterns"
*utils semantic-search --query="API rate limiting best practices"

# Context Analysis
*utils context-analysis --focus="[completeness|relevance|quality]"
*utils context-analysis --scope="project-wide" --report="detailed"
```

---

## Startup Project Scenarios

### 🚀 **Scenario 1: SaaS MVP Development**

**Context**: Building a project management SaaS from scratch

#### **Phase 1: Market Research & Strategy**

```bash
*agent analyst

# Research competitive landscape
*task context-retrieval --topic="project management tools" --focus="feature-comparison"
*task create-deep-research-prompt --topic="PM tool market trends 2025"

# Store research findings
*task context-memory-management --action="store" --tag="pm-tool-market-research" --priority="high"

# Analyze market gaps
*utils semantic-search --query="project management pain points small teams"
*utils context-analysis --focus="market-opportunity-size"
```

#### **Phase 2: Product Strategy Development**

```bash
*agent pm

# Retrieve market insights
*task context-retrieval --topic="pm-tool-market-research" --source="analyst"

# Create data-driven PRD
*task create-doc prd-tmpl
# Include: Market research findings, competitive gaps, user personas

# Store product strategy
*task context-memory-management --action="store" --tag="mvp-product-strategy" --share="architect,po"
```

#### **Phase 3: Technical Architecture**

```bash
*agent architect

# Get product requirements context
*task context-retrieval --topic="mvp-product-strategy" --source="pm"

# Research technical patterns for PM tools
*utils semantic-search --query="project management app architecture patterns scalable"
*task context-retrieval --topic="SaaS architecture" --scale="startup" --focus="cost-effective"

# Design MVP architecture
*task create-doc fullstack-architecture-tmpl

# Store technical decisions
*task context-memory-management --action="store" --tag="mvp-tech-architecture" --include="cost-analysis"
```

#### **Expected Outcomes**:

- ✅ Market-informed product strategy
- ✅ Technical architecture aligned with business goals
- ✅ Reusable research for future feature planning
- ✅ 60% faster product definition process

---

### 🏗️ **Scenario 2: E-learning Platform**

**Context**: Creating online education platform with video content

#### **Multi-Agent Workflow with Rich Context**

```bash
# 1. UX Research and Design Strategy
*agent ux-expert

*task context-retrieval --topic="e-learning UX patterns" --accessibility="wcag-aa"
*utils semantic-search --query="video player UX best practices mobile responsive"
*task context-memory-management --action="store" --tag="elearning-ux-patterns"

# 2. Technical Architecture for Video Platform
*agent architect

*task context-retrieval --topic="elearning-ux-patterns" --source="ux-expert"
*utils semantic-search --query="video streaming architecture CDN optimization"
*task context-retrieval --topic="video platform architecture" --scale="medium" --focus="performance"

*task create-doc fullstack-architecture-tmpl
*task context-memory-management --action="store" --tag="video-platform-arch" --include="performance-metrics"

# 3. Learning Management System Features
*agent pm

*task context-retrieval --topic="video-platform-arch" --focus="feature-constraints"
*utils semantic-search --query="LMS feature prioritization student engagement"
*task create-doc prd-tmpl

# 4. Video Content Testing Strategy
*agent qa

*task context-retrieval --topic="video-platform-arch" --focus="performance-requirements"
*utils semantic-search --query="video streaming testing strategies load performance"
*task context-memory-management --action="store" --tag="video-testing-strategy"
```

#### **Cross-Session Context Building**

```bash
# Week 1: Foundation
*task context-memory-management --action="store" --tag="elearning-foundation" --session="week-1"

# Week 2: Retrieve and Build Upon
*task context-retrieval --topic="elearning-foundation" --restore="previous-session"
*task context-memory-management --action="append" --tag="elearning-foundation"

# Week 3: Complete Product Definition
*task context-retrieval --topic="elearning-foundation" --complete="full-history"
```

---

## Enterprise Development

### 🏢 **Scenario 3: Microservices Architecture Migration**

**Context**: Migrating monolithic enterprise application to microservices

#### **Analysis and Planning Phase**

```bash
*agent architect

# Research migration patterns
*task context-retrieval --topic="monolith to microservices" --scale="enterprise" --industry="financial"
*utils semantic-search --query="strangler fig pattern implementation timeline risks"

# Analyze current system
*task document-project --focus="dependency-mapping"
*task context-memory-management --action="store" --tag="legacy-system-analysis" --priority="critical"

# Create migration strategy
*utils context-analysis --focus="technical-debt-assessment"
*task create-doc architecture-tmpl --template="brownfield-architecture-tmpl"
```

#### **Service Decomposition Planning**

```bash
*agent pm

# Get technical constraints
*task context-retrieval --topic="legacy-system-analysis" --source="architect"

# Research business domain patterns
*utils semantic-search --query="domain driven design microservices bounded contexts"
*task context-retrieval --topic="service decomposition" --focus="business-domains"

# Plan service rollout
*task create-doc prd-tmpl --focus="migration-roadmap"
*task context-memory-management --action="store" --tag="service-decomposition-plan"
```

#### **Quality Assurance Strategy**

```bash
*agent qa

# Understand architecture constraints
*task context-retrieval --topic="service-decomposition-plan" --source="pm"
*task context-retrieval --topic="legacy-system-analysis" --focus="integration-points"

# Plan comprehensive testing
*utils semantic-search --query="microservices testing strategies contract testing"
*task context-memory-management --action="store" --tag="microservices-test-strategy"
```

#### **Expected Outcomes**:

- ✅ Risk-assessed migration strategy
- ✅ Business-aligned service boundaries
- ✅ Comprehensive testing approach
- ✅ Historical decision tracking for future services

---

## Cross-Team Collaboration

### 👥 **Scenario 4: Multi-Team Feature Development**

**Context**: Payment system feature requiring coordination across teams

#### **Shared Context Setup**

```bash
# Team Lead: Establish shared context baseline
*agent sm

*task context-memory-management --action="store" --tag="payment-feature-baseline" --share="all-agents"
*utils context-analysis --scope="cross-team" --focus="dependency-identification"

# Share with specific teams
*task context-memory-management --action="share" --tag="payment-feature-baseline" --teams="backend,frontend,qa"
```

#### **Backend Team Context**

```bash
*agent architect

# Get shared baseline
*task context-retrieval --topic="payment-feature-baseline" --team="backend"

# Add backend-specific research
*utils semantic-search --query="payment processing API security PCI compliance"
*task context-memory-management --action="append" --tag="payment-feature-baseline" --scope="backend"
```

#### **Frontend Team Context**

```bash
*agent ux-expert

# Get shared baseline + backend insights
*task context-retrieval --topic="payment-feature-baseline" --include="backend"

# Add frontend-specific patterns
*utils semantic-search --query="payment form UX security mobile responsive"
*task context-memory-management --action="append" --tag="payment-feature-baseline" --scope="frontend"
```

#### **QA Team Integration**

```bash
*agent qa

# Get complete feature context
*task context-retrieval --topic="payment-feature-baseline" --include="backend,frontend"

# Plan integrated testing
*utils semantic-search --query="payment system testing end-to-end security"
*task context-memory-management --action="finalize" --tag="payment-feature-complete"
```

---

## Performance & Optimization

### ⚡ **Scenario 5: Performance Optimization Project**

**Context**: Optimizing slow-performing e-commerce platform

#### **Performance Analysis**

```bash
*agent qa

# Research performance patterns
*task context-retrieval --topic="ecommerce performance optimization" --scale="high-traffic"
*utils semantic-search --query="database query optimization ecommerce catalog"

# Analyze current metrics
*utils context-analysis --focus="performance-bottlenecks" --data="monitoring-metrics"
*task context-memory-management --action="store" --tag="performance-baseline" --metrics="response-times,throughput"
```

#### **Architecture Optimization**

```bash
*agent architect

# Get performance constraints
*task context-retrieval --topic="performance-baseline" --source="qa"

# Research optimization strategies
*utils semantic-search --query="ecommerce architecture optimization caching CDN database"
*task context-retrieval --topic="performance optimization patterns" --platform="web" --scale="enterprise"

# Design optimization plan
*task create-doc architecture-tmpl --focus="performance-improvements"
*task context-memory-management --action="store" --tag="optimization-strategy"
```

#### **Implementation Planning**

```bash
*agent pm

# Get technical optimization plan
*task context-retrieval --topic="optimization-strategy" --source="architect"

# Prioritize optimizations by impact
*utils context-analysis --focus="business-impact-analysis"
*task create-doc prd-tmpl --focus="performance-roadmap"
```

---

## Troubleshooting Examples

### 🔧 **Common Issues and Solutions**

#### **Issue 1: Context Retrieval Returns No Results**

```bash
# Diagnosis
*task context-memory-management --action="list" --filter="stored-tags"
*utils context-analysis --focus="storage-health" --report="detailed"

# Solution 1: Broaden search
*task context-retrieval --topic="authentication" --scope="broad" --similarity="0.5"

# Solution 2: Check related topics
*utils semantic-search --query="user login authentication patterns" --include-related="true"

# Solution 3: Verify storage
*task context-memory-management --action="verify" --tag="authentication-patterns"
```

#### **Issue 2: Memory Storage Failures**

```bash
# Check storage capacity
*utils context-analysis --focus="storage-utilization" --alerts="capacity"

# Optimize before storing
*task context-optimization --target-ratio="0.7" --preserve="key-decisions"
*task context-memory-management --action="store" --optimized="true"

# Clean up old data
*task context-memory-management --action="cleanup" --older-than="90-days" --priority="low"
```

#### **Issue 3: Slow Performance**

```bash
# Enable performance monitoring
*utils context-analysis --focus="performance-metrics" --monitor="enabled"

# Use caching for frequent queries
*task context-retrieval --topic="common-patterns" --cache="enabled" --ttl="24h"

# Optimize query scope
*task context-retrieval --topic="specific-topic" --scope="narrow" --max-results="5"
```

---

## 🎯 Quick Start Checklist

**For New Projects**:

- [ ] Set up context memory with `context-memory-management --action="initialize"`
- [ ] Store project baseline with `--tag="project-foundation"`
- [ ] Configure agent-specific context sharing
- [ ] Establish tagging conventions for your team

**For Existing Projects**:

- [ ] Analyze current context with `context-analysis --scope="project-wide"`
- [ ] Migrate important decisions to memory storage
- [ ] Set up cross-agent context retrieval patterns
- [ ] Optimize context workflows for your team

**Best Practices**:

- [ ] Use descriptive, searchable tags
- [ ] Store context at logical decision points
- [ ] Regular context quality analysis
- [ ] Cross-agent context validation

---

_Ready to implement these patterns in your projects? Start with a simple scenario and gradually build your rich context workflows! 🚀_
