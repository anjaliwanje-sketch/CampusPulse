# CampusPulse — Product Requirements Document (PRD)

## 1. Overview
CampusPulse is an **AI-Powered Student Placement Readiness & Intervention Platform** designed to solve placement unpredictability for higher education institutions. It shifts campus placements from reactive hiring to proactive, data-driven skill gap detection and intervention.

## 2. Target Users & Roles
- **Student**: Evaluates company-specific placement readiness, takes aptitude assessments, participates in AI mock interviews, identifies missing technical/soft skill gaps, receives college workshop intervention recommendations, attends workshops, completes post-assessment reassessments, and generates tailored resumes.
- **Placement Officer / College Admin**: Monitors institution-wide placement readiness, views aggregated skill gap cohorts, designs and assigns targeted college-led workshops, tracks workshop attendance, measures before/after intervention impact, and manages placement drives.

## 3. Core Workflow
```
Student Profile & Academic Data
           ↓
Target Company Placement Drive Requirements
           ↓
Online Assessment (Aptitude & Technical)
           ↓
AI Mock Interview (Role-specific QA & Behavioral)
           ↓
Proctoring Analysis & Integrity Score
           ↓
Company-Specific Readiness & Skill Gap Engine
           ↓
College-Level Cohort Aggregation (Placement Officer View)
           ↓
College Workshop & Intervention Assignment
           ↓
Student Registration & Attendance Recording
           ↓
Post-Workshop Assessment & Reassessment Engine
           ↓
Updated Readiness Score & Remaining Skill Gaps
```

## 4. Key Functional Modules

### 4.1 Authentication & Profile
- Registration with role selection (`Student`, `Placement Officer`).
- Student profile fields: Full Name, Registration Number, Email, Phone, Username, GitHub URL, LinkedIn URL, Department, Branch, CGPA, Graduation Year, Password.
- Placement Officer profile: Name, Employee ID, Email, Department.
- Protected routes based on JWT auth and user role permissions.

### 4.2 Company Drives & Job Roles
- Placement drives with detailed job specifications: Target Company Name, Role Title, Minimum CGPA, Required Skills (with target proficiency thresholds 0-100%), Target Date, Package (LPA), Drive Stages (Aptitude, Tech Interview, HR Interview).
- Student-Drive Matching: Calculates company-specific readiness score (%) rather than generic placement probability.

### 4.3 Online Assessment Engine
- Focuses on Aptitude, Logical Reasoning, Quantitative Ability, Verbal Ability, and Core Computer Science Fundamentals.
- Multi-choice and structured question format.
- Automated evaluation and skill-tagging per question.

### 4.4 AI Interview System
- AI-driven dynamic interview simulator.
- Generates company/role specific questions (Technical + HR/Behavioral).
- Evaluates candidate responses for correctness, technical clarity, communication depth, and sentiment.
- Generates detailed feedback breakdown and feeds interview score into readiness engine.

### 4.5 Online Proctoring & Integrity Architecture
- Web-based proctoring adapter recording session events.
- Detection capability specifications:
  - Phone detection flag
  - Multiple persons detected
  - Person missing / face not detected
  - Tab switching / focus loss
- Aggregates an Integrity Score (0-100%) and Trust Index.

### 4.6 Skill-Gap Engine
- Compares individual student skill proficiency against company drive requirements.
- Identifies critical gaps (e.g. Target DSA 75%, Current 48% → Gap: -27%).
- Categorizes gap severity (High Risk, Medium Risk, Ready).

### 4.7 College-Level Skill Gap Aggregation
- Aggregates individual gaps into cohort metrics for Placement Officers.
- Example: "50 students in CSE lack DSA + C++ for Amazon Drive; average score: 54%, target: 75%".
- Highlighting high-impact areas for intervention.

### 4.8 College Workshop / Intervention Module
- Placement officers create targeted workshops mapped to specific skill gaps, student cohorts, and upcoming company drives.
- Workshop details: Title, Target Skills, Assigned Instructor, Schedule, Capacity, Mode (Online/Offline/Hybrid), Meeting/Location Info.
- Registration & Attendance tracking.
- Post-workshop reassessment: Triggers mandatory evaluation post-workshop to recalculate skill scores and readiness improvement from real stored metrics.

### 4.9 AI Resume Analyzer & Builder
- Extracts key profile data, skills, projects, and achievements.
- Matches resume content against company Job Descriptions (JD).
- Generates company-tailored resume suggestions and formatting.

### 4.10 Analytics & Reports
- Placement Readiness distribution across departments.
- Pre vs Post workshop intervention efficacy reports.
- Student readiness leaderboard and risk warning list.
