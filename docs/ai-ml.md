# CampusPulse — AI/ML Services Architecture

## 1. Overview
CampusPulse incorporates dynamic AI/ML models and deterministic scoring adapters for:
1. Company-Specific Readiness Evaluation
2. Skill-Gap Detection & Cohort Aggregation
3. AI Mock Interview Simulator & Feedback Generator
4. Proctoring Integrity Adapter
5. Pre vs Post Workshop Impact Calculation
6. Resume - JD Compatibility Engine

## 2. Multi-Factor Readiness Scoring Model

Readiness is evaluated against a specific **Company Drive ($D$)** rather than generically.

$$\text{Readiness}(S, D) = w_{\text{acad}} \cdot R_{\text{acad}} + w_{\text{apt}} \cdot R_{\text{apt}} + w_{\text{tech}} \cdot R_{\text{tech}} + w_{\text{interview}} \cdot R_{\text{int}}$$

Where:
- $R_{\text{acad}} = \min(1.0, \frac{\text{CGPA}}{\text{Min CGPA Target}})$
- $R_{\text{apt}}$: Aptitude & Reasoning assessment percentile (0-100%)
- $R_{\text{tech}} = \frac{1}{N} \sum_{k=1}^N \min(1.0, \frac{\text{Student Skill Score}_k}{\text{Target Skill Threshold}_k})$
- $R_{\text{int}}$: AI Mock Interview Score (0-100%)
- Standard Weights: $w_{\text{acad}} = 0.15, w_{\text{apt}} = 0.25, w_{\text{tech}} = 0.35, w_{\text{interview}} = 0.25$

Risk Level Classification:
- **Ready**: Readiness $\ge 75\%$
- **Medium Risk**: $55\% \le \text{Readiness} < 75\%$
- **High Risk**: Readiness $< 55\%$

## 3. Skill-Gap Engine & Cohort Aggregation
- **Individual Skill Gap**:
  $$\text{Gap}_k = \text{TargetScore}_k - \text{CurrentScore}_k \quad (\text{if TargetScore}_k > \text{CurrentScore}_k)$$
- **College-Level Cohort Detection**:
  Groups students sharing identical target skill deficiencies for upcoming company drives:
  $$\text{Cohort Impact} = \text{Count}(\text{Students with } \text{Gap}_k > 15\%)$$
  Triggers automatic placement officer alert to launch a college intervention workshop.

## 4. AI Mock Interview Service
- Pluggable Adapter pattern using Google Gemini API (`gemini-1.5-flash` / `gemini-2.0-flash`) or local rule-based fallback.
- Technical evaluation parameters:
  - Technical Accuracy (1-10)
  - Clarity & Structure (1-10)
  - Depth of Explanation (1-10)
  - Soft Skill / Communication (1-10)

## 5. Online Proctoring Integrity Model
Integrity score decays dynamically during assessments based on detected flags:
$$\text{IntegrityScore} = 100 - \sum \text{Flag Weight}_i$$
Flag Weights:
- Phone Detected: $-25$
- Multiple Persons Detected: $-30$
- Face Missing / Not Detected: $-15$
- Tab Switch / Focus Lost: $-10$ per event

## 6. Real Impact Calculation Formula (Post-Workshop Reassessment)
Never fake improvement metrics! Impact is strictly computed from stored pre and post assessment scores:

$$\Delta_{\text{Skill}} = \text{PostWorkshopSkillScore} - \text{PreWorkshopSkillScore}$$
$$\Delta_{\text{Readiness}} = \text{Readiness}_{\text{Post}} - \text{Readiness}_{\text{Pre}}$$
$$\text{Gap Reduction} = \max(0, \text{Gap}_{\text{Pre}} - \text{Gap}_{\text{Post}})$$
