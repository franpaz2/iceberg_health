# Iceberg Health
**Automated Clinical Auditing System for Polypharmacy Patients**

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![HTMX](https://img.shields.io/badge/HTMX-336699?style=for-the-badge&logo=htmx&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Claude](https://img.shields.io/badge/Claude_Sonnet_4.6-D97757?style=for-the-badge&logo=anthropic&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

> **Iceberg Health** is a clinical auditing SaaS engine designed to transform unstructured medical histories into deterministic medical alerts. It combines the power of advanced NLP with an algorithmic rule engine to prevent prescription errors in milliseconds.

---

## The Clinical Problem
Primary care physicians and geriatricians deal daily with **polypharmacy** patients (taking 10+ daily drugs). Manually reviewing an unstructured clinical history (*"takes paracetamol in the morning, and sometimes adiro"*) to detect severe interactions, incorrect renal dosages, or contraindications takes between **15 and 30 minutes per patient**. 

This manual process is prone to human error, which can lead to emergency room admissions due to pharmacological toxicity or prescription failures.

## The Solution
Iceberg Health automates this exhaustive review through a 3-phase workflow, protecting the patient and saving the healthcare system thousands of hours of administrative work.

---

## Technical Architecture (3-Phase Pipeline)

The project is a reactive full-stack web application built on **FastAPI, HTMX, and Tailwind CSS**, driven by a powerful Python auditing engine.

### Phase 1: Free NLP Extraction (The Intelligence)
The physician inputs the clinical history in free text. The system makes an API call to **Claude Sonnet 4.6** (via OpenRouter) using advanced *Prompt Engineering*.
* **Input:** Unstructured clinical text.
* **Processing:** Inference of sex, age, chronic diseases (asthma, fall risk, renal problems), and medication with posology (dosage).
* **Output:** Structured JSON ready for computation.

### Phase 2: Taxonomy & Pharmacological Enrichment
The system classifies the extracted drugs into canonical families (e.g., *NSAIDs, SSRIs, Benzodiazepines*) and executes a clinical chronopharmacology analysis to detect posological errors (e.g., drugs prescribed at night that require fasting).

### Phase 3: Deterministic Industrial Audit (The Brain)
**Zero medical hallucinations.** Instead of relying on an LLM to evaluate interactions, the system uses **Pandas** and a proprietary *Fuzzy Matching* algorithm to cross-reference the extracted JSON against a **Master Database containing over 30,000 records from AEMPS(CIMA)** (Spanish Agency of Medicines and Medical Devices).
The engine instantaneously evaluates:
- Severe interactions between prescribed drugs.
- Contraindications due to pregnancy/lactation.
- Dosage adjustments for renal impairment.
- Inability to crush pills (patients with dysphagia).
- Fall risk in geriatric patients and cross-allergies.

---

## Impact & Results

| Metric | Traditional Process | With Iceberg Health |
| :--- | :--- | :--- |
| **Audit Speed** | 15 - 30 minutes | **< 1 minute** |
| **Reliability** | Dependent on the human factor | **100% Deterministic and Traceable** |
| **UI / UX** | Legacy medical software (slow) | **HTMX Reactivity (No reloads)** |

## Tech Stack
* **Backend:** Python 3.10+, FastAPI, Pandas, FuzzyWuzzy/TheFuzz.
* **Frontend:** HTMX, Tailwind CSS, Jinja2.
* **AI & NLP:** Claude Sonnet 4.6 (OpenRouter API), Prompt Engineering.
* **Data:** Non-relational database (AEMPS(CIMA)).

---
*Developed as part of the **Iceberg Datum** ecosystem of solutions.*
