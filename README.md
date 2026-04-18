# 🌾 AgriSaathi — Agricultural Intelligence Platform

AgriSaathi is a Streamlit-based web application designed to empower Indian farmers with AI-driven tools for plant disease detection, government scheme discovery, live mandi (market) price analytics, and an intelligent AI chatbot.

## 🚜 The Problem

Indian farmers, especially small and marginal ones, face a unique set of challenges that directly threaten their livelihoods:

- **Crop diseases go undetected until it's too late.** Most farmers lack access to agronomists or plant pathologists. By the time a disease is visually obvious, it has often already spread across the field, causing significant yield loss.
- **Government schemes remain out of reach.** India offers dozens of agricultural support schemes (subsidies, insurance, credit, pensions), but awareness is low, eligibility criteria are confusing, and there is no single accessible place to discover what a farmer qualifies for.
- **Market price information is opaque.** Farmers often sell their produce without knowing the prevailing mandi (wholesale market) prices, leaving them vulnerable to exploitation by middlemen and unable to time their sales for better returns.
- **Language and literacy barriers limit access to technology.** Most agricultural advisory tools are only available in English, making them inaccessible to the majority of farmers who speak Hindi or regional languages.
- **No unified platform for farm intelligence.** Farmers currently have to navigate multiple government portals, call helplines, or rely on word-of-mouth, there is no single tool that brings disease diagnosis, scheme discovery, price data, and advisory together.

AgriSaathi directly addresses these gaps by putting AI-powered, multilingual, and easy-to-use farm intelligence in the hands of every farmer.

---

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Modules](#modules)
- [Authentication](#authentication)
- [Contributing](#contributing)

---

## ✨ Features

- **🌿 Plant Disease Detection** — Upload a crop image to diagnose plant diseases using a HuggingFace computer vision model, enhanced with a RAG (Retrieval-Augmented Generation) pipeline for treatment recommendations.
- **🌱 Government Schemes Portal** — Browse and filter Indian agricultural schemes (PM-KISAN, PMFBY, KCC, Soil Health Card, etc.) by category, benefit type, and eligibility.
- **📊 Mandi Price Stats** — Embedded Databricks dashboard displaying real-time agricultural market prices across India.
- **🤖 Genie AI Chat** — Natural language interface powered by Databricks Genie to query agricultural data, crop statistics, and market insights.
- **🎙️ Voice Support** — Speech-to-text and text-to-speech in Indian regional languages via Sarvam AI (Hindi, English, and more).
- **👤 User Authentication** — Secure login and signup with user data stored in a local JSON file.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | [Streamlit](https://streamlit.io/) |
| AI / ML | HuggingFace Inference API, Sentence Transformers, FAISS |
| Data & Analytics | Databricks SDK (Genie AI), Databricks Dashboards |
| Voice AI | [Sarvam AI](https://www.sarvam.ai/) (STT, TTS, Translation) |
| Data Visualization | Plotly |
| Image Processing | Pillow (PIL) |
| Deployment | `app.yaml` (Cloud Run / App Engine compatible) |

---

## 📁 Project Structure

```
streamlit-hello-world-app/
├── app.py                  # Main entry point; wires together all modules and voice features
├── home.py                 # Home page with tabbed navigation across all four modules
├── login.py                # Login page with credential validation
├── signup.py               # User registration with Aadhaar and location fields
├── disease_detection.py    # Plant disease detection with HuggingFace + RAG pipeline
├── schemes_portal.py       # Government agricultural schemes browser and filter
├── schemes_summary.py      # Compact schemes summary component
├── mandi_prices.py         # Embedded Databricks Mandi price dashboard
├── chatbot.py              # Floating AI chatbot UI component
├── genie_chat.py           # Genie AI chat tab (full-page chat interface)
├── genie_client.py         # Databricks Genie SDK client wrapper
├── weather_predictions.py  # 7-day weather forecast with farming recommendations
├── requirements.txt        # Python dependencies
└── app.yaml                # Deployment configuration (run command)
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9 or higher
- A Databricks workspace with Genie enabled (for AI chat and Mandi dashboard)
- A HuggingFace API key (for disease detection)
- A Sarvam AI API key (for voice features)

### Installation

1. **Clone or unzip the project:**
   ```bash
   unzip streamlit-hello-world-app.zip
   cd streamlit-hello-world-app
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate      # macOS/Linux
   venv\Scripts\activate         # Windows
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the app:**
   ```bash
   streamlit run app.py
   ```

5. Open your browser and navigate to `http://localhost:8501`.

### Demo Credentials

| Username | Password |
|---|---|
| `admin` | `admin123` |
| `farmer` | `farmer123` |
| `demo` | `demo123` |

---

## ⚙️ Configuration

The following values are currently hardcoded in `app.py` and should be moved to environment variables or a secrets manager before production deployment:

| Variable | Description | Location |
|---|---|---|
| `GENIE_SPACE_ID` | Databricks Genie Space ID | `app.py` |
| `SARVAM_API_KEY` | Sarvam AI subscription key | `app.py` |
| `HF_API_KEY` | HuggingFace API key | `disease_detection.py` |
| `DASHBOARD_ID` | Databricks dashboard ID | `mandi_prices.py` |
| `WORKSPACE_URL` | Databricks workspace URL | `mandi_prices.py` |

**Recommended:** Use [Streamlit Secrets](https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/secrets-management) (`secrets.toml`) or environment variables to manage these values securely.

---

## 🧩 Modules

### 🌿 Plant Disease Detection (`disease_detection.py`)
Accepts a crop image upload and queries the `linkanjarad/mobilenet_v2_1.0_224-plant-disease-identification` model on HuggingFace. When FAISS and Sentence Transformers are available, a RAG pipeline augments the diagnosis with treatment recommendations from a local knowledge base. Supports diseases for Wheat, Rice, Cotton, Tomato, Potato, Soybean, and more.

### 🌱 Schemes Portal (`schemes_portal.py` / `schemes_summary.py`)
A searchable and filterable catalog of Indian government agricultural schemes including PM-KISAN, PMFBY, Kisan Credit Card, Soil Health Card, PM-Maandhan, and many others. Filters by benefit type, category, and state eligibility.

### 📊 Mandi Price Stats (`mandi_prices.py`)
Embeds a live Databricks dashboard (dark-themed) showing real-time commodity prices across Indian agricultural markets (mandis).

### 🤖 Genie AI Chat (`genie_chat.py`, `genie_client.py`, `chatbot.py`)
A full-page chat interface and a floating chatbot button, both powered by Databricks Genie. Sends natural language questions, polls for results, and surfaces SQL-backed data responses about crop statistics, scheme info, and market prices.

### 🌤️ Weather Predictions (`weather_predictions.py`)
7-day weather forecast visualization using Plotly charts, with farming activity recommendations based on predicted conditions. *(Note: this tab is currently commented out in `home.py`.)*

---

## 🔐 Authentication

User credentials are stored in a `users.json` file created at runtime in the project root. The signup form collects username, password, email, full name, location, and Aadhaar card number.

> ⚠️ **Security Notice:** The current authentication system stores passwords in plain text and is intended for demonstration purposes only. For production use, replace with a proper authentication solution using hashed passwords and a secure database.

---

## 🤝 Contributing

1. Fork the repository and create a feature branch.
2. Follow the existing module pattern — each feature lives in its own file with a `show_*()` function.
3. Test your changes locally with `streamlit run app.py`.
4. Submit a pull request with a clear description of your changes.
![Uploading mermaid-diagram.png…]()

