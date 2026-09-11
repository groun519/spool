# Spool

Spool preserves and retrieves the threads of conversations, decisions, and context across AI models.

It is a model-agnostic context and memory layer for long-running AI workflows. Raw sources remain the source of truth; searchable and structured memory is built on top of them, and only the context needed for the current task is retrieved.

## Why Spool

Long-running AI work eventually outgrows a single context window. Spool is intended to keep continuity without tying project memory to one chat, one model, or one provider.

```text
Conversations / Files / Git / Tool Events
                  |
                  v
                Spool
        raw sources + memory
                  |
        +---------+---------+
        |         |         |
     ChatGPT   Local LLM   Other agents
```

The first practical use case is continuity for long-running ChatGPT project work. The same storage layer is intended to remain usable later by local LLMs and multi-model agents.

## Principles

- **Raw sources are authoritative.** Summaries, facts, episodes, and decisions are derived data.
- **Model-agnostic by design.** Memory should survive model and provider changes.
- **Retrieve, do not preload.** Only relevant context should enter a model's active context window.
- **History is not overwritten.** Superseded decisions remain traceable to their original sources.
- **Private data stays local by default.** Conversation exports, databases, embeddings, and model files are not committed to the repository.
- **Start small.** The first milestone is reliable import and retrieval before richer agent memory is added.

## Initial Scope

The bootstrap version will focus on:

1. Importing ChatGPT conversation exports.
2. Preserving original messages and provenance.
3. Storing normalized data in SQLite.
4. Searching messages with SQLite FTS5.
5. Fetching surrounding conversation context.
6. Tracking project decisions and superseded decisions.

Later layers may add hybrid retrieval, episodic and semantic memory, entity relationships, agent state, skills, MCP/ChatGPT app integration, and local LLM integration.

## Planned Memory Layers

```text
Raw Sources
   |
   +-- Conversations
   +-- Documents
   +-- Git / Tool Events
   |
   v
Episodes
   |
   +-- Semantic Facts
   +-- Decisions
   +-- Procedures / Skills
   |
   v
Hybrid Retrieval
   |
   v
Context Builder
   |
   +-- ChatGPT
   +-- Local LLM
   +-- Other agents
```

## Repository vs. Local Data

This repository contains the implementation, schema, migrations, tests, and documentation.

Actual personal conversation data and generated memory databases should live outside Git history.

## Status

Early bootstrap / experimental.

## License

Apache License 2.0.
