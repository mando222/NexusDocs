---
sidebar_position: 4
---

# Sui Event Listener

This module implements a blockchain event listener for handling LLM inference requests from Sui Move events. It processes `RequestForCompletionEvent` events and manages tool execution and completions.

## Configuration

The script accepts configuration via environment variables and command-line arguments:

```env
NODE_TYPE=TALUS_NODE  # or EXTERNAL_NODE
PACKAGE_ID=<your_package_id>
SUI_PRIVATE_KEY=<your_private_key>
MODEL_OWNER_CAP_ID=<your_model_owner_cap_id>
```

### Command Line Arguments

```bash
python event_listener.py \
  --rpc http://localhost:9000 \
  --ws ws://localhost:9000 \
  --packageid <package_id> \
  --privkey <private_key> \
  --modelownercapid <model_owner_cap_id> \
  --toolurl http://0.0.0.0:8080/tool/use
```

## Core Components

### Event Handler

The main event handler (`prompt_event_handler`) processes `RequestForCompletionEvent` events and:

1. Extracts event data including:
   - Model name
   - Prompt contents
   - Maximum tokens
   - Temperature
   - Cluster execution ID
2. Executes tool calls if specified
3. Processes LLM completions
4. Submits completions back to the blockchain

```python
async def prompt_event_handler(
    client: SuiClient,
    package_id: str,
    model_owner_cap_id: str,
    event: SubscribedEvent,
    tool_url: str,
) -> Any:
```

### Tool Execution

Tools are executed via the `call_use_tool` function:

```python
async def call_use_tool(name, args, url):
```

This function:
- Validates tool existence
- Constructs tool arguments
- Makes HTTP requests to the tool endpoint
- Returns tool execution results

### Event Processing Loop

The main event processing loop:

1. Fetches events using cursor-based pagination
2. Processes events sequentially
3. Updates cursor position
4. Handles error conditions
5. Implements backoff when no events are found

## Text Processing

The module includes text sanitization functionality via `sanitize_text`:

```python
def sanitize_text(text):
```

This function:
- Normalizes Unicode characters
- Handles special characters
- Ensures ASCII compatibility
- Normalizes quotation marks and dashes

## Error Handling

The module implements comprehensive error handling:

1. Tool execution errors
2. Event processing failures
3. Blockchain transaction errors
4. Network connectivity issues

## Dependencies

Required Python packages:
- `pysui`: Sui blockchain interaction
- `aiohttp`: Async HTTP requests
- `python-dotenv`: Environment variable management
- `unidecode`: Text normalization
- Additional requirements from the tools module

## Usage Example

Basic usage to start the event listener:

```bash
# Set required environment variables
export PACKAGE_ID="0x..."
export SUI_PRIVATE_KEY="your_private_key"
export MODEL_OWNER_CAP_ID="0x..."

# Start the listener
python event_listener.py
```

## Best Practices

1. **Error Handling**: Implement proper error handling and logging
2. **Configuration**: Use environment variables for sensitive data
3. **Monitoring**: Monitor event processing and completion submission
4. **Gas Management**: Ensure sufficient gas for transactions
5. **Backoff Strategy**: Implement appropriate waiting periods when no events are found

## Security Considerations

1. Protect private keys and sensitive configuration
2. Validate tool inputs and outputs
3. Implement rate limiting for tool calls
4. Monitor for unusual activity patterns
5. Handle sensitive data appropriately