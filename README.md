Path: DiagnoLLM/README.md

# DiagnoLLM — Secure, Explainable AI Chatbot for Medical Diagnosis

This repository contains a deployable prototype scaffold for **DiagnoLLM**:
a context-aware, multimodal, and explainable medical diagnosis framework
(Large Language Model + multimodal fusion + ontology alignment + secure logging).

This README covers:
- Project overview
- Quickstart (local development)
- Environment variables and secrets
- Deployment options
- Where to find the main code

---

## Project overview

DiagnoLLM accepts:
- Patient textual input (symptoms, clinical notes)
- Structured vitals / lab values
- Medical images (e.g., chest X-ray)

It produces:
- Probable diagnoses (with confidence)
- Structured reasoning chains: symptom → possible disease → recommended tests → final suggestion
- Ontology mapping (ICD / SNOMED identifiers)
- Explainability artifacts (textual rationale + structured evidence)
- Optional immutable logging (ledger) when user consents

---

## Phase 1: Repo structure (top-level)



DiagnoLLM/
├─ README.md
├─ requirements.txt
├─ .env.example
├─ Dockerfile
├─ docker-compose.yml
├─ Procfile
├─ src/
│ ├─ harmonization/
│ ├─ core/
│ ├─ mrl/
│ ├─ blockchain/
│ ├─ api/
│ └─ ui/
└─ data/


---

## Quickstart — Local development (recommended)

1. Clone this repo:
```bash
git clone <your-repo-url>
cd DiagnoLLM


Create a python virtual environment and install dependencies:

python -m venv .venv
source .venv/bin/activate    # Linux/macOS
.venv\Scripts\activate       # Windows PowerShell
pip install --upgrade pip
pip install -r requirements.txt


Copy .env.example → .env and fill in your keys (do NOT commit .env):

cp .env.example .env
# edit .env and populate HF_API_KEY, OPENAI_API_KEY, etc.


Run the FastAPI backend:

uvicorn src.api.app:app --host 0.0.0.0 --port 8000 --reload


In another terminal, run the Streamlit UI:

streamlit run src.ui.streamlit_app.py


Visit:

API: http://localhost:8000

UI: http://localhost:8501 (Streamlit default)

Quickstart — Docker & docker-compose

Build and start services:

docker-compose up --build


Open:

API: http://localhost:8000

UI: http://localhost:8501

Deployment options

Hugging Face Spaces (Streamlit): use deploy/space_config.yaml and set HF secrets

Render / Heroku: use Dockerfile and Procfile

AWS ECS / ECR: build Docker image and deploy

Security & privacy

Do not send unredacted personal health information to external APIs unless permitted by your institution and compliant with local law (HIPAA/GDPR).

Use environment variables / secret manager for API keys (HF_API_KEY, OPENAI_API_KEY).

The repository includes a local ledger scaffold. For real deployments, integrate with an institutional audit/logging system and legal review.