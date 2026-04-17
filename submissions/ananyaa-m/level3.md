# Level 3 Submission — Ananyaa M

### **GitHub Repository**
https://github.com/ananyaa05/ananyaa-personal-twin-agent

### **LPI Tools Integrated**
The agent is hardcoded to orchestrate the following LPI tools:
* `query_knowledge` (Primary tool for retrieving pending academic tasks and lab schedules)
* `log_mood_state` (Secondary tool for emotional state analysis)
* `smile_overview` (Primary tool for monitoring user energy levels and physical status)
* `get_creative_log` (Hobby engagement tracking)
* `get_exercise_log` (Physical activity metrics)

### **Setup Instructions**
To run this agent locally, follow these steps:
1. Ensure **Ollama** is installed and running.
2. Download the **TinyLlama** model: `ollama pull tinyllama`.
3. Clone the agent repository.
4. Run the agent using Python: `python agent.py`.

### **Explainability Evidence**
```text
USER INPUT: "I'm exhausted from the Amity CSE lab."

[LPI_SYSTEM_CALL] Calling tool: smile_overview
[LPI_SYSTEM_CALL] Calling tool: query_knowledge

RECOMMENDATION:
"Based on [Tool: smile_overview] (Energy: 3) and your current [Tool: query_knowledge] status, I recommend immediate rest over further coding."
```

### **Security and Error Handling**
The agent includes robust error handling to manage empty user inputs and potential LLM connection failures (Ollama downtime). It sanitizes inputs to prevent prompt injection and ensures a valid response is generated before displaying the recommendation. It also includes input validation to prevent hallucination if LPI data is missing.