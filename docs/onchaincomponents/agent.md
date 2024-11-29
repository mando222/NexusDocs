---
sidebar_position: 2
---

# Agent Module

## Overview
This is a breakdown of the `talus::agent` module which forms a core part of the Talus system.

## Agent System Overview
An agent is a specialized entity that works within a Cluster setup. The system follows a clear hierarchy:
- Node → Model → Agent → Cluster

### Agent Creation Methods
There are two ways to create agents:
1. Cluster owners can create blueprints directly
2. Model providers can create shared Agent objects

## Core Components

### Main Structures
1. **Agent**
   - Core entity that other clusters can copy blueprints from

2. **AgentBlueprint**
   - Defines the agent's work and characteristics including:
     - Name (unique identifier)
     - Role
     - Goal
     - Backstory
     - Model information

3. **AgentOwnerCap**
   - Represents ownership and permissions for the agent

4. **AgentState**
   - Tracks the agent's state in a cluster execution

5. **AgentRosterPromise**
   - Allows cluster owners to add agents to their setup

### Key Functions
- `create_from_blueprint`: Creates a new Agent from a blueprint
- `create_and_share`: Creates and shares an agent in a more convenient way
- `issue_roster_promise`: Allows agent owners to create promises for cluster owners
- `clone_owner_cap`: Creates additional owner capabilities for the same agent

### Security Features
- Built-in ownership verification
- Protected access to sensitive components
- Event emission for tracking important actions

### Access Control
- Package-protected functions for internal use
- Public functions for general interaction
- Ownership verification through AgentOwnerCap

### Events
- `AgentCreatedEvent`: Emitted when a new agent is created
- `AgentRosterPromiseIssuedEvent`: Emitted when a roster promise is issued

## Summary
This module functions as a smart contract that manages AI agents in a decentralized system, where:
- Agents can be created and shared
- Ownership is clearly tracked
- Permissions are carefully managed
- Different clusters can use the same agent through a promise system