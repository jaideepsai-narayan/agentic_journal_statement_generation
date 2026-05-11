# Agentic_journal_statement_generation

# 🤖 Agentic Financial Reconciler & Journal Generator

![LangGraph](https://img.shields.io/badge/LangGraph-Agentic_Workflow-blue?style=for-the-badge)
![Pandas](https://img.shields.io/badge/Pandas-Data_Processing-150458?style=for-the-badge&logo=pandas)
![LLM Auditor](https://img.shields.io/badge/LLM-Audited-brightgreen?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.9+-yellow?style=for-the-badge&logo=python)

An intelligent, automated workflow built with **LangGraph** that reconciles bank transactions against invoices to calculate conversion fees, automatically drafting and auditing journal entries.

Instead of relying purely on large language models for arithmetic which can lead to hallucinations this project implements a robust **Maker-Checker (Generator-Validator)** pattern. 

## ✨ Key Features

- 🏗️ **Maker-Checker Architecture:** Combines the deterministic precision of Python/Pandas for mathematical calculations with the cognitive reasoning of an LLM.
- 🕵️‍♂️ **Agentic Revalidation:** An LLM auditor evaluates the draft journal entries step-by-step against strict accounting rules to ensure accuracy before finalizing.
- 🔀 **Complex Matching:** Easily parses multi-invoice payments (e.g., bank descriptions like `"1002, 1003"`) and maps them to their respective invoice rows.
- 🔄 **Cyclic Routing:** Conditionally routes failed validations for review, preventing erroneous financial data from being saved.

---

## 🗺️ Workflow Architecture

```mermaid
graph TD;
    A[(Invoices CSV)] --> C;
    B[(Bank CSV)] --> C;
    
    subgraph LangGraph Agentic Flow
    C[🛠️ Maker Node <br/> Generates Draft Journals] --> D{🕵️ Auditor Node <br/> LLM Validation};
    D -- "Valid = False" --> C;
    D -- "Valid = True" --> E[💾 Save Node];
    end
    
    E --> F[(Journals CSV)];
