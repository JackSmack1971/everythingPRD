# MCP Configuration Guide

**Complete Setup Guide for everythingPRD MCP Infrastructure**

This guide provides comprehensive instructions for configuring the four specialized MCP (Model Context Protocol) servers that power the everythingPRD system. Each server provides unique capabilities essential for professional PRD generation.

## 🎯 Overview

The everythingPRD system requires four MCP servers working in coordination:

| Server | Purpose | Complexity | Required For |
|--------|---------|------------|--------------|
| **Memory MCP** | Persistent context across sessions | High | Both agents |
| **Sequential Thinking** | Structured reasoning framework | Medium | Both agents |
| **Perplexity Ask** | Real-time research capabilities | Medium | Research integration |
| **Context7** | Live technical documentation | Low | Technical validation |

## 🚀 Quick Setup (Complete Configuration)

### Claude Desktop MCP Configuration

Add this complete configuration to your Claude Desktop `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "mem0": {
      "transport": "sse",
      "url": "http://localhost:8050/sse"
    },
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@zengwenliang/mcp-server-sequential-thinking"]
    },
    "perplexity-ask": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "-e", "PERPLEXITY_API_KEY", "mcp/perplexity-ask"],
      "env": {
        "PERPLEXITY_API_KEY": "YOUR_ACTUAL_API_KEY_HERE"
      }
    },
    "context7": {
      "url": "https://mcp.context7.com/mcp"
    }
  }
}
```

**⚠️ Important**: Replace `YOUR_ACTUAL_API_KEY_HERE` with your real Perplexity API key.

## 📋 Detailed Server Configuration

## 1. Memory MCP Server

### Overview
Provides persistent, knowledge graph-based memory capabilities for AI agents, enabling long-term information storage and retrieval across conversations and sessions.

### Key Features
- **Semantic Memory Storage**: Uses vector embeddings for intelligent information storage
- **Cross-Session Persistence**: Maintains context across different AI agent sessions
- **Memory Retrieval**: Full context refresh and semantic search capabilities
- **Knowledge Graph**: Builds relationships between stored information

### Technical Requirements
- **Python**: 3.12 or higher
- **Database**: PostgreSQL-compatible (Supabase recommended for cloud)
- **LLM Provider**: API keys for OpenAI, OpenRouter, or Ollama
- **Docker**: Optional but recommended for containerized deployment

### Installation Steps

#### Option 1: Docker Deployment (Recommended)
```bash
# Clone the repository
git clone https://github.com/coleam00/mcp-mem0
cd mcp-mem0

# Configure environment variables
cp .env.example .env
# Edit .env with your database and LLM provider credentials

# Start with Docker Compose
docker-compose up -d
```

#### Option 2: Local Python Installation
```bash
# Install dependencies
pip install -r requirements.txt

# Set up database (PostgreSQL)
createdb mem0_db

# Configure environment variables
export DATABASE_URL="postgresql://user:pass@localhost/mem0_db"
export OPENAI_API_KEY="your_openai_key"

# Start the server
python -m mem0.server
```

### Configuration Validation
```bash
# Test memory server health
curl http://localhost:8050/health

# Expected response: {"status": "healthy", "version": "1.0.0"}
```

### Use Cases in everythingPRD
- **Context Continuity**: Maintain brainstorming context across sessions
- **Decision Tracking**: Store and retrieve key product decisions
- **Research Accumulation**: Build knowledge base from research findings
- **Consistency Checking**: Prevent contradictory requirements or recommendations

---

## 2. Sequential Thinking MCP Server

### Overview
Implements structured problem-solving approach that breaks complex tasks into manageable, sequential steps with revision capabilities.

### Key Features
- **Structured Analysis**: Break complex problems into sequential steps
- **Iterative Refinement**: Revise and refine thoughts as understanding evolves
- **Alternative Pathways**: Branch into different reasoning approaches
- **Dynamic Adjustment**: Modify thinking steps based on complexity

### Technical Requirements
- **Node.js**: Latest LTS version
- **NPM**: Package manager for Node.js
- **NPX**: For direct package execution (comes with npm)

### Installation Steps

#### Automatic Installation (Recommended)
```bash
# NPX will automatically install and run the latest version
# This happens automatically when Claude Desktop starts the server
npx -y @zengwenliang/mcp-server-sequential-thinking
```

#### Manual Installation
```bash
# Install globally
npm install -g @zengwenliang/mcp-server-sequential-thinking

# Or install locally in project
npm install @zengwenliang/mcp-server-sequential-thinking
```

### Configuration Validation
The sequential thinking server is stateless and doesn't require health checks. Validation occurs during first use in Claude Desktop.

### Use Cases in everythingPRD
- **Feature Prioritization**: Systematic analysis of feature importance and complexity
- **Risk Assessment**: Structured evaluation of potential risks and mitigations
- **Market Analysis**: Step-by-step competitive and market research
- **Technical Architecture**: Systematic evaluation of implementation approaches

---

## 3. Perplexity Ask MCP Server

### Overview
Integrates with Perplexity's Sonar API to provide AI agents with real-time web search capabilities and current information access.

### Key Features
- **Real-time Web Search**: Access current information from across the internet
- **Conversational Interface**: Natural language queries with structured responses
- **Source Attribution**: Proper citation of research sources
- **Streaming Responses**: Efficient delivery of search results

### Technical Requirements
- **Perplexity Sonar API Key**: Valid subscription with sufficient credits
- **Docker**: For containerized deployment (recommended)
- **Node.js**: Alternative for local installation
- **Network Access**: Outbound connectivity to Perplexity API

### Getting Perplexity API Key

1. **Sign up at [Perplexity](https://www.perplexity.ai/)**
2. **Navigate to API section** in your account settings
3. **Generate API key** and note your credit limits
4. **Verify key works** with a test query

### Installation Steps

#### Docker Deployment (Recommended)
```bash
# Pull the official image
docker pull mcp/perplexity-ask

# Test with your API key
docker run -i --rm \
  -e PERPLEXITY_API_KEY="your_actual_api_key" \
  mcp/perplexity-ask
```

#### Local Node.js Installation
```bash
# Clone repository
git clone https://github.com/ppl-ai/modelcontextprotocol
cd modelcontextprotocol/perplexity-ask

# Install dependencies
npm install

# Set environment variable
export PERPLEXITY_API_KEY="your_actual_api_key"

# Start server
npm start
```

### Configuration Validation
```bash
# Test API key validity
curl -H "Authorization: Bearer YOUR_API_KEY" \
     https://api.perplexity.ai/models

# Expected: List of available models
```

### Rate Limits and Best Practices
- **Monitor API usage** against your monthly credit allocation
- **Implement query optimization** to reduce unnecessary requests
- **Use specific, targeted queries** rather than broad searches
- **Cache frequently accessed information** when possible

### Use Cases in everythingPRD
- **Market Research**: Current market size, trends, and competitive landscape
- **User Research**: Recent studies, surveys, and user behavior data
- **Technology Trends**: Latest developments in relevant technical areas
- **Business Intelligence**: Industry reports, financial data, and benchmarks

---

## 4. Context7 MCP Server

### Overview
Provides up-to-date, version-specific documentation and code examples for programming libraries and frameworks, eliminating outdated API references.

### Key Features
- **Live Documentation**: Fetches current, version-specific docs from source repositories
- **Library Resolution**: Converts general library names to Context7-compatible IDs
- **Topic Filtering**: Narrow documentation to specific areas (routing, hooks, etc.)
- **Token Control**: Configurable output length for optimal context usage

### Technical Requirements
- **Network Connectivity**: Direct access to https://mcp.context7.com
- **No Installation Required**: Cloud-hosted service
- **MCP Client**: Compatible with Claude Desktop, Cursor, Windsurf, VS Code

### Configuration
```json
{
  "context7": {
    "url": "https://mcp.context7.com/mcp"
  }
}
```

### Configuration Validation
```bash
# Test Context7 connectivity
curl https://mcp.context7.com/health

# Expected: {"status": "healthy", "libraries": [...]}
```

### Supported Libraries and Frameworks
- **Web Frameworks**: React, Vue, Angular, Svelte
- **Backend**: Node.js, Express, FastAPI, Django
- **Databases**: MongoDB, PostgreSQL, Redis
- **APIs**: Stripe, Twilio, SendGrid, AWS SDK
- **AI/ML**: TensorFlow, PyTorch, OpenAI

### Use Cases in everythingPRD
- **Technical Feasibility**: Validate API capabilities and limitations
- **Implementation Planning**: Get current best practices and examples
- **Architecture Decisions**: Compare framework capabilities and requirements
- **Security Compliance**: Access current security standards and implementations

---

## 🔧 Troubleshooting Guide

### Common Configuration Issues

#### Memory Server Won't Start
**Symptoms**: Connection refused, database errors
**Solutions**:
```bash
# Check database connectivity
pg_isready -h localhost -p 5432

# Verify environment variables
echo $DATABASE_URL
echo $OPENAI_API_KEY

# Review server logs
docker logs mcp-memory-server
```

#### Sequential Thinking Errors
**Symptoms**: NPX installation failures, command not found
**Solutions**:
```bash
# Update Node.js and npm
npm install -g npm@latest

# Clear npm cache
npm cache clean --force

# Reinstall package
npx -y @zengwenliang/mcp-server-sequential-thinking
```

#### Perplexity API Issues
**Symptoms**: Authentication errors, rate limit exceeded
**Solutions**:
```bash
# Verify API key
curl -H "Authorization: Bearer $PERPLEXITY_API_KEY" \
     https://api.perplexity.ai/models

# Check credit balance at https://www.perplexity.ai/settings/api

# Test with simple query
echo '{"model": "llama-3.1-sonar-small-128k-online", "messages": [{"role": "user", "content": "test"}]}' | \
curl -X POST https://api.perplexity.ai/chat/completions \
     -H "Authorization: Bearer $PERPLEXITY_API_KEY" \
     -H "Content-Type: application/json" \
     -d @-
```

#### Context7 Connectivity Problems
**Symptoms**: Network timeouts, service unavailable
**Solutions**:
```bash
# Test basic connectivity
ping mcp.context7.com

# Check firewall/proxy settings
curl -v https://mcp.context7.com/mcp

# Try alternative DNS
nslookup mcp.context7.com 8.8.8.8
```

### Performance Optimization

#### Memory Server Optimization
- **Database Tuning**: Configure PostgreSQL for memory workload
- **Connection Pooling**: Use connection pooling for high-volume usage
- **Index Optimization**: Ensure proper indexing for semantic search
- **Memory Management**: Monitor RAM usage and implement cleanup routines

#### Perplexity Rate Limit Management
- **Query Batching**: Combine related research questions
- **Caching Strategy**: Store frequently accessed research results
- **Priority Queuing**: Prioritize critical research requests
- **Fallback Sources**: Implement alternative research sources

## 📊 Configuration Testing Checklist

Before using the everythingPRD system, verify all components:

- [ ] **Memory Server**: Health check returns 200, can store/retrieve test data
- [ ] **Sequential Thinking**: Can execute basic reasoning tasks without errors
- [ ] **Perplexity Ask**: API key valid, can perform test searches
- [ ] **Context7**: Can access documentation for common libraries
- [ ] **Claude Desktop**: MCP configuration properly formatted and loaded
- [ ] **Network**: All outbound connections working (Perplexity, Context7)
- [ ] **Credentials**: All API keys and database credentials valid

## 🎯 Next Steps

Once all MCP servers are configured and validated:

1. **Review System Instructions**: Familiarize yourself with [BrainStormer](system-instruction-prompts/BrainStormer_MCP.md) and [PRD Generation Agent](system-instruction-prompts/PRD_Generation_Agent_MCP.md)
2. **Test Workflow**: Run a simple concept through the complete brainstorming → PRD generation pipeline
3. **Examine Examples**: Study the [example PRDs](prd-examples/) to understand output quality expectations
4. **Optimize Configuration**: Adjust settings based on your usage patterns and requirements

For ongoing support and advanced configuration options, refer to the individual MCP server documentation linked in each section.
