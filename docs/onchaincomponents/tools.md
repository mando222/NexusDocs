---
sidebar_position: 7
---

# Tool Module

## Core Purpose
- Represents utilities and resources for agents
- Attached to tasks for additional functionality
- Can have side effects (e.g., external API calls)

## Main Structure

### Tool
```rust
struct Tool {
    name: String,            // Tool identifier
    args: vector<String>     // Tool parameters/arguments
}
```

## Key Functions

### Creation
```rust
new(name: String, args: vector<String>): Tool
```

### Accessors
```rust
get_name(&Tool): String
get_args(&Tool): vector<String>
```

## Key Features
- Tools are optional attachments to tasks
- Parameters must be set when creating the cluster
- Can interact with external systems
- Examples include:
  - Wiki searches
  - Smart contract calls
  - API integrations

## Module Function
This module serves as:
- A way to extend agent capabilities
- A bridge to external resources
- A parameter system for tool configuration
- A mechanism for side effects in task execution

## Design Philosophy
The module is intentionally simple but powerful:
- Minimal structure
- Flexible naming
- Vector-based arguments for versatility
- Copy and drop traits for easy reuse