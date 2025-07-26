# System Instruction Prompts

**MCP-Enhanced AI Agent Instructions for Professional PRD Generation**

This directory contains the core system instruction prompts that power the everythingPRD workflow. Each instruction set is designed to work seamlessly with Model Context Protocol (MCP) servers to provide advanced capabilities beyond standard AI assistance.

## 📋 Overview

The system instructions implement a **two-agent sequential workflow** where specialized AI agents collaborate through MCP infrastructure to transform initial concepts into comprehensive, research-backed Product Requirements Documents.

### Agent Architecture

```
BrainStormer Agent → Research & Memory → PRD Generation Agent → Professional PRD
       ↓                    ↓                    ↓                    ↓
Concept Development    Data Integration    Document Synthesis    Quality Output
```

## 🔄 Complete Workflow Process

### Phase 1: Brainstorming & Concept Development
**Agent:** [BrainStormer_MCP.md](BrainStormer_MCP.md)

1. **Multi-stage ideation** with systematic concept exploration
2. **Self-directed critique** across five critical dimensions
3. **Evidence-based research integration** using Perplexity Ask
4. **Structured memory management** with decision tracking
5. **Iterative refinement** through sequential thinking framework

**Key Capabilities:**
- Sequential Thinking Server for structured multi-stage reasoning
- Memory Server for persistent context management across iterations  
- Perplexity Ask Server for real-time research and market intelligence
- Fetch Server for targeted content retrieval and document analysis

### Phase 2: PRD Generation & Research Integration
**Agent:** [PRD_Generation_Agent_MCP.md](PRD_Generation_Agent_MCP.md)

1. **Memory refresh** from previous brainstorming sessions
2. **Comprehensive research integration** with real-time market data
3. **Technical feasibility validation** using Context7 documentation
4. **Structured analysis framework** with systematic trade-off evaluation
5. **Professional document generation** with evidence-based claims

**Enhanced Capabilities:**
- **Persistent Memory System**: Maintain context across all PRD iterations
- **Real-Time Research Engine**: Access current market data and competitive intelligence
- **Technical Documentation Hub**: Get up-to-date API docs and specifications  
- **Structured Analysis Framework**: Apply systematic reasoning to complex decisions

## 🛠️ MCP Server Setup

### Required MCP Servers

All system instructions depend on proper MCP server configuration. Ensure these are set up before using the agents:

#### 1. Memory MCP Server
```json
{
  "mem0": {
    "transport": "sse", 
    "url": "http://localhost:8050/sse"
  }
}
```
**Purpose**: Persistent context management and cross-session continuity  
**Requirements**: PostgreSQL-compatible database, LLM provider API keys

#### 2. Sequential Thinking MCP Server  
```json
{
  "sequential-thinking": {
    "command": "npx",
    "args": ["-y", "@zengwenliang/mcp-server-sequential-thinking"]
  }
}
```
**Purpose**: Structured multi-stage reasoning and iterative refinement  
**Requirements**: Node.js and npm

#### 3. Perplexity Ask MCP Server
```json
{
  "perplexity-ask": {
    "command": "docker",
    "args": ["run", "-i", "--rm", "-e", "PERPLEXITY_API_KEY", "mcp/perplexity-ask"],
    "env": {
      "PERPLEXITY_API_KEY": "YOUR_API_KEY_HERE"
    }
  }
}
```
**Purpose**: Real-time web search and market research capabilities  
**Requirements**: Valid Perplexity Sonar API key

#### 4. Context7 MCP Server
```json
{
  "context7": {
    "url": "https://mcp.context7.com/mcp"
  }
}
```
**Purpose**: Live documentation and current API specifications  
**Requirements**: Network connectivity to documentation sources

## ⚙️ Configuration Validation

### Pre-Flight Checklist

Before starting the workflow, ensure:

- [ ] **Claude Desktop** MCP configuration is properly formatted
- [ ] **All four MCP servers** are accessible and responding
- [ ] **Perplexity API key** is valid and has sufficient credits
- [ ] **Memory server database** is connected and persistent
- [ ] **Sequential thinking** server is responding to requests
- [ ] **Context7** can access external documentation sources

### Configuration Testing

```bash
# Test MCP server connectivity
# Memory Server
curl http://localhost:8050/health

# Perplexity API
curl -H "Authorization: Bearer YOUR_API_KEY" https://api.perplexity.ai/models

# Context7
curl https://mcp.context7.com/health
```

## 📖 Usage Instructions

### Step 1: Initialize Brainstorming Project

1. **Create new Claude Desktop project**
2. **Paste BrainStormer_MCP.md** into project instructions
3. **Verify MCP server connections** are active
4. **Input initial concept** or requirements

### Step 2: Concept Development Process

The BrainStormer will automatically:
- **Store initial context** in memory for persistence
- **Research market validation** using Perplexity
- **Apply structured thinking** through sequential reasoning
- **Perform self-critique** across multiple dimensions
- **Refine concepts iteratively** based on research findings

### Step 3: Transfer to PRD Generation

1. **Create second Claude Desktop project** for PRD generation
2. **Paste PRD_Generation_Agent_MCP.md** into project instructions
3. **Reference brainstorming output** or key concepts
4. **Allow agent to refresh context** from memory

### Step 4: Professional PRD Creation

The PRD Generation Agent will:
- **Retrieve stored context** from brainstorming session
- **Conduct comprehensive research** for market validation
- **Validate technical feasibility** using live documentation
- **Apply structured analysis** for feature prioritization
- **Generate professional PRD** with evidence-based claims

## 🔍 Best Practices

### Memory Management
- **Store key decisions** with clear rationale and stakeholder input
- **Track changes** between iterations with impact analysis
- **Search memory** before making decisions to maintain consistency
- **Use descriptive tags** for efficient memory retrieval

### Research Integration
- **Triangulate information** using multiple sources for validation
- **Start broad then narrow** search queries for comprehensive coverage
- **Store research findings** with source attribution and confidence levels
- **Cross-reference claims** against stored evidence before finalizing

### Quality Assurance
- **Validate all quantitative claims** with recent research sources
- **Check technical requirements** against current documentation
- **Ensure stakeholder alignment** through memory-based consistency
- **Apply structured critique** across multiple evaluation dimensions

## ⚠️ Troubleshooting

### Common Issues and Solutions

#### Memory Server Problems
**Symptoms**: Context not persisting, memory search failures  
**Solutions**: 
- Verify database connectivity and credentials
- Check memory server logs for errors
- Restart memory server with fresh configuration
- Validate memory storage format and tags

#### Research Integration Failures  
**Symptoms**: Perplexity errors, outdated information, citation issues  
**Solutions**:
- Verify API key validity and rate limit status
- Check network connectivity to research sources
- Adjust search query complexity and frequency
- Implement fallback research strategies

#### Sequential Thinking Errors
**Symptoms**: Reasoning loops, incomplete analysis, logic failures  
**Solutions**:
- Break complex problems into smaller reasoning steps
- Use explicit branching for alternative approaches  
- Validate reasoning chains with evidence checks
- Apply revision capabilities for course corrections

#### Context7 Documentation Access
**Symptoms**: Outdated API docs, connection timeouts, missing libraries  
**Solutions**:
- Verify network connectivity to documentation sources
- Check library name formatting and availability
- Use alternative documentation sources when needed
- Cache frequently accessed documentation locally

### Performance Considerations

#### API Rate Limits
- **Perplexity**: Monitor usage against monthly credits
- **Context7**: Manage concurrent documentation requests
- **Memory Server**: Optimize query frequency and complexity
- **Sequential Thinking**: Balance depth vs. processing time

#### Memory Optimization
- **Regular cleanup** of outdated context and decisions
- **Efficient tagging** for faster memory retrieval
- **Batch operations** when possible to reduce overhead
- **Monitor storage growth** and implement archival strategies

## 🎯 Expected Outcomes

### From BrainStormer Agent
- **Comprehensive concept analysis** with market validation
- **Structured research integration** from authoritative sources
- **Self-critique and refinement** across multiple dimensions
- **Persistent memory storage** of key decisions and rationale

### From PRD Generation Agent  
- **Professional-quality PRDs** comparable to premium consulting output
- **Evidence-based claims** with proper source attribution
- **Technical feasibility validation** using current documentation
- **Comprehensive market analysis** with real-time data integration

### Quality Benchmarks
- **95%+ research accuracy** with validated sources
- **100% technical feasibility** confirmed through live documentation
- **Consistent decision-making** through memory management
- **Market-relevant positioning** with current competitive intelligence

## 📊 Success Metrics

Track the effectiveness of your system instruction implementation:

- **Research Integration**: All major claims backed by recent, authoritative sources
- **Technical Validation**: 100% of requirements validated against current documentation
- **Memory Consistency**: No contradictory decisions or recommendations
- **Output Quality**: PRDs comparable to professional consulting deliverables
- **Workflow Efficiency**: Reduced manual research and validation overhead

For additional support and advanced configuration options, see the main [MCP Configuration Guide](../MCP-configuration.md).
