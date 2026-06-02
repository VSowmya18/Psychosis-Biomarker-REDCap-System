# 🧠 Psychosis Biomarker Study - REDCap Clinical Research Database

A REDCap-based clinical research data collection and workflow management system designed for a seronegative autoimmune encephalitis (AIE) and psychosis biomarker study. The system supports the full research workflow - from rapid patient screening through longitudinal follow-up and outcome assessment.

---

## 🔬 Study Overview

This project supports a psychiatric biomarker research study investigating the intersection of psychotic presentations and autoimmune encephalitis. The REDCap system was built to:

- Screen potential participants against standardized inclusion/exclusion criteria
- Capture structured phenotypic and clinical presentation data
- Support autoimmune and neurologic differential diagnosis workflows
- Track laboratory, imaging, and treatment information
- Manage enrollment decisions and longitudinal follow-up reviews
- Improve data quality and consistency across multi-role study personnel

**Data sources:** Clinical documentation, psychiatric evaluations, laboratory results, imaging studies, and treatment records abstracted by research coordinators, medical students, and clinical trainees.

---

## 📋 Instruments (7 Total - 294 Fields)

| Instrument | Fields | Purpose |
|---|---|---|
| Psychosis Biomarker Exclusion Review | 9 | Initial rapid screening and eligibility determination |
| Post Review & Study Status | 21 | Enrollment decision, study status tracking, and follow-up management |
| Clinical Questionnaire | 86 | Comprehensive phenotypic data - demographics, psychiatric history, mental status exam, precipitating events |
| Brief Psychiatric Rating Scale (BPRS) | 15 | Standardized psychiatric symptom severity scoring with auto-calculated total |
| Autoimmune Encephalitis (AIE) Scoring | 18 | Graus criteria and APE2 score implementation with automated criteria adjudication |
| Labs | 68 | CSF analysis, hematology, autoimmune panels (ANA, TPO, GAD65, and others), neuronal antibody testing |
| Treatments | 77 | Immunosuppressive and psychiatric medication tracking with dosing, frequency, dates, and adverse reactions |

---

## ⚙️ Advanced REDCap Features Used

### Branching Logic
126 of 294 fields are conditionally displayed based on prior responses, keeping instruments clean and context-appropriate for each participant's clinical presentation. Examples include:

- Eligibility pathway branching after brief screening review
- Conditional lab sub-sections (CSF, hematology, autoimmune) shown only if the test was ordered
- Treatment detail fields appearing only for selected agents

### Calculated Fields & `@CALCTEXT` Annotations
- **BPRS Total Score** - auto-summed from 7 symptom subscale ratings
- **APE2 Score** - auto-summed from 6 clinical domain scores
- **MoCA Interpretation** - `@CALCTEXT` displays cognitive tier label (Normal / Mild / Moderate / Severe impairment) based on numeric score
- **Insight Interpretation** - `@CALCTEXT` maps numeric rating to descriptive clinical text
- **Graus Criteria Board** - `@HIDDEN @CALCTEXT` adjudicates Graus criteria (subacute onset + exclusion of alternatives + supportive features) and returns a pass/fail determination
- **APE2 Criteria Met** - `@HIDDEN @CALCTEXT` evaluates all six APE2 domains simultaneously and returns criteria status

### Conditional Banner Alerts
Three-tier color-coded status banners communicate real-time workflow state to users:

| Banner | Condition | Meaning |
|---|---|---|
| 🟢 Green | `final_status = Enrolled` AND `case_closure = Complete` | Participant fully enrolled and chart review closed |
| 🟡 Yellow | Post-review incomplete OR follow-up needed OR case open | Pending coordinator review or additional data required |
| 🔴 Red | `final_status = Excluded` AND `case_closure = Excluded` | Participant excluded; record closed |

### Form Display Logic
Instrument availability is gated by eligibility pathway - downstream instruments are only accessible after appropriate upstream forms are completed, enforcing the screening → enrollment → data collection → follow-up workflow order.

### Piping & Embedded Field References
Key decision variables (e.g., `[final_status]`, `[followup_needed]`, `[screening_eligibility]`) are piped across instruments to display contextual reminders and status indicators inline, reducing the need for users to navigate between forms.

### Longitudinal Structure
- Data is anchored to the patient's enrolled presentation and sample collection timepoint
- Follow-up workflows keep cases open for additional laboratory results, imaging, symptom assessments, or future reassessment
- The `followup_needed` flag drives dynamic re-review logic across the Post Review instrument

### Role-Based Workflow Guidance
Descriptive fields include embedded instructions differentiated by role - medical students are directed to save incomplete forms for coordinator review when unable to locate clinical information, supporting data quality across experience levels.

---

## 🛠️ Tools & Platform

- **Platform:** REDCap (Research Electronic Data Capture)
- **Features used:** Branching logic, calculated fields, `@CALCTEXT`, `@HIDDEN`, piping, conditional banner alerts, form display logic, longitudinal events, role-based workflow design
- **Instruments:** 7
- **Total fields:** 294
- **Fields with branching logic:** 126 (43%)

---
