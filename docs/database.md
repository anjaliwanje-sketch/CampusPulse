# CampusPulse — MongoDB Database Schema Specification

## 1. Overview
The database uses MongoDB with Mongoose ODM schemas.

## 2. Collections & Schemas

### 2.1 `users`
- `_id`: ObjectId
- `email`: String (Unique, Indexed)
- `password`: String (Hashed)
- `role`: String (`student` | `officer`)
- `name`: String
- `createdAt`: Date

### 2.2 `students`
- `_id`: ObjectId
- `userId`: Ref -> `users` (Indexed)
- `registrationNumber`: String (Unique, Indexed)
- `phone`: String
- `username`: String
- `githubUrl`: String
- `linkedInUrl`: String
- `department`: String
- `branch`: String
- `cgpa`: Number
- `graduationYear`: Number
- `skillScores`: Map<String, Number> (e.g. `{ "Data Structures": 54, "C++": 51, "SQL": 78 }`)
- `createdAt`: Date

### 2.3 `companies` & `drives`
- `_id`: ObjectId
- `companyName`: String
- `roleTitle`: String
- `minCgpa`: Number
- `packageLpa`: Number
- `requiredSkills`: Array of `{ skillName: String, targetScore: Number }`
- `stages`: Array of String
- `driveDate`: Date
- `createdAt`: Date

### 2.4 `assessments` & `assessment_results`
- `_id`: ObjectId
- `title`: String
- `category`: String (`Aptitude`, `Logical`, `Verbal`, `Technical`)
- `questions`: Array of `{ questionId: String, text: String, options: Array<String>, correctOption: Number, targetSkill: String }`

- `assessment_results`:
  - `studentId`: Ref -> `students`
  - `assessmentId`: Ref -> `assessments`
  - `score`: Number
  - `totalQuestions`: Number
  - `skillBreakdown`: Map<String, Number>
  - `proctoringLogs`: Array of `{ eventType: String, timestamp: Date, confidence: Number }`
  - `integrityScore`: Number
  - `completedAt`: Date

### 2.5 `interviews` & `interview_results`
- `_id`: ObjectId
- `studentId`: Ref -> `students`
- `driveId`: Ref -> `drives`
- `roleTitle`: String
- `questions`: Array of `{ questionId: String, text: String, skillTag: String }`
- `answers`: Array of `{ questionId: String, transcript: String, aiFeedback: String, score: Number }`
- `overallScore`: Number
- `technicalScore`: Number
- `communicationScore`: Number
- `status`: String (`in_progress`, `completed`)
- `completedAt`: Date

### 2.6 `workshops` & `workshop_enrollments`
- `_id`: ObjectId
- `title`: String
- `targetSkills`: Array of String (Indexed)
- `instructor`: String
- `scheduledAt`: Date
- `capacity`: Number
- `mode`: String (`Online`, `Offline`, `Hybrid`)
- `locationInfo`: String
- `targetDriveIds`: Array of Ref -> `drives`
- `assignedStudentIds`: Array of Ref -> `students`
- `postAssessmentQuestions`: Array of Questions

- `workshop_enrollments`:
  - `workshopId`: Ref -> `workshops`
  - `studentId`: Ref -> `students`
  - `registeredAt`: Date
  - `attended`: Boolean (Default: `false`)
  - `postAssessmentScore`: Number
  - `preWorkshopSkillScores`: Map<String, Number>
  - `postWorkshopSkillScores`: Map<String, Number>
  - `readinessDelta`: Number

### 2.7 `readiness_scores`
- `_id`: ObjectId
- `studentId`: Ref -> `students` (Indexed)
- `driveId`: Ref -> `drives` (Indexed)
- `overallReadiness`: Number (0-100%)
- `stageReadiness`: Map<String, Number>
- `missingSkills`: Array of `{ skillName: String, currentScore: Number, targetScore: Number, gap: Number }`
- `riskLevel`: String (`Low`, `Medium`, `High`)
- `calculatedAt`: Date

### 2.8 `notifications`
- `_id`: ObjectId
- `userId`: Ref -> `users` (Indexed)
- `title`: String
- `message`: String
- `type`: String (`workshop_assigned`, `readiness_updated`, `post_assessment_available`)
- `read`: Boolean (Default: `false`)
- `createdAt`: Date

## 3. Indexes
- `users`: `{ email: 1 }`
- `students`: `{ userId: 1 }`, `{ registrationNumber: 1 }`
- `readiness_scores`: `{ studentId: 1, driveId: 1 }`
- `workshop_enrollments`: `{ workshopId: 1, studentId: 1 }`
