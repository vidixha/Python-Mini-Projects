# HyperAPI Extraction Analysis

EX: Extracted Output from HyperAPI

GT: Ground Truth from the form

### 1) In INDICATION CHECKLIST:
- Failed for all the forms that had indications checked. Returned a 1–2 item subset of a multi-item list. | Evidence: (ALL 10 forms with Indications selected; e.g. WGS Good 9-17 — GT 17 indications, EX 1)

### 2) In PATIENT INFORMATION section:
- Hallucination in date_of_birth (GT blank, EX `"1961-07-15"`). | Evidence: (BAD WES 1-9)
- Missed state (GT `"PA"`, EX `""`). | Evidence: (BAD WES 1-9)
- Missed phone (GT `"888-888-9999"`, EX `""`). | Evidence: (BAD WES 1-9)
- Accession number field swapped with address (GT accession_number `"404 Error Road"`, EX put it in `address` and left `accession_number` empty). | Evidence: (BAD WES 1-9)
- Hospital MRN misread (GT `"BBeam"`, EX `"Brown"`). | Evidence: (BAD WES 1-9)

### 3) In ORDERING PHYSICIAN section:
- Hallucinated / missed Ordering Physician name when the section was populated / crowded (GT `"Boston Childrens"`, EX `"Bob Builder"` — picked up the additional-report name). | Evidence: (MEDIUM WGS 73-81)
- Missed Institution Code (GT `"BCH"`, EX `""`). | Evidence: (MEDIUM WGS 73-81)
- Swapped phone / fax / email of Ordering Physician with Additional Report Recipient, and missed some fields in this section (GT phone `"711-000-000"` / fax `"710-000-000"` / email `"Boston@hospital.com"`; EX phone `"123-456-7890"` / fax `""` / email `"Bob@gmail.com"` — all pulled from the additional-report row). | Evidence: (MEDIUM WGS 73-81)

### 4) In PAYMENT section:

*Institutional Billing* sub-section:
- Clubbed Institution name and Institution code into one field (GT name `"Boston Childrens"` + code `"BCH"`; EX name `"Boston Childrens BCM"`, code `""`). | Evidence: (MEDIUM WGS 73-81)
- Institution contact email replaced with the additional-report email. | Evidence: (MEDIUM WGS 73-81)

*Insurance* sub-section:
- Missed Insurance fields entirely when Institutional Billing was also selected (GT `insurance.selected=true` + `insured_date_of_birth`, `patient_relationship_to_insured`, `member_policy_number`, `member_group_number` all populated; EX `insurance.selected=false` and every primary sub-field empty). | Evidence: (MEDIUM WGS 73-81)

### 5) In TEST CODE SECTION:
- Missed the Comparator Selections of Maternal / Paternal (GT `corresponding_comparator_tests.maternal=true` and `paternal=true`; EX Skipped the Extraction). Probably missed including in extraction JSON Schema. | Evidence: (MEDIUM WGS 73-81)

### 6) In PROBAND SAMPLE section:
- Underperformed / hallucinated in PROBAND SAMPLE section — wrong checkbox selected (GT `buccal_swab=true`; EX `blood_in_edta=true`). | Evidence: (MEDIUM WGS 73-81; same pattern in BAD WES 1-9)
- Misread date_of_collection (GT `"4/22/26"`, EX `"2026-11-22"`). | Evidence: (MEDIUM WGS 73-81)

### 7) In ITEMS CHECKLIST FOR TESTING:
- Hallucinated in selecting items — returned items that were not checked on the form, and returned them as machine-style identifiers instead of the human-readable list. | Evidence: (BAD WES 1-9 — EX returned `["proband_sample", "signed_consent_form", "clinical_note_summary", "requisition", "indication_for_study"]`)

### 8) In COMPARATOR INFORMATION section:
- Dates were hallucinated / mangled (GT maternal DOB `"2/21/96"` → EX `"01/1983"`; GT paternal DOB `"7/17/95"` → EX `"05/1950"`). | Evidence: (MEDIUM WGS 73-81)
- First name misread (GT paternal `"Uris"` → EX `"Iris"`). | Evidence: (MEDIUM WGS 73-81)
- Many forms had Symptomatic findings hallucinated — even though Yes/No was not selected on the form, the extracted output contained `yes=true` or `no=true`. Hit 13 of 18 forms. | Evidence: (BAD WES 1-9, BAD WES 23-31, BAD WES 45-53, GOOD WGS 19-27, GOOD WGS 9-17, MEDIUM WGS 1-9, … )

### 9) In ADDITIONAL REPORTS section:
- Whole `additional_reports[1]` row silently dropped on several bad-handwriting forms. | Evidence: (WGS Bad 13-21)
- Phone / fax left empty even when the row was clearly printed (e.g. `fax=""` when GT was `"123-456-7890"`). | Evidence: (MEDIUM WGS 73-81)

