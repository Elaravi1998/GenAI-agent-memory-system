# 🧠 Agent Memory System

A practical **Generative AI Agent Memory System** built with Python and Jupyter Notebook.

This project demonstrates how an AI agent can move beyond simple conversation history and maintain **short-term memory, long-term memory, user preferences, project knowledge, semantic retrieval, memory consolidation, and memory-aware responses**.

The notebook provides a foundation for evolving the system into a production-grade memory architecture using **LangGraph, LangChain, vector databases, PostgreSQL/pgvector, Qdrant, Redis, MCP, and persistent storage**.

---

## 🚀 Project Overview

A basic chatbot typically works like this:

```text
User
 ↓
Conversation History
 ↓
LLM
 ↓
Response
```

An agent with memory works differently:

```text
User
 ↓
Current Conversation
 ↓
Memory Manager
 ├── Short-Term Memory
 ├── Long-Term Memory
 ├── User Preferences
 ├── Projects / Goals
 └── Relevant Past Knowledge
          ↓
    Memory Retrieval
          ↓
    Context Builder
          ↓
       LLM Agent
          ↓
   Memory-Aware Response
```

The objective is to build an AI agent that can decide:

> **What should I remember? → How important is it? → Where should it be stored? → When should I retrieve it? → Should it be updated or forgotten?**

---

# ✨ Key Features

## 🧠 1. Short-Term Memory

Maintains recent conversation context.

Example:

```text
User:
I am building an AI interview assistant.

User:
I prefer Python and React.

Assistant:
Understood.
```

The agent can use the recent conversation when responding to subsequent messages.

---

## 💾 2. Long-Term Memory

Stores useful information that should remain available beyond the current conversation.

Examples:

```text
User prefers Python for AI projects.
User is working on an AI interview assistant.
User prefers MongoDB for some projects.
User is building a GenAI portfolio.
```

Unlike simple chat history, these memories can be retrieved later based on relevance.

---

## 👤 3. User Preference Memory

The system can store stable preferences such as:

```text
Programming language preference
Technology preferences
Project preferences
Workflow preferences
Communication preferences
```

This allows future responses to be personalized without replaying the entire conversation history.

---

## 📝 4. Automatic Memory Extraction

The LLM analyzes conversation content and identifies information that may be useful for future interactions.

```text
Conversation
     ↓
Memory Extraction
     ↓
Candidate Memories
     ↓
Importance Assessment
     ↓
Safety Validation
     ↓
Memory Store
```

The extraction logic is instructed not to store:

* 🔐 API keys
* 🔑 Passwords
* 💳 Financial credentials
* 🚫 Highly sensitive information
* 🗑️ Temporary conversation details
* 🧠 Unsupported assumptions

---

# 🔎 5. Semantic Memory Retrieval

The system retrieves memories relevant to the current user query.

Example:

```text
Stored Memory:
"The user prefers Python for AI projects."

User:
"What programming language should I use for my next AI project?"
```

The memory retrieval system identifies the relevant preference and provides it to the LLM.

The current notebook includes a lightweight similarity implementation for demonstration.

A production system can replace it with:

* Qdrant
* ChromaDB
* FAISS
* Pinecone
* Weaviate
* PostgreSQL + pgvector
* MongoDB Atlas Vector Search

---

# 🔄 6. Memory Consolidation

Repeated or similar memories should not create unlimited duplicates.

Example:

```text
Memory 1:
User prefers Python.

Memory 2:
User generally uses Python for AI development.
```

Instead of storing both independently, the system can consolidate them into a stronger memory.

```text
New Memory
    ↓
Compare Existing Memories
    ↓
Similar?
 ┌──┴──┐
Yes    No
 ↓      ↓
Update  Create
```

---

# ✏️ 7. Memory Updates

Memory should be changeable.

For example:

```text
Old:
User prefers MongoDB.

New:
User has migrated the project to PostgreSQL.
```

The system can update the relevant memory rather than permanently keeping outdated information.

---

# 🗑️ 8. Memory Deletion

The project provides explicit memory management operations.

```text
List Memories
     ↓
Inspect Memory
     ↓
Update Memory
     ↓
Delete / Forget Memory
```

This is important for building user-controlled AI systems.

---

# 🤖 Memory-Aware AI Agent

The central workflow is:

```text
                 User Message
                      │
                      ▼
              ┌───────────────┐
              │ Current Intent│
              └───────┬───────┘
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
 Recent Conversation       Long-Term Retrieval
          │                       │
          └───────────┬───────────┘
                      ▼
                Context Builder
                      │
                      ▼
                   LLM Agent
                      │
                      ▼
                 AI Response
                      │
                      ▼
                Memory Update
```

---

# 🏗️ Architecture

```text
                       👤 User
                         │
                         ▼
                  💬 Conversation
                         │
                         ▼
                 🧠 Memory Manager
                         │
             ┌───────────┼───────────┐
             ▼           ▼           ▼
        Short-Term    Extraction   Retrieval
          Memory         │           │
             │           ▼           │
             │      Candidate       │
             │       Memories       │
             │           │           │
             └───────────┼───────────┘
                         ▼
                   💾 Memory Store
                         │
                         ▼
                  🧠 Context Builder
                         │
                         ▼
                       LLM
                         │
                         ▼
                 🤖 Final Response
```

---

# 🧩 Memory Types

A production system can divide memory into multiple categories.

## 🟢 Working Memory

Information required for the current task.

Examples:

```text
Current question
Current tool result
Current workflow state
Recent messages
```

---

## 🔵 Episodic Memory

Previous experiences and interactions.

Examples:

```text
Previous project discussion
Previous task
Previous decision
Previous troubleshooting session
```

---

## 🟣 Semantic Memory

Stable knowledge about the user or project.

Examples:

```text
User prefers Python.
Project uses MongoDB.
Application uses React.
```

---

## 🟠 Procedural Memory

Information about how the agent should perform a task.

Examples:

```text
Always validate generated code.
Run tests before finalizing.
Use a specific API workflow.
Follow project coding standards.
```

---

# 🛠️ Technology Stack

| Technology             | Purpose                                   |
| ---------------------- | ----------------------------------------- |
| 🐍 Python              | Core implementation                       |
| 📓 Jupyter Notebook    | Development environment                   |
| 🧠 LLM                 | Memory extraction and response generation |
| 🌐 OpenRouter          | LLM API                                   |
| 🔗 OpenAI Python SDK   | API integration                           |
| 🔐 python-dotenv       | Environment configuration                 |
| 📦 Pydantic            | Data models and validation                |
| 🔎 Vector Database     | Future semantic memory                    |
| 🔗 LangGraph           | Future agent orchestration                |
| 🦜 LangChain           | Future LLM framework integration          |
| 🔌 MCP                 | Future external memory/tool integration   |
| 🗄️ PostgreSQL / Redis | Future persistent memory                  |

---

# ⚙️ Installation

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/<your-username>/agent-memory-system.git

cd agent-memory-system
```

---

## 2️⃣ Create Virtual Environment

### Windows

```bash
python -m venv .venv
```

```bash
.venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv .venv
```

```bash
source .venv/bin/activate
```

---

## 3️⃣ Install Dependencies

```bash
pip install openai python-dotenv pydantic numpy jupyter
```

---

# 🔐 API Configuration

Create a `.env` file:

```env
OPENROUTER_API_KEY=your_openrouter_api_key
OPENROUTER_MODEL=openai/gpt-4.1-mini
```

⚠️ **Never commit `.env` or API keys to GitHub.**

Recommended `.gitignore`:

```gitignore
.env
.venv/
__pycache__/
.ipynb_checkpoints/
```

---

# ▶️ Running the Notebook

Start Jupyter:

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

Open:

```text
Agent_Memory_System.ipynb
```

Run the notebook cells from top to bottom.

---

# 🧪 Suggested Experiments

## Experiment 1 — Preference Memory

Tell the system:

```text
I prefer Python for AI projects.
```

Then later ask:

```text
Which programming language should I use for my AI project?
```

The agent should retrieve the relevant preference.

---

## Experiment 2 — Project Memory

Store:

```text
I am currently building an AI interview assistant.
```

Later ask:

```text
What AI project am I currently working on?
```

The agent should retrieve the project memory.

---

## Experiment 3 — Memory Update

First:

```text
I use MongoDB for my project.
```

Later:

```text
I migrated the project to PostgreSQL.
```

The memory manager should eventually represent the latest state instead of accumulating contradictory duplicates.

---

## Experiment 4 — Irrelevant Memory

Add several unrelated memories.

Then ask a specific question and verify that only relevant memories are retrieved.

---

## Experiment 5 — Privacy

Provide something resembling:

```text
OPENROUTER_API_KEY=...
```

The memory extraction layer should reject sensitive credentials instead of storing them.

---

# 🚀 Production Architecture

The notebook can evolve into:

```text
                 🌐 React / Next.js
                         │
                         ▼
                    ⚡ FastAPI
                         │
                         ▼
                🤖 LangGraph Agent
                         │
       ┌─────────────────┼─────────────────┐
       ▼                 ▼                 ▼
 Working Memory     Memory Manager       Tools
       │                 │                 │
     Redis              │                MCP
                         │
                ┌────────┴────────┐
                ▼                 ▼
          PostgreSQL          Vector DB
          / pgvector       / Qdrant etc.
                │                 │
                └────────┬────────┘
                         ▼
                      🧠 LLM
```

---

# 🔗 LangGraph Integration

The memory system can become part of a stateful LangGraph agent.

```text
START
  │
  ▼
Intent Detection
  │
  ▼
Memory Retrieval
  │
  ▼
Planner
  │
  ▼
Tool / Agent Execution
  │
  ▼
Response Generation
  │
  ▼
Memory Extraction
  │
  ▼
Memory Consolidation
  │
  ▼
END
```

This allows memory to become part of the agent's workflow rather than simply being injected into a prompt.

---

# 🔌 MCP Integration

The next version can expose memory operations as MCP tools.

Potential tools:

```text
memory_search()
memory_add()
memory_update()
memory_delete()
memory_list()
memory_summarize()
```

Architecture:

```text
                  AI Agent
                     │
                     ▼
                    MCP
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
     Search Memory  Add Memory  Update Memory
          │          │          │
          └──────────┼──────────┘
                     ▼
                Memory Store
```

---

# 🧠 Advanced Memory Features

Future versions can implement:

### 🕒 Memory Decay

Older memories can gradually receive lower retrieval priority.

### 🎯 Importance Scoring

Rank memories according to usefulness.

### 🔢 Confidence Scoring

Track how confidently a memory was extracted.

### 🔄 Memory Reflection

Combine multiple memories into higher-level knowledge.

### 🧹 Memory Cleanup

Detect stale or duplicated memories.

### ⚡ Hybrid Retrieval

Combine:

```text
Keyword Search
      +
Semantic Search
      +
Recency
      +
Importance
      +
User Context
```

---

# 📊 Memory Evaluation

A production memory system should be evaluated.

| Metric                    | Description                                 |
| ------------------------- | ------------------------------------------- |
| 🎯 Retrieval Precision    | Are retrieved memories relevant?            |
| 🔎 Retrieval Recall       | Are important memories being found?         |
| 🧠 Memory Usefulness      | Does memory improve responses?              |
| 🔄 Update Accuracy        | Are changed facts updated correctly?        |
| 🗑️ Forget Accuracy       | Are requested memories removed?             |
| 🚫 Sensitive Data Leakage | Are secrets prevented from entering memory? |
| ⏱️ Retrieval Latency      | How quickly is memory retrieved?            |
| 💰 Token Cost             | How much context is sent to the LLM?        |
| 📉 Stale Memory Rate      | How often does outdated information remain? |

---

# 🛡️ Privacy & Safety

Agent memory introduces important security considerations.

A production implementation should include:

* 🔐 Sensitive-data filtering
* 🔑 Secret detection
* 👤 User-level memory isolation
* 🗑️ User-controlled deletion
* 🧾 Memory audit logs
* 🚫 Prompt-injection protection
* 🔒 Access controls
* 🧹 Stale-memory cleanup
* 🎯 Confidence tracking

Never treat every piece of conversation as something that should automatically become permanent memory.

---

# 📁 Project Structure

Initial repository:

```text
agent-memory-system/
│
├── 📓 Agent_Memory_System.ipynb
├── 📄 README.md
├── 🔐 .env.example
├── 🚫 .gitignore
└── 📜 LICENSE
```

Future production structure:

```text
agent-memory-system/
│
├── app/
│   ├── memory/
│   │   ├── short_term.py
│   │   ├── long_term.py
│   │   ├── retrieval.py
│   │   ├── consolidation.py
│   │   └── policies.py
│   │
│   ├── agents/
│   ├── tools/
│   ├── mcp/
│   ├── rag/
│   └── api/
│
├── frontend/
├── notebooks/
│   └── Agent_Memory_System.ipynb
│
├── tests/
├── docs/
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

---

# 🗺️ Roadmap

```text
✅ Phase 1 — Notebook Prototype
        │
        ▼
🔄 Phase 2 — Persistent Memory
        │
        ▼
🔄 Phase 3 — Embedding-Based Retrieval
        │
        ▼
🔄 Phase 4 — Vector Database
        │
        ▼
🔄 Phase 5 — Memory Consolidation
        │
        ▼
🔄 Phase 6 — LangGraph Integration
        │
        ▼
🔄 Phase 7 — MCP Memory Tools
        │
        ▼
🔄 Phase 8 — Memory Evaluation
        │
        ▼
🚀 Phase 9 — Production Agent Memory Platform
```

---

# 🎯 Learning Outcomes

By completing this project, you will gain practical experience with:

* 🧠 Agent memory architecture
* 💬 Conversational state
* 💾 Long-term memory
* 🔎 Semantic retrieval
* 📝 LLM-based memory extraction
* 🔄 Memory consolidation
* 🎯 Importance scoring
* 🔐 Memory safety
* 🗑️ Memory lifecycle management
* 🔗 LangGraph
* 📚 Vector databases
* 🔌 MCP
* 🤖 Agentic AI architecture
* 📊 Memory evaluation
* 🚀 Production GenAI system design

---

# 🌟 Project Vision

The ultimate objective is not simply to create a chatbot with chat history.

The objective is to create an AI agent that can intelligently manage its own useful knowledge about users and projects:

```text
          💬 Conversation
                 │
                 ▼
        🧠 Should I remember?
                 │
                 ▼
          🎯 Importance?
                 │
                 ▼
           🔐 Is it safe?
                 │
                 ▼
            💾 Store
                 │
                 ▼
          🔎 Retrieve Later
                 │
                 ▼
           🔄 Update
                 │
                 ▼
            🗑️ Forget
```

> 🚀 **From Chat History → Intelligent Agent Memory → Production Memory Platform**

---

# 👨‍💻 Author

**Elavarasu Ravi**

AI / GenAI Engineer | Full-Stack Developer

---

# ⭐ Support

If you find this project useful, consider giving the repository a ⭐ and extending it with your own **LangGraph, RAG, MCP, vector memory, and multi-agent capabilities**.

#GenAI #AIAgents #AgentMemory #LangGraph #LangChain #RAG #MCP #LLM #Python #GenerativeAI #AgenticAI #AIEngineering
