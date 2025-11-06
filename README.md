# Solid Green — Net Zero (Modelled) Review Portal

A lightweight Streamlit web app that automates Solid Green's Net Zero Carbon (Modelled) report reviews.

## What it does
- Upload a Net Zero (Modelled) report (PDF)
- Automatically scores a strict checklist (1/0) via keyword heuristics
- Generates:
  - An **Excel** checklist with auto-scoring
  - A **PDF** infographic certificate with final score and required updates

> Note: This uses heuristic text checks. It’s designed for rapid internal QA. You can extend the keyword sets or wire in the OpenAI API for deeper semantic checks.

## Quickstart (local)
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
streamlit run app.py
```
Open the URL shown in your terminal (usually http://localhost:8501).

## Deploy options
- **Streamlit Community Cloud** (free/fast)
- **Docker** to any cloud (AWS, Azure, GCP)
- Your internal server

## Customisation
- Edit `CHECKS` in `app.py` to refine rules/keywords.
- Replace branding or colors inside the certificate generator in `build_certificate()`.

## Security
- Files are processed in-memory and not stored by default.
- Add authentication if exposing beyond internal users.