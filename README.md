# 🛡️ ScamShield AI

> **Real-time Scam & Fraud Detection Platform with Mobile App, OCR Screenshot Scanner, and AI Verification.**

ScamShield AI helps users analyze suspicious messages, phishing emails, SMS alerts, and payment scams before they fall victim. It combines rule-based fraud heuristics with OCR text extraction and optional Large Language Model (LLM) verification.

---

## 📱 Features

- **Mobile App (React Native / Expo)**:
  - 📷 **OCR Screenshot Scanner**: Upload or snap a screenshot of a suspicious chat, email, or text to extract the message text automatically using on-device OCR (`tesseract.js`).
  - 📋 **One-Tap Clipboard Paste**: Quickly paste messages copied from SMS, WhatsApp, Telegram, or email.
  - 🚦 **0–100 Risk Score**: Visual High / Medium / Low danger indicators.
  - ⚠️ **Signal Identification**: Detects urgent pressure, OTP/password requests, cryptocurrency/gift card payment traps, and phishing domains.
  - 🛡️ **Actionable Protection Advice**: Clear step-by-step guidance on what to do next.
  - 📜 **Scan History**: Stores previous checks locally on device.
  - 🔌 **Offline First**: Runs client-side heuristic rules locally even without internet connection, and synchronizes with the backend when online.

- **FastAPI Backend**:
  - High-performance asynchronous REST API.
  - SQLite persistence (`scamshield.db`) for tracking scan logs and threat telemetry.
  - Optional OpenAI / LLM chat completion integration with transparent rule floors.

- **Web Dashboard**:
  - Lightweight, responsive desktop dashboard with zero-build requirements.

---

## 🏗️ Project Architecture

```text
scamshield/
├── scamshield-mobile/          # React Native & Expo Mobile Application
│   ├── App.js                  # Main UI, OCR Screenshot reader & Scanner logic
│   ├── package.json            # Expo SDK 58, tesseract.js, expo-image-picker
│   └── app.json                # Expo mobile configuration
│
├── scamshield-ai/
│   ├── backend/                # FastAPI Python Backend
│   │   ├── app/
│   │   │   ├── main.py         # REST Endpoints (/api/scan, /api/scans, /health)
│   │   │   ├── analyzer.py     # Heuristic Rule Engine + LLM fallback
│   │   │   ├── models.py       # SQLAlchemy ORM Models
│   │   │   ├── database.py     # SQLite Database setup
│   │   │   └── config.py       # Environment configuration
│   │   └── requirements.txt    # FastAPI, Uvicorn, SQLAlchemy, Pydantic
│   │
│   └── frontend/               # Responsive Web Dashboard
│       ├── index.html          # Web UI layout
│       ├── app.js              # Web client logic & local analysis fallback
│       ├── styles.css          # Styling
│       └── serve.mjs           # Node.js preview server
│
├── .gitignore                  # Git exclusions (node_modules, venvs, DBs)
└── README.md                   # Project documentation
