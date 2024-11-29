---
sidebar_position: 3
---

# OffChain LLM Inference

The OffChain module provides a simple interface for making LLM inference requests to a local or remote LLM server.

## Configuration

The module uses environment variables for configuration:

```env
LLM_ASSISTANT_URL=http://localhost:8080/predict  # Default URL if not specified
```

## Usage

### Basic Example

```python
from offchain import OffChain

# Initialize the OffChain instance
off_chain = OffChain()

# Make an inference request
completion = off_chain.process(
    prompt="Write python script that prints the numbers 1 to 100",
    model_name="tinyllama",
    max_tokens=3000,
    temperature=0.3
)

print(completion)
```

### Parameters

The `process` method accepts the following parameters:

- `prompt` (str): The input text prompt for the LLM
- `model_name` (str): The name of the model to use (e.g., "tinyllama")
- `max_tokens` (int): Maximum number of tokens to generate
- `temperature` (float): Controls randomness in the output (0.0 to 1.0)

## API Details

### OffChain Class

```python
class OffChain:
    def process(
        self, 
        prompt: str, 
        model_name: str, 
        max_tokens: int, 
        temperature: float
    ) -> str:
```

The `process` method handles the HTTP request to the LLM server and returns the generated completion.

#### Request Format

The API expects a JSON payload with the following structure:

```json
{
    "prompt": "Your prompt text",
    "model": "model_name",
    "max_tokens": 3000,
    "temperature": 0.3
}
```

#### Response Format

The API returns a JSON response containing the completion:

```json
{
    "completion": "Generated text response"
}
```

## Error Handling

The module includes comprehensive error handling for API requests:

- Automatically raises exceptions for HTTP errors
- Includes detailed error messages with response content when available
- Wraps errors in a custom exception with a 500 status code

Example error handling:

```python
try:
    completion = off_chain.process(prompt, model_name, max_tokens, temperature)
except Exception as e:
    print(f"Error: {e}")
```

## Dependencies

The module requires the following Python packages:

- `requests`: For making HTTP requests
- `python-dotenv`: For loading environment variables

Install dependencies using:

```bash
pip install requests python-dotenv
```

## Best Practices

1. **Environment Variables**: Always use environment variables for configuration rather than hardcoding values.
2. **Error Handling**: Implement try-catch blocks around API calls to handle potential failures gracefully.
3. **Temperature**: Use lower temperature values (0.0-0.3) for more deterministic outputs, higher values (0.5-1.0) for more creative responses.
4. **Token Limits**: Set appropriate `max_tokens` based on your model and use case to avoid unnecessary computation.