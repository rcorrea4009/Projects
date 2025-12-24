# 📑 Implementation Documentation  
## HeartGuard AI Dashboard

**Link:** https://codepen.io/rcorrea4009/full/jErObGM

**Project Version:** 1.0  
**Design Choice:** Clinical Professional (Style 1 / Expanded)  
**Objective:** Integrate a backend Machine Learning (ML) model with the existing HTML/JS frontend.

---

## 📘 Overview

This documentation provides a clear roadmap for transitioning the **Clinical Blue Dashboard** from a static mock-up into a fully functional, model-driven healthcare application.

---

## 🏗️ 1. Architectural Overview

To move from mock data to real predictions, the system will adopt a **standard Client–Server Architecture**:

- **Frontend (UI)**  
  Existing HTML / CSS / JavaScript dashboard

- **API Layer**  
  Backend bridge (Flask or FastAPI) that accepts user input and communicates with the ML model

- **Backend (ML Model)**  
  Trained Python model that processes clinical data and returns a risk probability

---

## 🔌 2. UI Logic Integration Plan

Once the ML model is ready, the following updates will be applied to the frontend logic.

### A. Input Data Normalization

The ML model expects numerical inputs (e.g., `0 = Female`, `1 = Male`).  
Dashboard dropdowns and sliders will be mapped to these values before sending data to the backend.

---

### B. Asynchronous Prediction (AJAX / Fetch)

The current `runAnalysis()` function (based on `if/else` logic) will be replaced with an API call using `fetch()`.

**Workflow:**

- **Trigger:** User clicks **Run AI Prediction**
- **Action:** JavaScript collects 14+ clinical variables from the form
- **Request:** Data is sent to the API as a JSON payload
- **Response:** UI displays a loading spinner until the model returns a confidence score

---

### C. Dynamic Result Rendering

The **Risk Level Gauge** and **Description Text** will update dynamically based on the model’s confidence score.

- **Low Risk (< 30%)**  
  🟢 Green theme

- **Moderate Risk (30% – 70%)**  
  🟡 Yellow / Orange theme

- **High Risk (> 70%)**  
  🔴 Red theme + triggers **Contact Doctor** alert

---

## 📊 3. Data Mapping Table

This table defines how UI fields map to ML model features.

| UI Field Name       | Model Feature Key | Type        | Example Range              |
|--------------------|------------------|-------------|----------------------------|
| Age                | `age`            | Integer     | 20 – 100                   |
| Blood Pressure     | `trestbps`       | Integer     | 90 – 200 mm Hg             |
| Cholesterol        | `chol`           | Integer     | 120 – 400 mg/dl            |
| Max Heart Rate     | `thalach`        | Integer     | 60 – 220 bpm               |
| Chest Pain Type    | `cp`             | Categorical | 0, 1, 2, 3                 |
| Result Output      | `prediction`     | Float       | 0.0 – 1.0 (Probability)   |

---

## 🚀 4. Future Feature Roadmap  
### (Post-Model Integration)

Once the ML model is live in the UI, the following high-value enhancements can be implemented:

- **SHAP Value Visualization**  
  Explain model decisions (e.g., *“Risk is high primarily due to Blood Pressure and Age”*)

- **Doctor’s Annotation Module**  
  Allow clinicians to override AI predictions or add clinical notes

- **PDF Report Generation**  
  Generate downloadable clinical-grade reports using `j
