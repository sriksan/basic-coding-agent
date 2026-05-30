# AI Code Assistant (Foundational Agentic AI Architecture)

A framework-free, production-ready implementation of a terminal-based AI Code Assistant built using the **official Google GenAI SDK** (`gemini-3.5-flash`). This codebase implements the industry-standard **ReAct (Reasoning + Acting)** loop, showcasing how to give large language models secure read/write capabilities on a local machine without high-level wrappers like LangChain or LangGraph.

---

## 🛠️ Deep-Dive Architectural Design

### 1. The Translation Manifest (Function Schemas)
Large Language Models do not speak Python syntax; they communicate natively via structured text schemas. This project leverages `types.FunctionDeclaration` blocks to build a semantic blueprint (using JSON Schema standards). Each utility exposes:
* **Strict Parameter Enforcements:** Hard typing variables using `types.Type.STRING` so the model always formats accurate parameter signatures.
* **Semantic Tool Selection:** Plain-English `description` fields that the LLM reads to determine *why* and *when* a custom tool should be invoked to fulfill a request.

### 2. The Agentic Pipeline Sequence
Instead of processing random, disconnected functions, the agent stacks these capabilities into a logical, multi-step dependency pipeline to handle complex engineering tasks:



1. **Observe (`get_files_info`):** Synthesizes folder context to locate files.
2. **Analyze (`get_file_content`):** Pulls safe, truncated character chunks into context memory.
3. **Modify (`write_file`):** Synthesizes fixes internally and overwrites scripts cleanly.
4. **Verify (`run_python_file`):** Executes code natively to capture `stdout` and runtime errors.

### 3. Sandbox Host Security Guardrails
Granting code execution or file system capabilities to an LLM introduces systemic risk. To eliminate path-traversal attacks (e.g., a model or malicious prompt requesting `../../../../etc/passwd`), this script enforces a defensive operating system layer:



* **Absolute Resolution:** Standardizes runtime locations using `os.path.abspath`.
* **Path Canonicalization:** Cleans relative shortcuts using `os.path.normpath`.
* **Common Path Boundaries:** Evaluates the highest shared directory via `os.path.commonpath`. If an evaluation falls outside the specified root directory, execution halts safely before firing the python file descriptor loop.

---

## 📦 Prerequisites & Installation

Ensure you have a modern Python environment installed (v3.10+ recommended).

1. **Clone or create the project directory:**
   ```bash
   mkdir basic-agent && cd basic-agent
   pip install google-genai python-dotenv
2. **Install dependencies:**
   ```bash
   pip install google-genai python-dotenv
3. **Set Up Authentication:**
   ```bash
   GEMINI_API_KEY=AIzaSyYourActualSecretKeyHere