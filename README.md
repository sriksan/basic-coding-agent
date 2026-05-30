# AI Code Assistant (Basic Agentic AI)

A lightweight AI Code Assistant built using the **official Google GenAI SDK** (`gemini-3.5-flash`). This project serves as a foundational step toward understanding Agentic AI, demonstrating how to securely format payload matrices for multi-turn conversations and read token usage metadata without relying on heavy external frameworks like LangChain or LangGraph.

Additionally, this project introduces the core principles of **Tool Use / Function Calling**, demonstrating how standard Python subsystems (such as the `os` module) are exposed to the LLM to safely interface with your local filesystem.

---

### The LLM "Hand & Brain" Pattern
1. **The Brain (LLM Node):** Structures text inputs into an explicit object matrix:
   `List` -> `Content [Role=user]` -> `Part [Text]`
2. **The Hand (File Toolkit):** To scale towards true autonomous agents, the LLM is paired with Python execution routines (like `get_files_info`). This routine implements strict **Path Traversal Protection** to safely analyze file dimensions without exposing sensitive root system directories.

---