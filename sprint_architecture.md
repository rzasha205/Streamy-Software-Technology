# Streamy Sprint Board Execution Lifecycle

This diagram illustrates the workflow of development tasks across the Streamy sprint board.

```mermaid
flowchart TD

%% Define Backlog Lane
subgraph Backlog [1. Backlog / Todo Pool]
T1["Issue #1: Model Behavior Flow"]
T2["Issue #2: Draft Structural Class Maps"]
T3["Issue #3: Design Relational Storage"]
T4["Issue #4: Compile Python Skeletons"]
end

%% Define Active Sprint Lane
subgraph ActiveSprint [2. Active Sprint / In Progress]
Active["🛠 Active Developer Sprint Work"]
end

%% Define Completed Work Lane
subgraph VerifiedDone [3. Done / Merged Production]
Merged["📦 Merged Base Code & Docs synced"]
end

%% Define Workflow Transitions
T1 -->|Pick Task| Active
Active -->|Code Review PR Approved| Merged