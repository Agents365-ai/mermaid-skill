---
name: mermaid-skill
description: Use when user requests diagrams, flowcharts, sequence diagrams, class diagrams, ER diagrams, architecture charts, or visualizations. Also use proactively when explaining systems with 3+ components, APIs, data flows, or class hierarchies. Generates .mmd files and exports to PNG/SVG/PDF locally using mmdc CLI.
---

# Mermaid Diagrams

## Overview

Generate `.mmd` text files and export to PNG/SVG/PDF locally using `mmdc` (Mermaid CLI).

**Key advantage:** Text-based syntax with **fully automatic layout** — no x/y coordinates needed.

**Supported formats:** PNG, SVG, PDF
**Supported themes:** default, dark, neutral, forest, base

## When to Use

**Explicit triggers:** user says "diagram", "flowchart", "sequence diagram", "class diagram", "ER diagram", "state machine", "visualize", "画图", "架构图", "流程图", "git graph"

**Proactive triggers:**
- Explaining a system with 3+ interacting components
- Describing API flows, authentication sequences, message passing
- Showing class hierarchies or database schemas
- Illustrating state machines or lifecycle flows

**Skip when:** a simple list or table suffices, or user is in a quick Q&A flow

## Prerequisites

```bash
# Install mmdc globally
npm install -g @mermaid-js/mermaid-cli

# Verify
mmdc --version
```

If Chromium download fails during install:
```bash
PUPPETEER_SKIP_DOWNLOAD=true npm install -g @mermaid-js/mermaid-cli
```

## Workflow

1. **Check deps** — verify `mmdc --version` succeeds
2. **Pick diagram type** — choose the most appropriate type from the table below
3. **Generate** — write `.mmd` file to disk (output dir same as user's working dir)
4. **Export** — run `mmdc` to produce PNG (default), SVG, or PDF
5. **Report** — tell user the output file paths (source + image)

## Diagram Types

| Type | Keyword | Use for |
|------|---------|---------|
| Flowchart (top-down) | `flowchart TD` | processes, decision trees, pipelines |
| Flowchart (left-right) | `flowchart LR` | data flows, horizontal pipelines |
| Sequence | `sequenceDiagram` | API calls, protocol flows, message passing |
| Class | `classDiagram` | OOP models, data structures |
| ER | `erDiagram` | database schemas |
| State | `stateDiagram-v2` | state machines, lifecycle |
| Gantt | `gantt` | project timelines |
| Pie | `pie` | proportions, distributions |
| Git Graph | `gitGraph` | branch strategies |
| C4 Context | `C4Context` | high-level architecture |
| Mind Map | `mindmap` | topic breakdowns |

## Syntax Reference

### Flowchart

```
flowchart TD
  A[Client] --> B[API Gateway]
  B --> C[Auth Service]
  B --> D[Order Service]
  D --> E[(Order DB)]
  C --> F[(User DB)]

  subgraph Services
    C
    D
  end
```

**Node shapes:**
- `[text]` — rectangle
- `(text)` — rounded rectangle
- `{text}` — diamond (decision)
- `[(text)]` — cylinder (database)
- `[[text]]` — subroutine
- `((text))` — circle

**Arrow types:**
- `-->` — arrow
- `---` — line (no arrow)
- `-.->` — dashed arrow
- `==>` — thick arrow
- `-->|label|` — arrow with label

### Sequence Diagram

```
sequenceDiagram
  participant C as Client
  participant G as API Gateway
  participant A as Auth Service
  participant D as Database

  C->>G: POST /login
  G->>A: validate(credentials)
  A->>D: query user
  D-->>A: user record
  A-->>G: 200 OK + token
  G-->>C: {token: "..."}
```

**Arrow types:**
- `->>` — solid arrow (request)
- `-->>` — dashed arrow (response)
- `-x` — async message with X
- `activate/deactivate` — show activation boxes

### Class Diagram

```
classDiagram
  class User {
    +String name
    +String email
    +String passwordHash
    +login() bool
    +logout()
  }
  class Order {
    +int id
    +Date createdAt
    +float total
    +place()
    +cancel()
  }
  class Product {
    +int id
    +String name
    +float price
  }

  User "1" --> "*" Order : places
  Order "*" --> "*" Product : contains
```

### ER Diagram

```
erDiagram
  USER ||--o{ ORDER : places
  ORDER ||--|{ ORDER_ITEM : contains
  PRODUCT ||--o{ ORDER_ITEM : "included in"

  USER {
    int id PK
    string name
    string email
    datetime created_at
  }
  ORDER {
    int id PK
    int user_id FK
    float total
    string status
  }
  ORDER_ITEM {
    int order_id FK
    int product_id FK
    int quantity
  }
```

### State Diagram

```
stateDiagram-v2
  [*] --> Pending
  Pending --> Processing : payment_received
  Processing --> Shipped : packed
  Shipped --> Delivered : received
  Processing --> Cancelled : cancel
  Pending --> Cancelled : cancel
  Delivered --> [*]
  Cancelled --> [*]
```

### Git Graph

```
gitGraph
  commit id: "Initial commit"
  branch develop
  checkout develop
  commit id: "Add feature A"
  commit id: "Add feature B"
  checkout main
  merge develop id: "Release v1.0"
  branch hotfix
  checkout hotfix
  commit id: "Fix critical bug"
  checkout main
  merge hotfix id: "Hotfix v1.0.1"
```

## Export Commands

```bash
# Check CLI
mmdc --version

# PNG (recommended: 2048px wide, white background)
mmdc -i diagram.mmd -o diagram.png -w 2048 --backgroundColor white

# PNG with theme
mmdc -i diagram.mmd -o diagram.png -w 2048 --backgroundColor white --theme neutral
# Themes: default | dark | neutral | forest | base

# SVG
mmdc -i diagram.mmd -o diagram.svg

# PDF
mmdc -i diagram.mmd -o diagram.pdf
```

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| `mmdc` not found | Run `npm install -g @mermaid-js/mermaid-cli` |
| Chromium download fails during install | Use `PUPPETEER_SKIP_DOWNLOAD=true npm install -g @mermaid-js/mermaid-cli` |
| Wrong arrow in sequence diagram | Use `->>` for requests, `-->>` for responses; `-->` is for flowcharts |
| Node label with special chars (`:`, `"`) | Wrap in quotes: `A["Label: value"]` |
| Sequence participant order wrong | Declare `participant` in desired order explicitly at the top |
| Output blank or very small | Add `-w 2048` flag to set width |
| Subgraph name with spaces | Wrap in quotes: `subgraph "My Service Layer"` |
| Too many nodes in one diagram | Split into multiple diagrams or use subgraphs to group |
