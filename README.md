# RoadWatch

RoadWatch is a full-stack AI-powered civic platform that allows citizens to report urban infrastructure issues — potholes, electrical faults, water leaks, sanitation problems — and get instant AI-generated responses. Government officers access a real-time command dashboard to manage, prioritize, and resolve issues.

## ✨ Key Features

### 👤 Citizen Side

- Report infrastructure issues with text description and photo evidence
- AI classifier instantly detects category (road/electrical/water/sanitation) and urgency (1–5)
- Real-time AI chat support powered by trained ML model
- Smart conversation handler (greetings, status queries, complaints)
- JWT-based authentication with role management
- Photo evidence saved to server and MongoDB

### 🏛️ Government Side

- Protected dashboard — only accessible with government credentials
- CORE.OS Command Center — unique multi-view dashboard:
  - Overview with live complaint pulse graph
  - Reports queue with urgency badges and status management
  - Analytics with category breakdown and trend charts
  - Citizen activity log with report counts
  - Live chat panel for real-time citizen communication
  - Zone hotspot heatmap
- One-click status updates (Pending → In Progress → Resolved)
- Real-time socket updates

### 🤖 AI & ML

- Custom trained Random Forest classifier built with scikit-learn
- Trained on Google Colab with TF-IDF vectorization
- Three separate models:
  - `category_model.pkl` — classifies issue type
  - `urgency_model.pkl` — predicts urgency level (1–5)
  - `chat_model.pkl` — detects conversation intent (greeting, complaint, status, etc.)
- Flask API serves all models on port 8000
- Node.js backend calls Flask via HTTP for real-time predictions

## 🏗️ Architecture

```text
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  React Frontend │────▶│  Node.js Backend│────▶│  Python Flask   │
│  localhost:8080 │     │  localhost:5000 │     │  localhost:8000 │
│                 │     │                 │     │                 │
│  - Citizen UI   │     │  - Auth (JWT)   │     │  - ML Models    │
│  - Gov Dashboard│     │  - REST API     │     │  - category_model│
│  - Live Chat    │     │  - Socket.io    │     │  - urgency_model │
│  - Report Form  │     │  - File Upload  │     │  - chat_model    │
└─────────────────┘     └────────┬────────┘     └─────────────────┘
                                  │
                         ┌────────▼────────┐
                         │    MongoDB      │
                         │ localhost:27017 │
                         │                 │
                         │  - users        │
                         │  - reports      │
                         │  - allowed_emails│
                         └─────────────────┘
```

## 🛠️ Tech Stack

| Layer | Technology |
| --- | --- |
| Frontend | React 18, TypeScript, Vite, Tailwind CSS, Framer Motion |
| Backend | Node.js, Express.js, Socket.io |
| ML API | Python, Flask, Flask-CORS |
| Machine Learning | scikit-learn, TF-IDF, Random Forest Classifier |
| Database | MongoDB, Mongoose |
| Auth | JWT, bcryptjs |
| File Upload | Multer |
| Real-time | Socket.io |
| Model Training | Google Colab |
