# Expert Rules Algorithm for Rare Disease Detection - Detailed Outline

**Function:** ExpertRules(patient_id)

**Input:** Patient diagnosis, lab, clinical, and drug data

**Output:** Rule classifications (Rule1-Rule5)

---

## Rule 1: Baseline Hematological-Organomegaly Rule

**if** (General organomegaly [R19.00, R19.05, R19.06, R19.09] OR Hepatosplenomegaly [R16.2] OR Hepatomegaly [R16.0] OR Splenomegaly [R16.1]) AND Abnormal CBC (WBC, Hemoglobin, Platelet, or Neutrophil) **then**
- Rule1 ← TRUE

### Sub-conditions for Organomegaly:

**if** General organomegaly [R19.00, R19.05, R19.06, R19.09] **then**
- R19.00: Intra-abdominal and pelvic swelling, mass and lump, unspecified site
- R19.05: Other intra-abdominal and pelvic swelling, mass and lump  
- R19.06: Epigastric swelling, mass or lump
- R19.09: Other intra-abdominal and pelvic swelling, mass and lump

**if** Hepatosplenomegaly [R16.2] **then**
- R16.2: Hepatosplenomegaly, not elsewhere classified
- Definition: Simultaneous enlargement of both liver and spleen

**if** Hepatomegaly [R16.0] **then**
- R16.0: Hepatomegaly, not elsewhere classified
- Definition: Liver enlargement only

**if** Splenomegaly [R16.1] **then**
- R16.1: Splenomegaly, not elsewhere classified
- Definition: Spleen enlargement only

### Sub-conditions for Abnormal CBC:

**if** patient has received velaglucerase alfa OR imiglucerase parenteral **then**
- Search method: Case-insensitive search in drug dataset
- Lab filtering: Use only labs obtained BEFORE first ERT date
- Fallback: If no pre-ERT labs exist for specific parameter, use ALL available labs for that parameter

**else**
- Lab selection: Use ALL available laboratory values

**For each CBC parameter (WBC, Hemoglobin, Platelet, Neutrophil):**
- Priority 1: Most recent lab value BELOW reference range
- Priority 2: If no below-range values, most recent lab value ABOVE reference range  
- Priority 3: If no abnormal values, most recent lab value overall

**Reference ranges:**
- WBC: 4.5-11.0 × 10³/μL
- Hemoglobin: 132-173 g/L
- Platelet: 140-400 × 10³/μL
- Neutrophil: 1.8-7.7 × 10³/μL

---

## Rule 2: Growth-Associated Hematological Rule

**if** Growth retardation [R62.50, R62.51, R62.52, R62.59] AND Rule1 **then**
- Rule2 ← TRUE

### Sub-conditions for Growth retardation:

**if** Growth retardation [R62.50, R62.51, R62.52, R62.59] **then**
- R62.50: Delayed milestones in childhood
- R62.51: Failure to thrive in child
- R62.52: Short stature (child)
- R62.59: Other lack of expected normal physiological development in childhood

### Dependencies:
- Rule1 must be TRUE

---

## Rule 3: Comprehensive Growth-Associated Rule

**if** (Growth retardation [R62.50, R62.51, R62.52, R62.59] OR Failure to thrive [R62.7] OR Height/Weight Centile < 3) AND Rule1 AND Rule2 **then**
- Rule3 ← TRUE

### Sub-conditions for Growth issues:

**if** Growth retardation [R62.50, R62.51, R62.52, R62.59] **then**
- Same as Rule 2 growth retardation codes

**if** Failure to thrive [R62.7] **then**
- R62.7: Adult failure to thrive

**if** Height/Weight Centile < 3 **then**
- Clinical measurement from Height/Weight Centile assessments
- Threshold: Below 3rd percentile

### Dependencies:
- BOTH Rule1 AND Rule2 must be TRUE

---

## Rule 4: Pulmonary-Associated Rule

**if** Interstitial lung disease [J84.9, J84.10, J84.112, J84.114, J84.848] AND Rule1 **then**
- Rule4 ← TRUE

### Sub-conditions for Interstitial lung disease:

**if** Interstitial lung disease [J84.9, J84.10, J84.112, J84.114, J84.848] **then**
- J84.9: Interstitial pulmonary disease, unspecified
- J84.10: Pulmonary fibrosis, unspecified
- J84.112: Idiopathic pulmonary fibrosis
- J84.114: Acute interstitial pneumonitis
- J84.848: Other specified interstitial pulmonary diseases

### Dependencies:
- Rule1 must be TRUE

---

## Rule 5: Neurological-Associated Rule

**if** Rule1 AND (Hypotonia [P94.1, P94.2] OR Developmental delay [R62.50, R62.59]) **then**
- Rule5 ← TRUE

### Sub-conditions for Neurological manifestations:

**if** Hypotonia [P94.1, P94.2] **then**
- P94.1: Hypertonia neonatorum
- P94.2: Congenital hypertonia

**if** Developmental delay [R62.50, R62.59] **then**
- R62.50: Delayed milestones in childhood
- R62.59: Other lack of expected normal physiological development in childhood

### Dependencies:
- Rule1 must be TRUE

---

## Final Classification

positive_prediction ← Rule1 OR Rule2 OR Rule3 OR Rule4 OR Rule5

**return** Rule1, Rule2, Rule3, Rule4, Rule5, positive_prediction