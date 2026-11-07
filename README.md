<p align="center">
  <img src="logo.jpeg" alt="Wellvia logo" width="180"/>
</p>

<h1 align="center">Wellvia</h1>

<p align="center">
  <strong>An AI-powered health &amp; nutrition companion: a Flutter app paired with an ESP32 wearable.</strong><br/>
  <em>Built for the IEEE CSTAM2.0 Technical Challenge (November 2025).</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white" alt="Flutter"/>
  <img src="https://img.shields.io/badge/Dart-0175C2?style=flat-square&logo=dart&logoColor=white" alt="Dart"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black" alt="Firebase"/>
  <img src="https://img.shields.io/badge/ESP32-E7352C?style=flat-square&logo=espressif&logoColor=white" alt="ESP32"/>
  <img src="https://img.shields.io/badge/Ollama-000000?style=flat-square&logo=ollama&logoColor=white" alt="Ollama"/>
</p>

---

## Overview

Wellvia turns raw data from a wrist-worn sensor and from everyday habits into health insights you can act on. The mobile app reads vitals from an ESP32 wearable over Bluetooth Low Energy, raises alerts when readings look abnormal, tracks workouts and meals, and includes an AI assistant you can chat with about your data.

<p align="center">
  <img src="watch_prototype.jpeg" alt="Wellvia wearable prototype" width="220"/>
</p>

## Features

| | |
|---|---|
| ❤️ **Real-time vitals** | Heart rate, SpO₂, body temperature and motion streamed from the wearable over BLE |
| 🚨 **Smart alerts** | Rule-based alert engine with warning, critical and emergency levels, plus local notifications |
| 🍽️ **Meal-to-data** | Snap a photo of a meal; a vision model estimates calories, protein, carbs and fat |
| 💬 **AI health chat** | Conversational assistant (LLM via Ollama) that can reference your own logged data |
| 🏃 **Workout sessions** | Start a session, follow live metrics, review history |
| 📊 **Trends & wellness score** | Daily, weekly and monthly charts and an overall wellness score |
| 🧭 **Guided onboarding** | Profile, health info and personal goals set up in a few steps |
| 📴 **Offline-first** | Local SQLite cache with background sync to Cloud Firestore |

## Architecture

```
 ┌──────────────┐   BLE    ┌───────────────────────┐   Firebase SDK   ┌──────────────────────┐
 │ ESP32 + HR / │ ───────▶ │  Flutter app          │ ───────────────▶ │ Firebase Auth        │
 │ SpO₂ / temp  │          │  (Provider, SQLite)   │                  │ Cloud Firestore      │
 │ sensors      │          └──────────┬────────────┘                  └──────────────────────┘
 └──────────────┘                     │ HTTPS (meal photos, chat)
                                      ▼
                           ┌───────────────────────┐   ┌─────────────────────────────┐
                           │  FastAPI backend      │──▶│ Ollama models               │
                           │  REST API /api/v1/... │   │ vision: meal analysis       │
                           └───────────────────────┘   │ text: health chatbot        │
                                                       └─────────────────────────────┘
```

- **Mobile app (`front_end/`)**: Flutter with Provider for state, `flutter_blue_plus` for BLE, `sqflite` for the local cache, and `fl_chart` / Syncfusion for charts. It talks to Firebase directly for authentication and data.
- **Backend (`back_end/`)**: FastAPI service exposing auth, users, vitals, activities, alerts, sessions, nutrition, vision and chatbot routes under `/api/v1`. It hosts the AI features, using Ollama models for meal-photo analysis and chat.
- **Cloud (Firebase)**: Authentication and Cloud Firestore, protected by the per-user rules in [`firestore.rules`](firestore.rules).
- **Hardware**: An ESP32 microcontroller with health sensors (circuit below).

<p align="center">
  <img src="circuit_diagram.jpeg" alt="ESP32 circuit diagram" width="620"/>
</p>

## Repository structure

```
.
├── front_end/              # Flutter mobile app
│   ├── lib/
│   │   ├── core/           # theme, constants, helpers
│   │   ├── models/         # vitals, alerts, sessions, nutrition, user
│   │   ├── providers/      # auth, bluetooth, vitals, alerts state
│   │   ├── screens/        # home, vitals, alerts, nutrition, chat, session, profile…
│   │   ├── services/       # BLE, alert engine, Firebase/Firestore, sync, notifications
│   │   └── widgets/        # charts and reusable UI
│   └── pubspec.yaml
├── back_end/               # FastAPI backend
│   ├── app/
│   │   ├── api/v1/         # route modules (incl. vision + chatbot)
│   │   ├── models/ schemas/ services/ middleware/ utils/
│   │   └── main.py
│   └── requirements.txt
├── firestore.rules         # Firestore security rules
└── *.md                    # integration & implementation notes
```

## Getting started

### Prerequisites

- Flutter SDK 3.x
- Python 3.8+
- A Firebase project (Authentication + Firestore enabled)
- [Ollama](https://ollama.com) for the AI features (optional for the rest of the app)

### 1. Clone

```bash
git clone https://github.com/CHAABEN-Chahin/wellvia.git
cd wellvia
```

### 2. Backend

```bash
cd back_end
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env            # then point it at your Firebase service account
uvicorn app.main:app --reload
```

The API runs at `http://127.0.0.1:8000`, with interactive docs at `/docs`. See [`back_end/README.md`](back_end/README.md) and [`back_end/API_QUICK_REFERENCE.md`](back_end/API_QUICK_REFERENCE.md).

### 3. Mobile app

```bash
cd front_end
# Android: put your google-services.json in android/app/
# iOS:     put your GoogleService-Info.plist in ios/Runner/
flutter pub get
flutter run
```

> **Note:** the meal-photo screen calls the backend's `/get_calories` endpoint through a URL set in `lib/screens/nutrition/log_meal_screen.dart`. Point it at your own backend before using that feature.

More detail: [`front_end/SETUP.md`](front_end/SETUP.md) · [`front_end/DEVELOPER_GUIDE.md`](front_end/DEVELOPER_GUIDE.md) · [`FIRESTORE_SETUP.md`](FIRESTORE_SETUP.md)

## Security

- Firebase Authentication for identity; Firestore rules restrict every user to their own documents.
- Backend secrets live in `.env` / service-account files, which are git-ignored.
- Tokens on the device are kept in the platform keystore via `flutter_secure_storage`.

## Team

Built during the IEEE CSTAM2.0 Technical Challenge by:

- **CHAABEN Chahin**
- AOUINI Anas
- MECHRIA Khawla
- KAMMOUN Mohamed Yassine

Thanks to everyone who contributed code. See the [contributors graph](../../graphs/contributors).

## License

No license has been chosen yet, so all rights are reserved by the authors.
