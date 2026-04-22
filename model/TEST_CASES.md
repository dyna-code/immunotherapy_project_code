# UI Test Cases — Immunotherapy Survival Prediction

Manual test cases for verifying the risk score calculation in the frontend.

> ⚠️ **Prerequisite:** Age must be entered in **years**, not days. The age field label says "Days" but the coefficient requires years. Ensure the fix `ageInDays / 365.25` is applied in `changeDataFormat()` before running these tests.


---

## Test Cases

### 🔴 TC-1: Extremely High Risk

| Field | Value |
|---|---|
| Age at Sequencing | `18` |
| Mutation Count | `1` |
| TMB (nonsynonymous) | `0.5` |
| Tumor Purity | `0.5` |
| Cancer Type | `Breast Cancer` |
| Drug Type | `PD-1 Inhibitor` |
| Sex | `Male` |
| Sample Type | `Metastatic` |

**Expected Output**

| Field | Expected |
|---|---|
| Risk Score | `2.92` |
| Approximate Median Survival | `0-3 months` |
| Risk Group | `Extremely High Risk` |

---

### 🟠 TC-2: High Risk

| Field | Value |
|---|---|
| Age at Sequencing | `55` |
| Mutation Count | `8` |
| TMB (nonsynonymous) | `6.0` |
| Tumor Purity | `0.4` |
| Cancer Type | `Non-Small Cell Lung Cancer` |
| Drug Type | `PD-1 Inhibitor` |
| Sex | `Male` |
| Sample Type | `Primary` |

**Expected Output**

| Field | Expected |
|---|---|
| Risk Score | `1.47` |
| Approximate Median Survival | `3-6 months` |
| Risk Group | `High Risk` |

---

### 🟡 TC-3: Moderate Risk

| Field | Value |
|---|---|
| Age at Sequencing | `55` |
| Mutation Count | `10` |
| TMB (nonsynonymous) | `7.0` |
| Tumor Purity | `0.4` |
| Cancer Type | `Glioma` |
| Drug Type | `PD-1 Inhibitor` |
| Sex | `Male` |
| Sample Type | `Primary` |

**Expected Output**

| Field | Expected |
|---|---|
| Risk Score | `1.16` |
| Approximate Median Survival | `6-12 months` |
| Risk Group | `Moderate Risk` |

---

### 🟢 TC-4: Low Risk

| Field | Value |
|---|---|
| Age at Sequencing | `65` |
| Mutation Count | `10` |
| TMB (nonsynonymous) | `8.0` |
| Tumor Purity | `0.35` |
| Cancer Type | `Melanoma` |
| Drug Type | `PD-1 Inhibitor` |
| Sex | `Female` |
| Sample Type | `Primary` |

**Expected Output**

| Field | Expected |
|---|---|
| Risk Score | `0.63` |
| Approximate Median Survival | `1-3 years` |
| Risk Group | `Low Risk` |

---

### 🔵 TC-5: Favorable

| Field | Value |
|---|---|
| Age at Sequencing | `55` |
| Mutation Count | `20` |
| TMB (nonsynonymous) | `15.0` |
| Tumor Purity | `0.4` |
| Cancer Type | `Renal Cell Carcinoma` |
| Drug Type | `PD-1 Inhibitor` |
| Sex | `Female` |
| Sample Type | `Primary` |

**Expected Output**

| Field | Expected |
|---|---|
| Risk Score | `0.34` |
| Approximate Median Survival | `>3 years` |
| Risk Group | `Favorable` |

---

## Risk Tier Thresholds Reference

| Risk Score (HR) | Risk Group | Approximate Median Survival |
|---|---|---|
| > 1.5 | 🔴 Extremely High Risk | 0–3 months |
| 1.2 – 1.5 | 🟠 High Risk | 3–6 months |
| 0.8 – 1.2 | 🟡 Moderate Risk | 6–12 months |
| 0.5 – 0.8 | 🟢 Low Risk | 1–3 years |
| < 0.5 | 🔵 Favorable | > 3 years |
