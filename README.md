# Achalasia ML Research Project Plan

## Working Title

**Achalasia Patient Pathways: An Exploratory Data Science Study of Symptom Trajectories, Risk Factors, and Treatment Outcomes**

## Core Aim

Build an open, reproducible data science pipeline to explore patterns in achalasia patient histories, symptom progression, diagnostic delays, treatment choices, and outcomes.

## 1. Research Framing

### Main Research Question

Can self-reported patient history and symptom data reveal meaningful subgroups or trajectories among people diagnosed with achalasia?

### Secondary Questions

* Do patients with Type I, Type II, and Type III achalasia report different symptom timelines?
* How common is reflux-like illness before achalasia diagnosis?
* Are there clusters of patients based on pre-diagnosis symptoms, suspected triggers, or comorbidities?
* What factors are associated with delayed diagnosis?
* What factors are associated with post-treatment reflux after POEM or Heller myotomy?
* Do treatment outcomes differ by subtype, reflux history, age, or symptom duration?

## 2. Repo Structure

```text
achalasia-ml-study/
│
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── requirements.txt
├── pyproject.toml
├── .gitignore
│
├── docs/
│   ├── project_overview.md
│   ├── research_questions.md
│   ├── ethics_and_privacy.md
│   ├── data_dictionary.md
│   ├── survey_design.md
│   ├── analysis_plan.md
│   ├── limitations.md
│   └── paper_outline.md
│
├── data/
│   ├── raw/              # Not committed if identifiable
│   ├── interim/          # Cleaned but not final
│   ├── processed/        # Anonymised analysis-ready data
│   └── synthetic/        # Fake example data for repo/testing
│
├── notebooks/
│   ├── 01_exploratory_analysis.ipynb
│   ├── 02_symptom_timelines.ipynb
│   ├── 03_clustering.ipynb
│   ├── 04_treatment_outcomes.ipynb
│   └── 05_figures_for_paper.ipynb
│
├── src/
│   └── achalasia_ml/
│       ├── __init__.py
│       ├── config.py
│       ├── load_data.py
│       ├── clean_data.py
│       ├── features.py
│       ├── analysis.py
│       ├── clustering.py
│       ├── modelling.py
│       ├── visualisation.py
│       └── utils.py
│
├── tests/
│   ├── test_clean_data.py
│   ├── test_features.py
│   └── test_synthetic_data.py
│
├── scripts/
│   ├── generate_synthetic_data.py
│   ├── run_cleaning_pipeline.py
│   └── run_analysis_pipeline.py
│
├── outputs/
│   ├── figures/
│   ├── tables/
│   └── reports/
│
└── paper/
    ├── manuscript.md
    ├── abstract.md
    ├── references.bib
    └── figures/
```

---

## 3. README.md Draft

```markdown
# Achalasia ML Study

An exploratory data science project investigating self-reported symptom trajectories, diagnostic pathways, and treatment outcomes in achalasia.

## Purpose
Achalasia is a rare oesophageal motility disorder with unclear causes and often delayed diagnosis. This project aims to build a reproducible analytical pipeline for exploring patient-reported patterns and generating future research hypotheses.

## Key Questions
- What symptom trajectories are reported before diagnosis?
- How often do reflux-like symptoms precede dysphagia?
- Are there identifiable patient subgroups using unsupervised learning?
- What factors are associated with diagnostic delay?
- What factors are associated with post-treatment reflux or persistent symptoms?

## Important Disclaimer
This project is exploratory and does not attempt to prove causation. Findings should be interpreted as hypothesis-generating only.

## Data
No identifiable patient data should be committed to this repository. Synthetic data is provided for demonstration and testing.

## Status
Early planning / exploratory phase.
```

---

## 4. Ethics and Privacy

### Core Principle

Patient data must be treated as sensitive health data.

### Rules

* Do not commit raw identifiable data to GitHub.
* Use synthetic data for public demos.
* Store real survey data securely and separately.
* Avoid collecting unnecessary identifying information.
* Use age bands rather than exact date of birth.
* Use approximate timelines rather than exact dates where possible.
* Be transparent with participants about how data will be used.

### Consent Wording Concepts

Participants should understand:

* The project is exploratory research.
* Participation is voluntary.
* Data will be anonymised before analysis.
* They can skip questions.
* No medical advice will be given.
* Results may be shared publicly in aggregate form.

### Important Note

If collaborating with a charity, university, NHS service, or journal, formal ethics approval may be required.

---

## 5. Survey Design

### Sections

#### A. Demographics

* Age band
* Sex
* Country/region
* Ethnicity, optional and carefully phrased
* Height/weight change bands, optional

#### B. Diagnosis

* Age at first symptoms
* Age at diagnosis
* Achalasia type: I / II / III / unknown
* Diagnostic tests used:

  * Gastroscopy
  * Barium swallow
  * Manometry
  * pH study
  * CT scan

#### C. Symptom Timeline

* First major symptom
* Reflux-like symptoms before diagnosis
* Dysphagia onset
* Solids vs liquids
* Regurgitation
* Chest pain
* Weight loss
* Night symptoms
* Aspiration/coughing

#### D. Possible Preceding Factors

These must be framed carefully as associations, not causes.

* Significant viral illness before symptoms
* COVID history
* Autoimmune diagnosis
* Allergy/atopy history
* Major stress period
* Surgery/trauma history
* Medication history
* Opioid use
* Cannabis use
* Smoking/vaping
* Alcohol intake
* Dietary patterns

#### E. Comorbidities

* GERD/reflux diagnosis
* Hiatus hernia
* IBS
* thyroid disease
* autoimmune disease
* connective tissue disease
* neurological disease

#### F. Treatment

* POEM
* Heller myotomy + fundoplication
* Balloon dilation
* Botox
* Medication only
* Awaiting treatment

#### G. Outcomes

* Swallowing improvement
* Regurgitation improvement
* Reflux after treatment
* Need for PPIs
* Repeat procedures
* Satisfaction score
* Current diet freedom

---

## 6. Data Dictionary Example

| Field                   | Type     | Description                                       |
| ----------------------- | -------- | ------------------------------------------------- |
| participant_id          | string   | Random anonymous ID                               |
| age_band                | category | Age group                                         |
| sex                     | category | Self-reported sex                                 |
| country                 | category | Country of residence                              |
| achalasia_type          | category | Type I / II / III / unknown                       |
| symptom_duration_years  | numeric  | Time from first symptom to diagnosis              |
| reflux_before_dysphagia | boolean  | Reflux-like symptoms before swallowing difficulty |
| treatment_type          | category | POEM / Heller / dilation / Botox / none           |
| post_treatment_reflux   | category | none / mild / moderate / severe                   |
| current_diet_score      | ordinal  | 1 = liquid only, 5 = unrestricted                 |

---

## 7. Analysis Plan

### Phase 1: Descriptive Statistics

* Age at symptom onset
* Time to diagnosis
* Symptom frequencies
* Treatment breakdown
* Post-treatment outcome summaries

### Phase 2: Timeline Analysis

* Common symptom orderings
* Reflux-first vs dysphagia-first groups
* Diagnostic delay distributions

### Phase 3: Clustering

Explore whether patients group naturally by:

* symptom trajectory
* reflux history
* subtype
* comorbidities
* treatment outcomes

Potential methods:

* k-means on engineered features
* hierarchical clustering
* UMAP/t-SNE visualisation
* Gaussian mixture models
* latent class analysis if appropriate

### Phase 4: Predictive Modelling

Hypothesis-generating models only.

Potential targets:

* diagnostic delay > 2 years
* post-POEM reflux
* persistent dysphagia after treatment
* high diet restriction after treatment

Potential models:

* logistic regression
* random forest
* gradient boosting
* calibrated models for interpretability

### Phase 5: Interpretability

Use:

* feature importance
* SHAP values
* partial dependence plots
* cautious interpretation

---

## 8. Main Limitations

* Self-selection bias from patient communities
* Recall bias in symptom timelines
* Small sample size due to rarity
* Confounding between symptoms and diagnosis timing
* Treatment outcomes influenced by surgeon/centre experience
* Association does not imply causation

---

## 9. Potential Paper Structure

### Abstract

Brief summary of exploratory study, methods, findings, limitations.

### Introduction

* Achalasia overview
* Diagnostic delay problem
* Unknown aetiology
* Need for patient-centred datasets

### Methods

* Survey design
* Recruitment
* Data cleaning
* Feature engineering
* Statistical/ML methods

### Results

* Cohort description
* Symptom timelines
* Clusters/subgroups
* Treatment outcomes
* Reflux trajectory findings

### Discussion

* Interpretation
* Comparison with existing literature
* Hypotheses generated
* Limitations
* Future work

### Conclusion

Exploratory patient-reported data may reveal meaningful symptom trajectories and outcome patterns that justify future prospective studies.

---

## 10. Minimum Viable Project

### MVP Goal

Build a working open-source pipeline using synthetic data before collecting real data.

### MVP Steps

1. Create GitHub repo.
2. Add README, ethics note, survey draft, data dictionary.
3. Generate synthetic dataset of 500 fake patients.
4. Build cleaning pipeline.
5. Build exploratory notebook.
6. Build simple clustering notebook.
7. Write a mock results report.
8. Contact charity/patient group with a professional proposal.

---

## 11. Suggested First Milestone

**Milestone 1: Reproducible Synthetic Pipeline**

Deliverables:

* Repo structure complete
* Synthetic dataset generated
* Data dictionary complete
* EDA notebook complete
* Initial clustering demo complete
* Draft survey complete

This allows the project to be shown to charities or clinicians without needing real patient data yet.

---

## 12. Charity / Clinician Collaboration Pitch

Short pitch:

> I am an ML engineer and achalasia patient developing an exploratory, privacy-conscious data science project to analyse patient-reported achalasia symptom pathways and treatment outcomes. I would like to collaborate with patient organisations and clinicians to design a responsible survey and open analytical framework. The aim is to generate structured hypotheses and to better understand patient trajectories.

---

## 13. Immediate Next Actions

1. Create repo: `achalasia-ml-study`
2. Add documentation files.
3. Draft survey in Markdown.
4. Create synthetic dataset generator.
5. Build first exploratory analysis notebook.
6. Prepare short pitch to Achalasia Action or similar charity.
7. Identify one clinician or academic advisor if possible.
