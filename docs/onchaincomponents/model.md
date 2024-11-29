---
sidebar_position: 4
---
# Model Module

## Core Purpose
The module represents software running on a Node, following the hierarchy:
Node → Model → Agent → Cluster

## Main Structures

### Model (Shared Object)
- Core container for model information
- Used to create agents
- Contains `ModelInfo`

### ModelInfo
- id: Model identifier
- node: Node running the model
- name: Model name
- model_hash: Unique identifier for model version
- capacity: Processing capacity
- max_context_length: Maximum input context
- token_price: Cost per token
- description: Model description
- family: Model family (e.g., GPT, BERT)
- vendor: Provider name
- Various flags:
  - is_fine_tuned
  - is_open_source

### ModelOwnerCap
- Represents ownership rights
- Controls model updates and management
- Can issue inference promises

## Key Functions

### Creation and Management
- `create()`: Creates new Model
- `issue_inference_promise()`: Allows creation of agents
- `redeem_inference_promise()`: Converts promise to ModelInfo
- `clone_owner_cap()`: Creates additional owner capabilities

## Permission System
- Owner capabilities control model management
- Inference promises control agent creation
- Model information can only be accessed with proper permissions

## Events
- `ModelCreatedEvent`: When new models are registered
- `ModelInferencePromiseIssuedEvent`: When new promises are created

## Testing Support
- Includes mock data generators
- Test-only helper functions
- Simple model creation for testing

## Module Function
This module serves as:
- A registry for AI models
- A permission management system for model usage
- A way to track model capabilities and characteristics
- A bridge between nodes (hardware) and agents (usage)