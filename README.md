# TP53 Mutation and Overall Survival in TCGA Breast Cancer

## Question
Is TP53 mutation associated with overall survival in breast invasive carcinoma, and does subtype confound the relationship?

## Data
TCGA Breast Invasive Carcinoma (PanCancer Atlas), downloaded from cBioPortal (cbioportal.org/datasets). Files used: `data_clinical_patient.txt`, `data_mutations.txt`. Data files are not included here; download them from the link above.

## Methods
- Python (pandas, lifelines, matplotlib) in Google Colab
- Patients labeled TP53-mutated if they had at least one TP53 mutation in the mutation file (copy-number changes not included)
- Kaplan-Meier curves and log-rank tests for overall survival
- Subtype-stratified log-rank tests (Basal, Her2, LumA, LumB)
- Cox proportional hazards model adjusted for age and subtype

## Results
- 1,084 patients; 348 TP53-mutated, 736 not; 151 deaths total
- Overall log-rank p = 0.75 (no significant difference)
- TP53 mutation rate varied strongly by subtype (about 90% in Basal vs. about 11% in LumA), so subtype is a major confounder
- Within subtypes, only Her2 showed p < 0.05 (p = 0.016), based on 15 deaths and not significant after correcting for 4 tests
- Adjusted Cox model (n = 981): TP53 HR = 1.15 (95% CI 0.71-1.87, p = 0.58). Age was the clearest predictor (HR 1.04 per year)

## Limitations
"Altered" here means mutation only (copy-number changes are not included). A previous analysis using cBioPortal's built-in tools, which defines altered as mutation or copy-number change, gave log-rank p = 0.358 (n = 996). The difference is likely due to the different definition and patient cohort; this will be tested by adding copy-number data.
## Next steps
- Add copy-number data so "altered" matches cBioPortal's definition
- Repeat with disease-free / progression-free survival
- Split TP53 mutations by type (missense vs. truncating)
- Reproduce the analysis in R
