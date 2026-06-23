# 🧠 Multilingual Mental-Health Chatbot
 
> A safe, grounded mental-health support chatbot in **English, Hindi, and Urdu**, powered by an **LLM + RAG** pipeline, served through a secure **Django** backend with authentication and **Stripe** subscriptions.
 
<!-- Replace these with your real badges -->
![Python](https://img.shields.io/badge/python-3.11+-blue.svg)
![Django](https://img.shields.io/badge/django-5.x-092E20.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)
 
---
 
## Overview
 
This project is a multilingual mental-health assistant designed to provide **safe, empathetic, and grounded** responses. Instead of letting the language model answer freely, every reply is anchored to a curated knowledge base using **Retrieval-Augmented Generation (RAG)** — reducing hallucination and keeping responses aligned with vetted mental-health resources.
 
The system supports **English, Hindi, and Urdu**, making support accessible to a wider community.
 
> ⚠️ **Important:** This chatbot is **not a substitute for professional medical or psychological care**. It does not provide diagnosis or treatment. If you or someone you know is in crisis, please contact a licensed professional or a local emergency helpline.
 
---
 
## ✨ Features
 
- 🌐 **Multilingual support** — English, Hindi, and Urdu
- 🔍 **RAG-grounded responses** — retrieval over a curated knowledge base for safe, factual answers
- 🧩 **Smart document pipeline** — chunking, embeddings, and metadata filtering for precise retrieval
- 🔐 **Secure backend** — Django with user authentication and session management
- 💳 **Subscription payments** — Stripe integration for tiered access
- 🛡️ **Safety-first design** — grounded answers minimize hallucination on a sensitive domain
---
 
## 🏗️ Architecture
 
```
User (EN / HI / UR)
        │
        ▼
┌─────────────────────┐
│   Django Backend    │  ← Auth, sessions, Stripe billing
└─────────┬───────────┘
          │ query
          ▼
┌─────────────────────┐
│   RAG Pipeline      │
│  1. Embed query     │
│  2. Vector search   │  ← metadata filtering (language, topic)
│  3. Retrieve chunks │
│  4. Build prompt    │
└─────────┬───────────┘
          │ grounded context
          ▼
┌─────────────────────┐
│        LLM          │  → safe, grounded response
└─────────────────────┘
```
 
**How retrieval works:**
1. Source documents are split into overlapping **chunks**.
2. Each chunk is converted into a vector using an **embedding model**.
3. Chunks are stored in a **vector database** with **metadata** (e.g. language, topic, source).
4. At query time, the user's question is embedded and matched against the store, with **metadata filtering** to keep results relevant (e.g. matching the user's language).
5. Retrieved chunks are passed to the **LLM** as grounding context to generate the final response.
---
 
## 🛠️ Tech Stack
 
| Layer | Technology |
|-------|-----------|
| Backend | Django, Django REST Framework |
| LLM | `<your-llm-provider>` (e.g. OpenAI / Groq / local) |
| Embeddings | `<your-embedding-model>` |
| Vector store | `<your-vector-db>` (e.g. FAISS / Chroma / pgvector / Supabase) |
| Payments | Stripe |
| Database | PostgreSQL |
| Auth | Django authentication |
 
> _Edit the placeholders above to match your actual stack._
 
---
 
## 🚀 Getting Started
 
### Prerequisites
 
- Python 3.11+
- PostgreSQL
- A Stripe account (test keys are fine for development)
- An LLM provider API key
### Installation
 
```bash
# Clone the repo
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
 
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
 
# Install dependencies
pip install -r requirements.txt
```
 
### Environment Variables
 
Create a `.env` file in the project root:
 
```env
# Django
SECRET_KEY=your-django-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
 
# Database
DATABASE_URL=postgres://user:password@localhost:5432/dbname
 
# LLM / Embeddings
LLM_API_KEY=your-llm-api-key
EMBEDDING_MODEL=your-embedding-model
 
# Vector store (if applicable)
VECTOR_DB_URL=your-vector-db-url
 
# Stripe
STRIPE_SECRET_KEY=sk_test_xxx
STRIPE_PUBLISHABLE_KEY=pk_test_xxx
STRIPE_WEBHOOK_SECRET=whsec_xxx
```
 
### Run It
 
```bash
# Apply migrations
python manage.py migrate
 
# (Optional) create a superuser
python manage.py createsuperuser
 
# Ingest documents into the vector store
python manage.py ingest_documents   # adjust to your actual command
 
# Start the dev server
python manage.py runserver
```
 
The app will be available at `http://localhost:8000`.
 
---
 
## 📂 Project Structure
 
```
.
├── chatbot/            # RAG pipeline: chunking, embeddings, retrieval
├── accounts/           # Authentication & user management
├── billing/            # Stripe subscription logic
├── api/                # REST endpoints
├── data/               # Source documents / knowledge base
├── config/             # Django settings
├── requirements.txt
└── manage.py
```
 
> _Adjust this tree to reflect your real layout._
 
---
 
## 💳 Subscriptions
 
Access is managed through **Stripe subscriptions**. To configure:
 
1. Add your products and prices in the Stripe Dashboard.
2. Set the corresponding price IDs in your settings/env.
3. Configure a webhook endpoint pointing to your `/billing/webhook/` route and set `STRIPE_WEBHOOK_SECRET`.
For local webhook testing, use the [Stripe CLI](https://stripe.com/docs/stripe-cli):
 
```bash
stripe listen --forward-to localhost:8000/billing/webhook/
```
 
---
 
## 🧪 Roadmap
 
- [ ] Add more languages
- [ ] Conversation history & memory
- [ ] Admin dashboard for knowledge-base management
- [ ] Improved crisis-detection and safe-handoff flows
---
 
## 🤝 Contributing
 
Contributions are welcome. Please open an issue to discuss significant changes before submitting a PR.
 
---
 
## ⚠️ Disclaimer
 
This software is provided for informational and supportive purposes only. It is **not** a medical device and does **not** provide professional medical advice, diagnosis, or treatment. Always seek the guidance of a qualified health provider with any questions regarding a mental-health condition. If you are in crisis, contact your local emergency services or a crisis helpline immediately.
 
---
 
## 📄 License
 
Distributed under the MIT License. See `LICENSE` for details.
