# Vetted

Fraud intelligence for job seekers in South Africa.

South Africa's high unemployment makes job seekers prime targets for fake jobs,
learnerships and bursaries that ask for fees, documents or banking details.
Vetted aims to reduce the number of people who fall victim by scoring job
postings *before* anyone pays or shares personal information.

## What makes it different

Not a chatbot wrapper. Vetted combines three things:

1. **Verification checks**: domain age, email/domain match, careers-page check
2. **Shared scam-reports database**: moderated reports from real users
3. **ML risk score**: a baseline TF-IDF model, later a transformer, with explanations

It targets patterns common in South Africa: WhatsApp-only hiring, fake
learnerships, and fees for uniforms or training.

## Status

Early development, built in small increments.

- [x] Repo skeleton, Django project (`vetted_api`), `scans` app
- [ ] Rule-based scorer and `POST /v1/scan`
- [ ] TF-IDF model with evaluation report
- [ ] Browser extension (Chrome dev, Firefox release)
- [ ] Verification layer
- [ ] Scam reports and moderation
- [ ] Transformer model, SHAP explanations, MLflow tracking

## Planned API

`POST /v1/scan` with `{text, url, company?, contact_email?}` returns
`{risk_score, label, reasons[], checks{}, scan_id}`.

## Tech stack

Django + DRF · scikit-learn / DistilBERT · SHAP · MLflow · WXT + TypeScript
(Manifest V3) · Postgres (Neon) · Docker · GitHub Actions

Built entirely on free tiers and open-source tools.

## Repo layout

    backend/     Django API
    extension/   Browser extension
    data/        Datasets and training notebooks
    .github/     CI workflows

## Local setup

    python -m venv .venv
    .venv\Scripts\activate        # Windows
    pip install -r backend/requirements.txt
    cd backend
    python manage.py migrate
    python manage.py runserver

## Disclaimer

Vetted gives a risk assessment, not a verdict. A low score does not guarantee
a posting is legitimate. Report suspected scams to the relevant authorities.
