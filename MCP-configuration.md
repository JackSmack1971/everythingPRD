## 1. Memory MCP Server

### Overview
The Memory MCP server provides persistent, knowledge graph-based memory capabilities for AI agents. It enables long-term information storage and retrieval across conversations and sessions [GitHub](https://github.com/coleam00/mcp-mem0).

### Key Features
- **Semantic Memory Storage**: Uses vector embeddings to store information with semantic understanding
- **Memory Retrieval**: Full context refresh by retrieving all stored memories
- **Semantic Search**: Find relevant past information using similarity search
- **Cross-Session Persistence**: Maintains context across different AI agent sessions

### Technical Requirements
- Python 3.12+
- PostgreSQL-compatible database (Supabase recommended)
- API keys for LLM providers (OpenAI, OpenRouter, or Ollama)
- Docker (optional but recommended)

### Installation & Configuration
```json
{
  "mcpServers": {
    "mem0": {
      "transport": "sse",
      "url": "http://localhost:8050/sse"
    }
  }
}
```

### Use Cases
- Long-term conversation memory for AI assistants
- Knowledge accumulation across multiple sessions
- Context-aware responses based on historical interactions
- Personal AI assistants that remember preferences and past conversations

## 2. Sequential Thinking MCP Server

### Overview
The Sequential Thinking MCP server implements a structured problem-solving approach that breaks complex tasks into manageable, sequential steps. It enables AI agents to engage in multi-step reasoning with revision capabilities [GitHub](https://github.com/zengwenliang416/mcp-server-sequential-thinking).

### Key Features
- **Structured Analysis**: Break complex problems into sequential steps
- **Iterative Refinement**: Revise and refine thoughts as understanding evolves
- **Alternative Pathways**: Branch into different reasoning approaches
- **Dynamic Adjustment**: Modify the number of thinking steps as needed
- **Solution Validation**: Generate and verify hypotheses

### Technical Requirements
- Node.js and npm
- NPX access or Docker runtime

### Installation & Configuration
```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@zengwenliang/mcp-server-sequential-thinking"]
    }
  }
}
```

### Use Cases
- Complex problem-solving that requires step-by-step analysis
- Planning and design projects needing multiple iterations
- Analytical workflows requiring course corrections
- Research tasks where scope evolves over time
- Educational applications teaching structured thinking

## 3. Perplexity Ask MCP Server

### Overview
The Perplexity Ask MCP server integrates with Perplexity's Sonar API to provide AI agents with real-time web search capabilities. It enables access to current information from across the internet [GitHub](https://github.com/ppl-ai/modelcontextprotocol).

### Key Features
- **Real-time Web Search**: Access current information from the internet
- **Conversational Interface**: Structured message format for natural interaction
- **Streaming Responses**: Efficient delivery of search results
- **Customizable Parameters**: Adjustable search depth and result formatting
- **Multi-App Support**: Compatible with Claude Desktop, Cursor, and other MCP clients

### Technical Requirements
- Node.js and npm
- Valid Perplexity Sonar API key
- Docker (optional)
- MCP-compatible client

### Installation & Configuration
```json
{
  "mcpServers": {
    "perplexity-ask": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "-e", "PERPLEXITY_API_KEY", "mcp/perplexity-ask"],
      "env": {
        "PERPLEXITY_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

### Use Cases
- Real-time research and fact-checking
- Current events and news queries
- Market research and trend analysis
- Academic research with recent publications
- Competitive analysis and business intelligence


## 4. Context7 MCP Server

### Overview
Context7 MCP server provides up-to-date, version-specific documentation and code examples for programming libraries and frameworks. It eliminates outdated API references and hallucinated code by fetching live documentation directly from sources [GitHub](https://github.com/upstash/context7).

### Key Features
- **Live Documentation**: Fetches current, version-specific docs from source repositories
- **Library Resolution**: Converts general library names to Context7-compatible IDs
- **Topic Filtering**: Narrow documentation to specific topics (routing, hooks, etc.)
- **Token Control**: Configurable output length (default 10,000 tokens)
- **Multi-Client Support**: Works with Cursor, Windsurf, Claude Desktop, VS Code, and more

### Technical Requirements
- Node.js >= 18.0.0
- MCP-compatible client (Cursor, Windsurf, Claude Desktop, etc.)
- Network connectivity to https://mcp.context7.com

### Installation & Configuration
```json
{
  "mcpServers": {
    "context7": {
      "url": "https://mcp.context7.com/mcp"
    }
  }
}
```

### Use Cases
- Generating accurate code snippets with current APIs
- Learning new frameworks with up-to-date examples
- Avoiding deprecated functions and outdated practices
- Onboarding developers to new libraries
- Maintaining code with latest best practices
