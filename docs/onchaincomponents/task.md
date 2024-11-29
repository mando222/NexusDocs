---
sidebar_position: 6
---

# Task Module

## Core Purpose
- Represents individual work units assigned to agents
- Each task is bound to a specific agent in a cluster

## Main Structures

### TaskBlueprint
```rust
struct TaskBlueprint {
    name: TaskName,           // Unique identifier within cluster
    agent: AgentName,         // Assigned agent
    description: String,      // Task description
    expected_output: String,  // Expected result
    prompt: String,          // Instructions for the agent
    context: String,         // Additional context
    tool: Option<Tool>       // Optional tool for execution
}
```

### TaskState
```rust
struct TaskState {
    name: TaskName,
    agent_name: AgentName,
    input_context: String,
    status: String,          // idle/running/success
    prompt: Option<ID>,
    response: String
}
```

## Key Functions

### Creation
- `new()`: Creates basic TaskBlueprint
- `new_with_tool()`: Creates TaskBlueprint with attached tool
- `new_state()`: Creates initial TaskState
- `into_name()`: Converts string to TaskName

### State Management
- `attach_tool()`: Adds tool to task
- `set_state_status()`: Updates task status
- `set_state_response()`: Sets task response

## Status States
- `idle`: Task not started
- `running`: Task in progress
- `success`: Task completed

## Accessors
- Getters for all task properties
- Status check helpers (is_idle, is_running, is_successful)
- Package-protected setters for state management

## Module Function
This module serves as:
- A blueprint for work to be done
- A state tracker for ongoing tasks
- A way to assign work to specific agents
- A system for monitoring task progress

## Architecture
The module demonstrates clear separation between:
- Task definition (Blueprint)
- Task execution state (State)
- Task identification (Name)