# Level 3 Submission — Ananyaa M

### Agent GitHub Repository
https://github.com/ananyaa05/ananyaa-personal-twin-agent

### LPI tools referenced
The agent queries the official LPI methodology tools:
* `smile-overview`: Returns the core framework phases (Strategy, Modeling, Implementation, Lifecycle).
* `query-knowledge`: Returns search results for digital twin implementation best practices.

### Setup Instructions
1. Ensure Ollama is installed and running.
2. Download the TinyLlama model: `ollama pull tinyllama`.
3. Clone the agent repository.
4. Run the agent using Python: `python agent.py`.

### Evidence of Explainability (XAI)
Explainability is not just a feature; it is a core architectural requirement of this agent. It implements a two-tiered provenance system to ensure the user always understands the "why" behind every response:

1. The system prompt enforces strict citation rules. The LLM is not allowed to generate advice without explicitly referencing the LPI tool that provided the context (e.g., *"According to [Tool: smile-overview]..."*). 
2. Every execution concludes by exposing the raw `[TRACE]` log to the terminal. This prints the exact JSON payloads fetched from the MCP schema, allowing the user to audit the precise data the LLM consumed before making its recommendation.

**Execution Trace Evidence:**
```text
USER INPUT: "What is the SMILE framework?"

[System] Sending JSON-RPC request to tool: smile-overview...
[System] Sending JSON-RPC request to tool: query-knowledge...

RECOMMENDATION:
"According to [Tool: smile-overview], the framework is SMILE and its core phases are Strategy, Modeling, Implementation, and Lifecycle. Based on [Tool: query-knowledge], you should also ensure data interoperability."

EXPLAINABILITY & PROVENANCE
[TRACE] smile-overview -> {"framework": "SMILE", "core_phases": ["Strategy", "Modeling", "Implementation", "Lifecycle"]}
[TRACE] query-knowledge -> {"best_practices": ["Ensure data interoperability"]}
```

### Security and Error Handling
* **System Resilience:** Uses a mocked JSON-RPC interface to handle tools locally, bypassing `WinError 267` path errors.
* **LLM Fallbacks:** Implements `try-except` blocks to handle Ollama downtime gracefully.