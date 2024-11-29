---
sidebar_position: 3
---

# Cluster Module

## Overview
This module represents the core functionality for managing groups of AI agents working together.

## Cluster System Overview
- A Cluster is a group of agents collaborating toward a common goal
- Each concrete goal is managed through a `ClusterExecution`
- Flow: Node → Models → Agents → Clusters

## Core Components

### Main Structures
1. **Cluster**
   - Core container for a group of agents and their tasks
   
2. **ClusterBlueprint**
   - Defines the cluster's configuration:
     - Name and description
     - Collection of tasks
     - Map of agents (name → blueprint)
     
3. **ClusterExecution**
   - Manages an active execution instance:
     - Tracks current status
     - Maintains task states
     - Handles memory/messaging
     - Records user input and responses

### Key Functions
- `create()`: Creates a new empty Cluster
- `execute()`: Starts a new ClusterExecution
- `submit_completion_*()`: Various methods for submitting task completions:
  - As node owner
  - As model owner
  - As cluster owner
- `add_agent()`: Adds new agents to the cluster
- `add_task()`: Adds new tasks to the cluster

### Memory & Context Management
- Maintains a history of past messages
- Uses last 5 messages for context in new prompts
- Tracks task completion and responses

### Events System
- `ClusterCreatedEvent`: When new clusters are created
- `ClusterExecutionCreatedEvent`: When executions start
- `ClusterResponseEvent`: When responses are ready
- `AgentAddedToClusterEvent`: When agents join clusters

## Task Execution Flow
1. User creates a cluster
2. Agents and tasks are added
3. User initiates execution with input
4. System processes tasks sequentially
5. Results are stored and events emitted

## Module Function
This module serves as an orchestration layer that:
- Manages multiple AI agents working together
- Handles task scheduling and execution
- Maintains conversation context and memory
- Controls permissions and ownership
- Manages the flow of information between components