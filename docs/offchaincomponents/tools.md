---
sidebar_position: 2
---

# Tools Overview

This section covers the offchain tools available for LLM inference and various other functionalities.

## Model Inference

Model inference is handled through Ollama, which is integrated via the `/predict` route in `server/main.py`. This endpoint manages the execution of defined Ollama models for inference operations.

## Available Tools

Tools are implemented in `server/tools/tools.py` and are executed through the `/tool/use` route in `server/main.py`. 

:::info API Keys Required
Some tools require API keys to function. These should be set in your `.env` file:

- OpenAI tools require an [OpenAI API key](https://openai.com/index/openai-api/)
- Scene explanation requires a [Scenex API key](https://scenex.jina.ai/api)
- Tavily search requires a [Tavily API key](https://app.tavily.com)

These tools can be removed if not needed for your implementation.
:::

### Supported Tools

The following tools are currently available:

#### Search & Research Tools
- **search**: Web search functionality using DuckDuckGo
- **tavily_search**: Enhanced search capabilities through Tavily
- **wikipedia**: Wikipedia information retrieval
- **arxiv**: Academic paper search on arXiv
- **pubmed**: Medical and life sciences literature search
- **browser**: Website content scraping and summarization
- **instagram_search**: Instagram-specific content search

#### File & System Tools
- **shell**: Shell command execution
- **python_repl**: Python code execution environment
- **read_file**: File content reader
- **list_directory**: Directory content listing

#### AI & Vision Tools
- **scene_explain**: Image content analysis
- **gpt4_vision**: Image analysis using GPT-4 Vision
- **dalle3**: Text-to-image generation
- **openai_embeddings**: Text embedding generation using OpenAI

## Adding New Tools

Tools can be extended by modifying `server/tools/tools.py`. The implementation follows these key structures:

1. **Argument Structure**: Each tool inherits from `pydantic.BaseModel`
2. **Tool Call Body**: Defines the tool's name and argument structure
3. **Mapping**: Tools are registered in two dictionaries:
   - `TOOL_ARGS_MAPPING`: Maps tools to their argument structures
   - `TOOLS`: Maps tools to their executable functions

### Implementation Example

```python
# Example tool definition
from pydantic import BaseModel

class SearchArgs(BaseModel):
    query: str

# Tool registration
TOOL_ARGS_MAPPING = {
    "search": SearchArgs
}

TOOLS = {
    "search": create_clusterai_tool(lambda args: perform_search(args.query))
}
```

:::tip
The `create_clusterai_tool` wrapper enables lambda functions to be defined as tools, supporting potential onchain tool definition.
:::

## Testing

To run the test suite:

```bash
pip3 install pytest
PYTHONPATH=src pytest tests
```

## File References

- Main server implementation: [`server/main.py`](./src/nexus_tools/server/main.py)
- Tools implementation: [`server/tools/tools.py`](./src/nexus_tools/server/tools/tools.py)