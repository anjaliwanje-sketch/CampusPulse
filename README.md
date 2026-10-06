# CampusPulse — AI-Powered Student Placement Readiness & Intervention Platform

CampusPulse is a comprehensive, production-grade higher education placement platform designed to transition campus hiring from reactive placement predictions to proactive, data-driven skill gap detection and targeted college-led interventions.

---

## 1. Features

- **Company-Specific Placement Readiness**: Calculates student preparedness against specific company drive requirements ($min(CGPA)$, required skill thresholds, aptitude, and AI technical interview scores) rather than generic placement probability.
- **Online Proctoring Architecture**: Webcam proctoring event tracker with flag decays (`PHONE_DETECTED`, `MULTIPLE_PERSONS_DETECTED`, `TAB_SWITCH`) and cumulative trust score calculation.
- **AI Mock Interview Simulator**: Dynamic interview simulator evaluating technical depth, clarity, and soft skills with real-time feedback and score contribution.
- **College-Level Skill Gap Aggregation**: Groups individual student deficiencies into actionable college cohorts for Placement Officers.
- **College Workshop Intervention Module**: Allows placement officers to launch targeted workshops mapped to specific skill gaps, assign instructors, record attendance, and execute post-workshop assessments.
- **Dynamic Real Impact Reassessment**: Measures before-vs-after skill score delta ($\Delta_{\text{Skill}}$, $\Delta_{\text{Readiness}}$, $\text{Gap Reduction}$) from real stored metrics.
- **AI Resume Tailor**: Evaluates resume text compatibility against company Job Descriptions.
- **Role-Based Access Control**: Strict isolation between `Student` and `Placement Officer` permissions.

---

## 2. Architecture & Tech Stack

```text
Frontend (React 18 + Vite)
    │
    ▼ REST API (JWT Bearer Auth over HTTPS)
Backend (Express.js / Node.js)
    │
    ├──► MongoDB Collections (Mongoose ODM)
    └──► AI & Proctoring Adapters (Google Gemini / Fallback Heuristics)
```

- **Frontend**: React 18, Vite, React Router DOM v6, Lucide React, Modern CSS System.
- **Backend**: Express.js, Mongoose ODM, JWT, bcryptjs.
- **Database**: MongoDB (supporting MongoDB URI connection and in-memory hybrid store fallback).
- **AI/ML**: Google Gemini API adapter for mock interview evaluation & resume JD matching.

---

## 3. Project Structure

```text
CampusPulse/
├── docs/
│   ├── PRD.md
│   ├── design.md
│   ├── architecture.md
│   ├── api.md
│   ├── database.md
│   └── ai-ml.md
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
├── backend/
│   ├── src/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── middleware/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── services/
│   │   └── utils/
│   ├── tests/
│   │   └── api.test.js
│   ├── package.json
│   └── server.js
├── models/
│   ├── readiness_weights.json
│   └── proctoring_config.json
├── .env.example
├── README.md
└── package.json
```

---

## 4. Setup & Running Locally

### 4.1 Prerequisites
- Node.js (v18+)
- MongoDB (Optional; system includes automatic hybrid fallback store if MongoDB is not running locally)

### 4.2 Installation

```bash
# Install all dependencies
npm run install:all
```

### 4.3 Environment Setup
Copy `.env.example` to `.env`:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/campuspulse
JWT_SECRET=campuspulse_super_secret_jwt_key_2026
GEMINI_API_KEY=your_gemini_api_key_here
```

### 4.4 Running Backend

```bash
cd backend
npm start
```

### 4.5 Running Frontend

```bash
cd frontend
npm run dev
```

The frontend will be available at `http://localhost:5173`.

---

## 5. Testing

Run backend unit & core engine tests:

```bash
cd backend
node --test tests/api.test.js
```

---

## 6. API Documentation

Detailed REST API specifications are available in [`docs/api.md`](docs/api.md).
