# CampusPulse — REST API Specification

All API requests and responses use JSON. Authenticated endpoints require `Authorization: Bearer <token>` header.

Standard Success Response Format:
```json
{
  "success": true,
  "data": { ... }
}
```

Standard Error Response Format:
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message"
  }
}
```

---

## 1. Authentication APIs (`/api/auth`)

### 1.1 `POST /api/auth/register`
- **Access**: Public
- **Body**:
  ```json
  {
    "role": "student", // or "officer"
    "name": "Jane Doe",
    "email": "jane@university.edu",
    "password": "Password123!",
    "confirmPassword": "Password123!",
    "registrationNumber": "REG2026001",
    "phone": "+1987654321",
    "username": "janedoe",
    "githubUrl": "https://github.com/janedoe",
    "linkedInUrl": "https://linkedin.com/in/janedoe",
    "department": "Computer Science",
    "branch": "B.Tech CSE",
    "cgpa": 8.5,
    "graduationYear": 2026
  }
  ```
- **Response**: `{ "success": true, "data": { "token": "...", "user": { ... } } }`

### 1.2 `POST /api/auth/login`
- **Access**: Public
- **Body**: `{ "email": "jane@university.edu", "password": "Password123!" }`
- **Response**: `{ "success": true, "data": { "token": "...", "user": { ... } } }`

### 1.3 `GET /api/auth/me`
- **Access**: Authenticated
- **Response**: User object & student profile details.

---

## 2. Student APIs (`/api/students`)

### 2.1 `GET /api/students/profile`
- **Access**: Student / Officer
- **Response**: Profile details, skills, readiness history.

### 2.2 `GET /api/students/readiness`
- **Access**: Student
- **Query**: `?driveId=<driveId>`
- **Response**: Company-specific readiness breakdown, stage readiness, risk identification, missing skills.

### 2.3 `GET /api/students/skill-gaps`
- **Access**: Student
- **Response**: List of skill gaps with current score vs target score per company drive.

---

## 3. Placement Drives APIs (`/api/drives`)

### 3.1 `GET /api/drives`
- **Access**: Authenticated
- **Response**: Array of placement drives.

### 3.2 `POST /api/drives`
- **Access**: Officer only
- **Body**:
  ```json
  {
    "companyName": "TechCorp",
    "roleTitle": "Software Engineer",
    "minCgpa": 7.5,
    "requiredSkills": [
      { "skillName": "Data Structures", "targetScore": 75 },
      { "skillName": "C++", "targetScore": 70 }
    ],
    "driveDate": "2026-11-15",
    "packageLpa": 12.5,
    "stages": ["Aptitude", "AI Technical Interview", "HR Interview"]
  }
  ```

### 3.3 `GET /api/drives/:id`
- **Access**: Authenticated
- **Response**: Drive details with student eligibility and target skill thresholds.

---

## 4. Assessment APIs (`/api/assessments`)

### 4.1 `GET /api/assessments`
- **Access**: Authenticated
- **Response**: Available aptitude & technical assessments.

### 4.2 `GET /api/assessments/:id`
- **Access**: Authenticated
- **Response**: Assessment questions (without answers).

### 4.3 `POST /api/assessments/:id/submit`
- **Access**: Student
- **Body**: `{ "answers": [ { "questionId": "q1", "selectedOption": 2 } ], "proctoringEvents": [...] }`
- **Response**: Test score, skill breakdown, updated readiness impact.

---

## 5. AI Interview APIs (`/api/interviews`)

### 5.1 `POST /api/interviews/start`
- **Access**: Student
- **Body**: `{ "driveId": "drive123", "roleTitle": "Backend Engineer" }`
- **Response**: Interview session ID, initial question set.

### 5.2 `POST /api/interviews/:id/answer`
- **Access**: Student
- **Body**: `{ "questionId": "q1", "transcript": "I would use a HashMap because..." }`
- **Response**: Immediate AI feedback, follow-up or next question.

### 5.3 `POST /api/interviews/:id/evaluate`
- **Access**: Student
- **Response**: Final interview evaluation, communication score, technical depth score, updated readiness contribution.

---

## 6. Proctoring APIs (`/api/proctoring`)

### 6.1 `POST /api/proctoring/log-event`
- **Access**: Student
- **Body**: `{ "sessionId": "sess123", "eventType": "PHONE_DETECTED", "timestamp": "...", "confidence": 0.92 }`
- **Response**: Recorded flag acknowledgment & cumulative integrity score.

---

## 7. College Intervention & Skill Gap Aggregation APIs (`/api/skill-gaps`)

### 7.1 `GET /api/skill-gaps/aggregation`
- **Access**: Officer only
- **Response**: Aggregated cohort gaps (e.g. "50 students lack DSA for Amazon").

### 7.2 `GET /api/skill-gaps/cohorts`
- **Access**: Officer only
- **Response**: List of student cohorts grouped by missing skill clusters.

---

## 8. Workshop APIs (`/api/workshops`)

### 8.1 `POST /api/workshops`
- **Access**: Officer only
- **Body**:
  ```json
  {
    "title": "Mastering DSA & C++",
    "targetSkills": ["Data Structures", "C++"],
    "instructor": "Prof. Alan Turing",
    "scheduledAt": "2026-10-20T10:00:00Z",
    "capacity": 60,
    "mode": "Hybrid",
    "locationInfo": "Lab 3 & Zoom Link",
    "targetDriveIds": ["drive123"],
    "assignedStudentIds": ["stud1", "stud2"]
  }
  ```

### 8.2 `GET /api/workshops`
- **Access**: Authenticated (filtered by student recommendation if student)

### 8.3 `POST /api/workshops/:id/register`
- **Access**: Student

### 8.4 `POST /api/workshops/:id/attendance`
- **Access**: Officer
- **Body**: `{ "studentAttendance": [ { "studentId": "stud1", "attended": true } ] }`

### 8.5 `POST /api/workshops/:id/post-assessment`
- **Access**: Student
- **Body**: `{ "answers": [...] }`
- **Response**: Reassessment scores, pre-vs-post workshop impact calculation (`Readiness +18%`, `Skill Gap Reduced`).

---

## 9. AI Resume APIs (`/api/resume`)

### 9.1 `POST /api/resume/analyze`
- **Access**: Student
- **Body**: `{ "driveId": "drive123", "resumeText": "..." }`
- **Response**: Matching score, missing keywords, tailored recommendations.

---

## 10. Reports & Notifications APIs (`/api/reports` & `/api/notifications`)

### 10.1 `GET /api/reports/placement-readiness`
- **Access**: Officer only
- **Response**: Institution-wide readiness distribution, pre/post workshop impact statistics.

### 10.2 `GET /api/notifications`
- **Access**: Authenticated
- **Response**: List of user notifications (e.g. workshop assignment, readiness updates).
