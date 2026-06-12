---
name: mermaid-diagramming
description: Create Mermaid diagrams using the project's blue-gray theme. Use whenever the user asks to draw a diagram, create a flowchart, visualize a process, document architecture, or add any Mermaid diagram to a markdown file. Trigger on phrases like "draw a diagram", "create a flowchart", "visualize this", "add a mermaid diagram", "document the flow", "sequence diagram", "architecture diagram", or any request to diagram a process or system
---

# Mermaid Diagramming

Produce Mermaid diagrams.

## Rules

1. **One diagram per concept.** If a section needs multiple views, use separate fenced blocks with a heading for each.
2. **Keep labels short.** Node labels ≤ 6 words. Use subgraphs for grouping, not long labels.
3. **Decision nodes use `{...}` rhombus shape.** Action nodes use `[...]` rectangles. Terminal/IO nodes use `[/..../]` parallelograms.
4. **Left-to-right for pipelines, top-to-bottom for hierarchies.** Default to `LR` for data flow; `TD` for org charts, call trees, and phase sequences.

## Diagram Types

### Flowchart — processes and pipelines

```mermaid
flowchart LR
    A[Input] --> B{Valid?}
    B -->|yes| C[Process]
    B -->|no| D[Reject]
    C --> E[Output]
```

### Sequence — interactions between actors/services

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server
    participant D as Database
    C->>S: POST /resource
    S->>D: INSERT row
    D-->>S: OK
    S-->>C: 201 Created
```

### Graph with subgraphs — architecture layers

```mermaid
flowchart TD
    subgraph API["API Layer"]
        R[Router]
        M[Middleware]
    end
    subgraph Domain["Domain Layer"]
        S[Service]
        E[Entities]
    end
    subgraph Infra["Infrastructure"]
        DB[(Database)]
        Cache[(Cache)]
    end
    R --> M --> S --> E
    S --> DB
    S --> Cache
```

### State diagram — lifecycle / state machine

```mermaid
stateDiagram-v2
    [*] --> Pending
    Pending --> Running : start
    Running --> Passed : success
    Running --> Failed : error
    Passed --> [*]
    Failed --> [*]
```

## Procedure

1. Identify the diagram type that best fits the concept (flowchart, sequence, state, ER, etc.).
2. Draft the structure — nodes, edges, labels — before writing Mermaid syntax.
3. Open the ```` ```mermaid ```` block.
4. Write the diagram type declaration on line 2.
5. Verify the diagram is syntactically valid (balanced brackets, no duplicate node IDs).

## Persist to file

Always persist to a new file unless asked to add to and existing file. Use serena for writing to disk

1. **Slugify** the feature name: lowercase, replace spaces with hyphens, strip special characters. ("User Login with MFA" → `user-login-with-mfa`)
2. **Create** `docs/diagrams/` if missing.
3. **Check** whether `docs/diagrams/<slug>.md` already exists. If yes, ask: overwrite or create a versioned file (`<slug>-v2.md`)?

## Adding a diagram to an existing file

When inserting a diagram into an existing markdown file:

1. Read the file first to understand the document structure and find the right insertion point.
2. Use a second-level heading (`##`) above the diagram block to name the concept.



