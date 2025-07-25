# Prompt Pulse
A Lightweight LLM Prompt Evaluation &amp; Monitoring System


Prompt Pulse is a lightweight, production-grade platform to evaluate, score, and monitor LLM prompt responses over time. 


## 🔍 What It Does

- Submit and track LLM prompts
- Run LLMs (e.g., GPT-4) and store responses
- Automatically score responses using LangChain agents
- Track cost, latency, and drift over time
- Store structured data in Databricks Delta Lake
- Deploy with Terraform, schedule with GitHub Actions, manage infra with ArgoCD


## ⚙️ Tech Stack

| Layer      | Stack                                |
|-----------|---------------------------------------|
| Language   | Python                                |
| LLM Agent  | LangChain                             |
| Backend    | FastAPI                               |
| Infra      | AWS (S3, Lambda/ECS), Terraform       |
| Data       | Databricks Delta Lake (Spark, PySpark)|
| CI/CD      | GitHub Actions, ArgoCD                |
| Frontend   | React (optional)                      |


## 📌 Roadmap

- [ ] FastAPI LLM run + scoring service
- [ ] Databricks Delta ingestion pipeline
- [ ] Terraform AWS infrastructure
- [ ] Scheduled CI (daily evals)
- [ ] Dashboard frontend (basic)

## Architecture 


```mermaid
flowchart TD
  %% Components
  ReactApp["React App"]
  FastAPI["FastAPI Server"]
  LangChain["LangChain Agent (OpenAI / Anthropic)"]
  S3["AWS S3 Bucket"]
  Cron["GitHub Actions"]
  DBX["Databricks Job"]
  Delta["Delta Lake Table"]
  Dashboard["Dashboard UI"]
  Terraform["Terraform"]
  Argo["ArgoCD"]

  %% Data flow
  ReactApp -->|User prompt| FastAPI
  FastAPI -->|Send prompt| LangChain
  LangChain -->|Return result| FastAPI
  FastAPI -->|Save output| S3

  Cron -->|Trigger batch job| S3
  S3 -->|Data| DBX
  DBX -->|Write processed data| Delta
  Delta -->|Visualize| Dashboard

  %% Infra
  Terraform --> FastAPI
  Terraform --> DBX
  Terraform --> S3
  Argo --> FastAPI

```