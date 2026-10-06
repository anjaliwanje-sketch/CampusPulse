# CampusPulse — System Architecture Document

## 1. Monorepo Directory Layout
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
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── utils/
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
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
│   │   ├── utils/
│   │   ├── validators/
│   │   └── app.js
│   ├── tests/
│   ├── package.json
│   └── server.js
├── models/
│   ├── readiness_weights.json
│   └── proctoring_config.json
├── .env.example
├── README.md
└── package.json
```

## 2. Component Stack

### 2.1 Frontend Framework
- **Framework**: React 18 with Vite
- **Routing**: React Router DOM v6
- **State & Auth**: React Context API (`AuthContext`)
- **Icons**: Lucide React
- **Styling**: Modern Modular Vanilla CSS & Utility classes
- **HTTP Client**: Axios with interceptors for JWT token injection

### 2.2 Backend Framework
- **Runtime**: Node.js v18+
- **Framework**: Express.js
- **Database ORM/ODM**: Mongoose ODM connecting to MongoDB
- **Authentication**: JSON Web Tokens (JWT) & bcryptjs password hashing
- **Input Validation**: Express-validator & Joi / custom middleware

### 2.3 System Data Flow
```text
Frontend React App
    │ (REST APIs over HTTPS with Bearer Token)
    ▼
Express Controllers (Request Validation & Auth Middleware)
    │
    ▼
Backend Service Layer (Business Logic, Readiness Calculation, Cohort Aggregator)
    │
    ├──► MongoDB Collections (Users, Drives, Assessments, Workshops, Scores)
    │
    └──► AI & Proctoring Adapters (Gemini Service / Local Fallback Rules)
```

## 3. Security Architecture
- Password Hashing with `bcryptjs` (salt rounds: 10).
- Role-based Access Control (`RBAC`) enforced at backend route level (`verifyToken`, `requireRole('officer')`).
- Environment variables isolation (`MONGODB_URI`, `JWT_SECRET`, `GEMINI_API_KEY`).
- CORS restriction to configured `FRONTEND_URL`.
