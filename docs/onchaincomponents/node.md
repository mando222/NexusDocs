---
sidebar_position: 5
---

# Node Module

## Core Purpose
Represents a computational unit capable of running AI models, following the hierarchy:
Node → Model → Agent → Cluster

## Main Structure

### Node
```rust
struct Node {
    id: UID,
    name: String,                    // Node identifier
    node_type: String,              // Type of computational unit
    gpu_memory: u64,                // Available GPU memory
    image_hash: vector<u8>,         // Hash of the node's image
    external_arguments: vector<u8>   // Additional configuration
}
```

## Key Features
- Owned object design (not shared)
- Basis for model creation
- Represents physical or virtual compute resources
- Tracks hardware specifications

## Functionality
`create()` creates new Node with:
- Name and type
- GPU memory specifications
- Image configuration
- External arguments

## Events
### NodeCreatedEvent
- Emitted when new nodes are registered
- Includes node ID and name

## Module Function
This module serves as:
- A registry for compute resources
- The foundation of the system's hardware layer
- A way to track and manage computational capabilities
- The starting point for model deployment

## Key Observations
The module is notably simpler than others because it represents base infrastructure:
- More straightforward than agent/model modules
- Focused on hardware representation
- Currently lacks advanced ownership patterns (noted as TODO)
- Foundational for the rest of the system