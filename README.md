# ⚖️ AI Legal Assistant Agent

An **Agentic RAG-based Legal Assistant** designed to provide context-aware responses from legal documents using **Retrieval-Augmented Generation (RAG)** and intelligent agent workflows.

The system combines **LangGraph, LangChain, OpenAI, Pinecone, Streamlit, and SQLite** to retrieve relevant legal information, evaluate its relevance, rewrite queries when necessary, and generate context-aware responses.

---

## 🚀 Overview

Finding relevant information from lengthy legal documents can be difficult and time-consuming.

The **AI Legal Assistant Agent** addresses this problem by allowing users to ask questions in natural language and retrieving relevant information from a legal knowledge base before generating a response.

Instead of relying only on the language model's internal knowledge, the system follows a **Retrieval-Augmented Generation workflow**:

```text
User Query
    ↓
Query Analysis
    ↓
Query Rewriting
    ↓
Document Retrieval
    ↓
Relevance Scoring
    ↓
Context Selection
    ↓
LLM Response Generation
    ↓
Context-Aware Answer
```

The system also uses an **agentic workflow** to dynamically determine how a query should be processed.

---

# ✨ Key Features

### 🤖 Agentic RAG

Uses an agent-based workflow to intelligently process user queries and retrieve relevant information before generating responses.

### 🔎 Automated Retrieval

Searches the vector database for documents or chunks relevant to the user's question.

### 📊 Relevance Scoring

Evaluates retrieved information to determine whether the retrieved context is sufficiently relevant to the query.

### 🔄 Query Rewriting

If the initial retrieval is not sufficiently relevant, the system can rewrite the user's query and perform retrieval again.

### 👤 Adaptive AI Personas

Supports adaptive AI personas to provide responses according to different interaction styles.

### 💾 FAQ Storage

Uses SQLite to store frequently asked questions and related information for improved reuse and continuous knowledge management.

### 📚 Context-Aware Responses

Generates answers using retrieved legal context rather than relying solely on the language model.

### 🖥️ Streamlit Interface

Provides an interactive web interface through Streamlit for users to interact with the legal assistant.

---

# 🏗️ System Architecture

```text
                         ┌──────────────────┐
                         │      User        │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │   Streamlit UI   │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │   User Query     │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │    LangGraph     │
                         │  Agent Workflow  │
                         └────────┬─────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                    ▼                           ▼
             Query Analysis              Query Rewriting
                    │                           │
                    └─────────────┬─────────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │     Pinecone     │
                         │  Vector Search   │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │ Relevance Scoring│
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │ Retrieved Legal  │
                         │     Context      │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │      OpenAI      │
                         │   LLM Response   │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │ Final Contextual │
                         │     Answer       │
                         └──────────────────┘

                    ┌──────────────────────┐
                    │       SQLite        │
                    │     FAQ Storage     │
                    └──────────────────────┘
```

---

# 🧠 How the Agent Works

## 1. User Query

The user enters a legal question through the Streamlit interface.

Example:

```text
"What are the relevant provisions regarding this legal issue?"
```

The query is passed to the agent workflow.

---

## 2. Query Processing

The LangGraph workflow analyzes the incoming query and determines how it should be processed.

The goal is to make the query suitable for accurate retrieval.

---

## 3. Query Rewriting

If the original query does not produce sufficiently relevant results, the system can rewrite the query.

For example:

```text
Original Query
      ↓
"legal issue regarding contract termination"

      ↓

Rewritten Query
      ↓
"legal provisions and conditions related to termination
of a contractual agreement"
```

This helps improve retrieval quality.

---

## 4. Vector Retrieval

The processed query is used to search the **Pinecone vector database**.

Relevant document chunks are retrieved based on semantic similarity.

This allows the system to find information even when the user's wording differs from the wording used in the source documents.

---

## 5. Relevance Scoring

Retrieved documents are evaluated to determine whether they contain useful information for answering the question.

The system uses relevance evaluation before passing the retrieved context to the language model.

---

## 6. Context Construction

The most relevant retrieved information is combined into the context supplied to the language model.

Conceptually:

```text
User Question
      +
Retrieved Legal Context
      ↓
LLM Prompt
```

This reduces dependence on unsupported model-generated information.

---

## 7. Response Generation

The retrieved context is provided to the **OpenAI language model**.

The model generates a natural-language response based on the available context.

---

## 8. FAQ Storage

Frequently asked questions can be stored using **SQLite**.

This provides a lightweight persistent storage mechanism for FAQ-related information.

---

# 🛠️ Tech Stack

| Technology    | Purpose                                      |
| ------------- | -------------------------------------------- |
| **Python**    | Core application development                 |
| **LangChain** | LLM and retrieval workflow integration       |
| **LangGraph** | Agentic workflow orchestration               |
| **OpenAI**    | Large Language Model for response generation |
| **Pinecone**  | Vector database for semantic retrieval       |
| **Streamlit** | Interactive web interface                    |
| **SQLite**    | FAQ and lightweight persistent storage       |

---

# 📂 Project Structure

The exact structure may vary depending on the implementation, but the project is organized around the following major components:

```text
AI-Legal-Assistant-Agent/
│
├── application/
│   └── Streamlit interface and application logic
│
├── agent/
│   └── LangGraph agent workflow
│
├── retrieval/
│   └── Document retrieval and relevance processing
│
├── data/
│   └── Legal documents / knowledge resources
│
├── database/
│   └── SQLite FAQ storage
│
├── requirements.txt
├── README.md
└── ...
```

---

# 🔐 Environment Variables

API credentials should **never be hard-coded** in the source code.

Create a `.env` file locally and configure the required credentials.

Example:

```env
OPENAI_API_KEY=your_openai_api_key
PINECONE_API_KEY=your_pinecone_api_key
```

> Never commit your `.env` file or API keys to GitHub.

Add `.env` to `.gitignore`:

```text
.env
```

---

# ⚙️ Installation

## 1. Clone the Repository

```bash
git clone https://github.com/rithikka135/AI-Legal-Assistant-Agent.git
```

Navigate into the project:

```bash
cd AI-Legal-Assistant-Agent
```

---

## 2. Create a Virtual Environment

```bash
python -m venv venv
```

### Windows

```bash
venv\Scripts\activate
```

### Linux / macOS

```bash
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Configure Environment Variables

Create:

```text
.env
```

Add the required API credentials.

---

## 5. Run the Application

If the Streamlit entry point is `app.py`:

```bash
streamlit run app.py
```

If your project uses a different Streamlit entry file, replace `app.py` with the appropriate filename.

---

# 💡 Example Workflow

```text
User:
"What does the relevant legal document say about this issue?"

        ↓

LangGraph Agent

        ↓

Analyze Query

        ↓

Retrieve Relevant Documents
from Pinecone

        ↓

Evaluate Relevance

        ↓
      ┌───────────────┐
      │ Relevant?     │
      └───────┬───────┘
          Yes │ No
              │
              ▼
       Rewrite Query
              │
              └──────→ Retrieve Again

        ↓

Construct Context

        ↓

OpenAI LLM

        ↓

Context-Aware Response
```

---

# 🎯 Project Objectives

The project was developed with the following objectives:

* Build an AI assistant capable of working with legal information.
* Improve information retrieval from legal documents.
* Combine retrieval systems with generative AI.
* Implement an agentic workflow using LangGraph.
* Improve retrieval through relevance scoring.
* Improve poorly formulated queries using query rewriting.
* Provide an interactive user interface.
* Maintain FAQ information using SQLite.

---

# 🔍 Why RAG?

A standard LLM can generate answers based on its learned knowledge, but it may not have access to the specific legal documents required for a particular query.

RAG addresses this by introducing an external retrieval step:

```text
Traditional LLM

Question
   ↓
LLM
   ↓
Answer
```

With RAG:

```text
Question
   ↓
Retriever
   ↓
Relevant Documents
   ↓
LLM + Retrieved Context
   ↓
Answer
```

This makes the system more suitable for domain-specific information retrieval.

---

# 🤖 Why Agentic RAG?

Traditional RAG generally follows a fixed pipeline:

```text
Query → Retrieve → Generate
```

This project introduces an agentic workflow:

```text
Query
  ↓
Analyze
  ↓
Retrieve
  ↓
Evaluate
  ↓
Is context sufficient?
  ├── Yes → Generate Response
  │
  └── No → Rewrite Query
               ↓
            Retrieve Again
```

The workflow allows the system to make decisions during the retrieval process instead of following only a fixed retrieval path.

---

# 📈 Key Learning Outcomes

Through this project, the following concepts were explored:

* Retrieval-Augmented Generation
* Agentic AI
* LangGraph workflows
* LangChain
* Vector databases
* Semantic retrieval
* Relevance evaluation
* Query rewriting
* Prompt construction
* Large Language Models
* Streamlit application development
* SQLite database integration

---

# ⚠️ Disclaimer

This project is intended for **educational and informational purposes only**.

The AI Legal Assistant does not replace a qualified lawyer or professional legal advice. Users should consult a qualified legal professional for advice regarding actual legal matters.

---

# 👩‍💻 Author

**Rithikka A.**

Computer Science and Engineering — AI Honors
Kumaraguru College of Technology

### Connect

* GitHub: https://github.com/rithikka135
* LinkedIn: https://linkedin.com/in/rithikka-ab315772a2
* Email: [rithikka91@gmail.com](mailto:rithikka91@gmail.com)

---

## ⭐ Project Highlights

**Agentic RAG** • **LangGraph** • **LangChain** • **OpenAI** • **Pinecone** • **Streamlit** • **SQLite**

If you find this project useful, consider giving the repository a ⭐.
