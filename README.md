# Multi-Agent Research Automation System using LangGraph

## Overview

This project is an end-to-end **multi-agent research automation system** built using **LangGraph**, **GPT-5 Nano**, **Wikipedia**, and **Tavily Search**.

The system simulates a team of AI analysts who independently investigate different perspectives of a research topic, conduct structured interviews with an AI expert, gather external context, and generate a final report.

Key capabilities:
- Multi-Agent Systems
- Human-in-the-Loop Control
- Map-Reduce Execution
- Parallel Subgraph Processing
- RAG (Wikipedia + Tavily)
- Structured Outputs (Pydantic)
- MLOps-style orchestration

---

## 1. Multi-Agent Analyst Generation

The system creates up to **3 analysts**.

Each analyst contains:
- Name
- Role
- Affiliation
- Focus Area

They represent different perspectives of the same topic.

---

## 2. Human Feedback Loop

Before execution, a human can:

- Approve analysts
- Modify analysts
- Reject and regenerate

Flow:

If feedback ≠ "approve"
→ system returns to analyst creation

If feedback = "approve"
→ system proceeds to interviews

### Benefits:
- Human control
- Safer generation
- Better specialization
- Improved governance

---

## 3. Map-Reduce Pattern (Parallel Execution)

### Map Phase

Each analyst runs in parallel:

Send("conduct_interview", {...})

Each analyst:
- asks questions
- retrieves context
- interacts with expert
- builds independent insights

### Benefits:
- parallel execution
- faster processing
- scalable design
- independent reasoning

---

## 4. Controlled Interview Loop

Each analyst interacts with an expert.

Constraints:
- max turns = 2
- early exit phrase: "Thank you so much for your help!"

Interview ends when:
- max rounds reached OR
- analyst ends conversation

### Benefits:
- prevents infinite loops
- controls token usage
- predictable execution

---

## 5. Reduce Phase

After interviews:
- each analyst produces a section
- all sections are merged using operator.add

Final output:
- Introduction
- Main report
- Conclusion
- Final report

---

## 6. Structured Output Generation

System uses Pydantic schemas for:

- analyst structure
- search queries
- report sections

Final structure:

- Introduction
- Analyst Sections
- Insights
- Conclusion
- Sources

---

## 7. MLOps / LLMOps Governance

This system behaves like an AI pipeline.

Controls:
- human approval gate
- fixed analyst count
- max interview rounds
- structured schemas
- deterministic routing
- controlled tool usage

Outcome:
- predictable execution
- production-ready workflow

---

## 8. RAG (Retrieval-Augmented Generation)

Tools used:

WikipediaLoader
TavilySearch

Purpose:
- fetch external knowledge
- improve factual accuracy
- reduce hallucinations

---

## Workflow

START
  ↓
Create Analysts
  ↓
Human Feedback Loop
  ↓
Approve / Regenerate
  ↓
Parallel Interviews (Map Phase)
  ↓
Each Analyst:
   Ask Question
   Retrieve Context
   Expert Answer
   Repeat (max 2 or exit)
   Write Section
  ↓
Reduce Phase
  ↓
Merge Sections
  ↓
Write Introduction
Write Report
Write Conclusion
  ↓
Final Output
  ↓
END

---

## Key Parameters

- Max Analysts: 3  
- Human Feedback: Yes  
- Max Interview Rounds: 2  
- Tools: Wikipedia + Tavily  
- Execution: Parallel  
- Reducer: operator.add  

---

## Technologies

- Python  
- LangGraph  
- LangChain  
- GPT-5 Nano  
- Pydantic  
- Tavily API  
- Wikipedia Loader  

---

## Why This Project Matters

Demonstrates:
- multi-agent systems
- graph orchestration
- RAG pipelines
- structured LLM workflows
- MLOps-style AI design

---

## Future Improvements

- Streamlit UI
- LangSmith tracing
- vector database
- PDF export
- cloud deployment

---

## Run

pip install -r requirements.txt  
python research_graph.py  

---

## Author

Multi-agent LangGraph system for automated research and structured AI reasoning.
