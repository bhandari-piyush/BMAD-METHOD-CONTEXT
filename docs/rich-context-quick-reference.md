# BMAD Rich Context - Quick Reference

**Essential commands and patterns for enhanced agent capabilities**

## 🚀 Quick Commands

### Context Retrieval

```bash
*task context-retrieval --topic="[subject]" --scope="[narrow|broad]"
*task context-retrieval --topic="API design patterns" --scale="enterprise"
*task context-retrieval --topic="user research" --timeframe="6-months"
```

### Memory Management

```bash
*task context-memory-management --action="store" --tag="[memorable-name]"
*task context-memory-management --action="retrieve" --tag="[tag-name]"
*task context-memory-management --action="list" --filter="[keyword]"
```

### Semantic Search

```bash
*utils semantic-search --query="[natural language search]"
*utils semantic-search --query="React performance optimization"
*utils semantic-search --query="payment form UX best practices"
```

### Context Analysis

```bash
*utils context-analysis --focus="[completeness|quality|performance]"
*utils context-analysis --scope="project-wide" --report="detailed"
```

---

## 🎭 Enhanced Agents

### Planning Agents (Rich Context)

- **🎭 bmad-orchestrator** - Advanced workflow orchestration
- **🏗️ architect** - Technical pattern memory & retrieval
- **📋 pm** - Product strategy & market research context
- **📝 po** - Backlog patterns & user journey memory
- **📊 analyst** - Business research & insight patterns
- **🎨 ux-expert** - Design patterns & accessibility context
- **🧪 qa** - Test strategies & quality metrics
- **🏃 sm** - Team dynamics & sprint retrospectives

### Development Agent (Lean Context)

- **💻 dev** - Streamlined for fast implementation

---

## 🔄 Common Workflows

### Cross-Agent Knowledge Sharing

```bash
# 1. Store knowledge with sharing
*agent [source-agent]
*task context-memory-management --action="store" --tag="feature-research" --share="architect,dev"

# 2. Retrieve in target agent
*agent [target-agent]
*task context-retrieval --topic="feature-research" --source="[source-agent]"
```

### Progressive Context Building

```bash
# Week 1: Foundation
*task context-memory-management --action="store" --tag="project-foundation"

# Week 2: Build upon
*task context-retrieval --topic="project-foundation" --restore="previous-session"
*task context-memory-management --action="append" --tag="project-foundation"
```

### Smart Pattern Discovery

```bash
# Find relevant patterns
*utils semantic-search --query="[describe what you need]"

# Analyze context quality
*utils context-analysis --focus="completeness"

# Store for future use
*task context-memory-management --action="store" --tag="[pattern-name]"
```

---

## 🎯 Best Practices

### Tagging Strategy

- **Time-based**: `q1-2025-strategy`, `sprint-15-retrospective`
- **Feature-based**: `authentication-v2`, `payment-processing`
- **Role-based**: `architect-decisions`, `ux-patterns-mobile`
- **Phase-based**: `mvp-requirements`, `scale-optimization`

### Query Patterns

- **Specific**: `--topic="API rate limiting" --scale="high-traffic"`
- **Time-sensitive**: `--timeframe="last-month"`
- **Multi-dimensional**: `--platform="mobile" --security="biometric"`
- **Pattern-based**: `"database migration zero downtime patterns"`

### Memory Management

- **Critical decisions**: `--priority="high" --retention="permanent"`
- **Sprint learnings**: `--priority="medium" --retention="6-months"`
- **Temporary insights**: `--priority="low" --retention="30-days"`

---

## 🔧 Troubleshooting

### No Results from Retrieval

```bash
# Check stored tags
*task context-memory-management --action="list" --filter="keywords"

# Broaden search
*task context-retrieval --topic="topic" --scope="broad" --similarity="0.5"

# Use semantic search
*utils semantic-search --query="describe what you're looking for" --include-related="true"
```

### Storage Issues

```bash
# Check capacity
*utils context-analysis --focus="storage-utilization"

# Optimize before storing
*task context-optimization --target-ratio="0.7"
*task context-memory-management --action="store" --optimized="true"

# Clean up old data
*task context-memory-management --action="cleanup" --older-than="90-days"
```

### Performance Issues

```bash
# Enable caching
*task context-retrieval --cache="enabled" --ttl="24h"

# Narrow scope
*task context-retrieval --scope="narrow" --max-results="5"

# Monitor performance
*utils context-analysis --focus="performance-metrics" --monitor="enabled"
```

---

## 📚 Full Guides

- **[Rich Context User Guide](./rich-context-user-guide.md)** - Comprehensive capabilities overview
- **[Practical Examples](./rich-context-examples.md)** - Real-world scenarios and workflows
- **[Context Engineering Guide](./context-engineering-guide.md)** - Technical details and architecture
- **[Main User Guide](./user-guide.md)** - General BMAD usage

---

_Keep this reference handy for quick lookup of rich context capabilities! 🚀_
