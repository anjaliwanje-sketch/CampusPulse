# CampusPulse — UI/UX Design System Specification

## 1. Visual Direction
CampusPulse strictly adheres to a **professional, clean, modern, university-grade aesthetic**. It avoids excessive gradients, neon colors, heavy glassmorphism, or cartoonish graphics.

### 1.1 Color Palette
- **Background Main**: `#090d16` (Slate Dark) / `#f8fafc` (Light Mode)
- **Card / Surface**: `#111827` (Dark Surface) / `#ffffff` (Light Surface)
- **Border**: `#1f2937` (Dark Border) / `#e2e8f0` (Light Border)
- **Primary Accent**: `#3b82f6` (Indigo/Blue 500) - Used for primary CTA and active states
- **Success / Ready**: `#10b981` (Emerald 500)
- **Warning / At-Risk**: `#f59e0b` (Amber 500)
- **Danger / Critical Gap**: `#ef4444` (Red 500)
- **Text Primary**: `#f9fafb` (Dark Mode Primary) / `#0f172a` (Light Mode Primary)
- **Text Secondary**: `#9ca3af` / `#64748b`

### 1.2 Typography
- **Primary Font**: `Inter`, `-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, `Roboto`
- **Headings**: Semi-bold to Bold, tight letter-spacing (`-0.02em`)
- **Code / Mono**: `JetBrains Mono`, `Fira Code`, `monospace`

## 2. Layout Structure

### 2.1 Navigation Bar (Header)
- Logo: **CampusPulse** (Clean mark with pulse dot)
- User Profile Summary (Avatar, Name, Role Badge: `Student` or `Placement Officer`)
- Quick Notifications Bell with Unread Badge
- Logout Action

### 2.2 Sidebar Navigation
- **Student Menu**:
  - Dashboard Overview
  - Placement Drives
  - Online Assessments
  - AI Mock Interview
  - Skill Gap Analysis
  - Recommended Workshops
  - AI Resume Tailor
- **Placement Officer Menu**:
  - College Overview
  - Cohort Skill Gaps
  - Workshop Manager (Create & Track)
  - Placement Drives Manager
  - Student Readiness Directory
  - Intervention Analytics

## 3. UI Components Standards

### 3.1 Stat Cards
- Minimal border, solid background (`#111827`).
- Top label in muted text, large metric value in high contrast font.
- Sub-text showing cohort size, readiness %, or flag status.

### 3.2 Skill Gap Indicators
- Visual comparison bar: Target Skill Level (Line indicator) vs Student Proficiency (Filled bar).
- Color coding:
  - Green (>= Target)
  - Yellow (-1% to -15% Gap)
  - Red (<-15% Gap)

### 3.3 Assessment & Interview Player
- Split view: Prompt/Question left, Response area right.
- Proctoring Status Banner top right (Camera Feed / Integrity Status pill).
- Progress bar and timer pill.

### 3.4 Workshop Cards & Cohort Tables
- Cohort aggregation view: Number of affected students, target company drives impacted, common skill deficiency badges.
- Workshop Cards: Schedule pill, instructor, registered capacity bar, action button (`Register`, `Mark Attendance`, `Start Post-Assessment`).

## 4. Design Guidelines Compliance
- **No placeholders**: All UI widgets display data or clear empty states (`No upcoming workshops assigned`, `Complete an assessment to calculate readiness`).
- **Responsive**: Grid layout wrapping cleanly from desktop to mobile screens.
