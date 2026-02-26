# Example Prompts and Expected Behavior

## 1. Full Review (Default Mode)

### Prompt

> Review the following manuscript as a blinded peer reviewer. [Attach or paste full manuscript]

### Expected behavior

- Material inventory listing all sections received
- Review confidence rated as **Full** (if complete) or **Limited** (if partial)
- All 12 output sections produced (0 through 11)
- Default mode: `FULL_METHODS + CONSISTENCY_AUDIT`

---

## 2. Rapid Editorial Triage

### Prompt

> Mode: RAPID_SCREEN. Triage this manuscript for likely reject vs revision. Focus only on validity-threatening flaws and major reporting omissions.
>
> [Paste abstract + key methods + results]

### Expected behavior

- Material inventory noting that only abstract, methods, and results were provided
- Review confidence rated as **Limited**
- High-level assessment focused on fatal flaws and major concerns
- Abbreviated output focused on decision-critical issues

---

## 3. Consistency Audit Only

### Prompt

> Mode: CONSISTENCY_AUDIT. Audit the provided abstract, Table 1, Table 2, and figure captions for internal numerical and metric consistency only. Do not perform a full methodological critique.
>
> [Paste materials]

### Expected behavior

- Section 7 (Internal Consistency Audit) is the primary output
- Other sections marked as not applicable to this mode
- Specific mismatch citations with locations (e.g., "Abstract states N=342 but Table 1 reports N=338")

---

## 4. Non-specialist Statistical Pass

### Prompt

> Mode: STATS_SIMPLE. Assess denominator clarity, missingness, endpoint definition, multiplicity, effect size/CI reporting, and whether a simpler analysis is more appropriate.
>
> [Paste methods and results sections]

### Expected behavior

- Section 8 (Statistical Review) is the primary output
- Simple-first checks prioritized over advanced statistical concerns
- Clear yes/no assessments for each checklist item

---

## 5. Revision Response Audit

### Prompt

> Mode: REVISION_RESPONSE_AUDIT. Here is the revised manuscript, the original reviewer comments, and the authors' point-by-point response letter. Assess whether the revision adequately addresses the prior concerns.
>
> --- REVIEWER COMMENTS ---
> [Paste reviewer comments]
>
> --- RESPONSE LETTER ---
> [Paste authors' response]
>
> --- REVISED MANUSCRIPT ---
> [Paste revised manuscript]

### Expected behavior

- Uses the REVISION_RESPONSE_AUDIT output format (not the standard format)
- Comment-by-comment audit with assessment ratings
- New issues introduced by revision are flagged
- Overall revision trajectory assessed

---

## 6. Partial Manuscript (Abstract Only)

### Prompt

> Review this abstract for a cross-sectional study on nurse burnout and patient safety outcomes.
>
> **Background:** Nurse burnout is associated with adverse patient outcomes. This cross-sectional study examined the relationship between burnout scores and medication error rates across 12 hospitals.
>
> **Methods:** We surveyed 1,247 nurses using the Maslach Burnout Inventory and linked responses to unit-level medication error reports over 6 months. Multivariable logistic regression adjusted for nurse experience, unit type, and hospital size.
>
> **Results:** Higher emotional exhaustion scores were significantly associated with increased medication errors (OR 2.3, 95% CI 1.4-3.8, p<0.001). The association remained significant after adjustment (aOR 1.9, 95% CI 1.2-3.1, p=0.008). Hospitals with >40% high-burnout nurses had 3.1x the error rate.
>
> **Conclusion:** Nurse burnout causes medication errors. Hospitals should implement burnout prevention programs to improve patient safety.

### Expected output (abbreviated)

```
### 0) Material Inventory and Review Scope
- Received: Abstract only
- Not received: Introduction, Methods (full), Results (full), Discussion, Tables, Figures, Supplementary Materials, References
- Review confidence: **Limited** — only the abstract was provided

### 1) Overall Recommendation
- Major Revision
- The conclusion makes causal claims unsupported by the cross-sectional design, and key methodological details cannot be verified from the abstract alone.

### 2) Summary Assessment
This study examines the association between nurse burnout (Maslach Burnout Inventory) and medication error rates across 12 hospitals using a cross-sectional design with multivariable logistic regression. The topic is relevant and the sample size appears adequate. However, the conclusion overstates the findings by using causal language ("causes") from a cross-sectional design. The unit of analysis appears mixed (individual nurse survey linked to unit-level error reports), raising ecological fallacy concerns.

### 3) Fatal Flaws
- The conclusion states burnout "causes" medication errors. A cross-sectional design cannot establish causation. This is a fundamental overclaim that misrepresents the study's evidence.

### 4) Major Concerns
- Issue: Unit of analysis mismatch
  Where it appears: Methods/Results in abstract
  Why it matters: Individual-level burnout scores are linked to unit-level error reports, creating an ecological fallacy risk. The logistic regression treats this as individual-level data without acknowledging the clustered structure.
  What would strengthen it: Clarify the analytic unit, use multilevel modeling to account for hospital/unit clustering, or reframe as a unit-level analysis.

- Issue: The "3.1x error rate" statistic
  Where it appears: Results
  Why it matters: This appears to be a different metric (rate ratio) than the OR/aOR reported for the primary analysis, but is presented without a confidence interval, p-value, or clear denominator. It is also based on an unclear threshold (">40% high-burnout nurses") that may be post hoc.
  What would strengthen it: Report with uncertainty interval, clarify how the threshold was selected, and state whether this was a prespecified analysis.

### 9) Supplementary Materials Assessment
Supplementary materials were not provided and are not referenced in the abstract. Given the multilevel data structure and multiple analytical approaches implied, supplementary materials detailing the full model specifications would strengthen reproducibility.

### 10) Claims That Overreach the Evidence
- "Nurse burnout causes medication errors" → "Nurse burnout was associated with medication errors in this cross-sectional analysis"
- "Hospitals should implement burnout prevention programs to improve patient safety" → This prescriptive conclusion requires interventional evidence not provided by this design
```

---

## 7. ML/Prediction Model Manuscript

### Prompt

> Review the following manuscript describing a machine learning model for predicting 30-day hospital readmission using electronic health records.
>
> [Paste full manuscript]

### Expected behavior

- ML-specific red flags checked: data leakage, train/test separation, external validation, feature preprocessing, overfitting risk
- TRIPOD/TRIPOD-AI guideline awareness applied
- Calibration and discrimination metrics assessed for consistency
- Model versioning and feature definitions checked between methods and results

---

## 8. Manuscript with Supplementary Materials

### Prompt

> Review this manuscript. The supplementary materials are included after the main text.
>
> --- MAIN MANUSCRIPT ---
> [Paste main text]
>
> --- SUPPLEMENTARY MATERIALS ---
> [Paste supplementary tables, figures, methods]

### Expected behavior

- Supplementary materials explicitly audited for consistency with main text
- Methods deferred to supplements checked for completeness
- Section 9 (Supplementary Materials Assessment) fully populated
- Cross-references between main text and supplements verified

---

## 9. Manuscript Referencing Supplements Not Provided

### Prompt

> Review this manuscript. Note: I do not have the supplementary materials available.
>
> [Paste main text that references "see Supplementary Table S1", "detailed in Supplementary Methods", etc.]

### Expected behavior

- Section 9 flags all supplement references found in the text
- Claims dependent on supplementary data noted as unverifiable
- Classified as Major Concern if key methods or results are deferred to missing supplements
- Material Inventory clearly lists supplementary materials as not received
