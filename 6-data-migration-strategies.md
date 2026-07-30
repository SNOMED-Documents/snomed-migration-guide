# Data Migration Strategies

Most real migrations use a combination of strategies, applied to different data types based on their clinical value and the effort required to convert them.

## Full FHIR conversion

Legacy clinical records are fully converted to FHIR resources with SNOMED CT codes. The converted records are the primary live clinical records. Original data is retained alongside with provenance links.

**Appropriate for:** data essential for ongoing care — active diagnoses, current medications, allergies, surgical history, recent lab results. Data needed for AI model training, semantic search, or population analytics. Data that is accessed frequently and requires the highest quality coding.

**Effort profile:** High upfront (planning, mapping development, conversion pipeline, and testing — typically 8–15 months for a significant data set). Low ongoing once complete.

**Requirement:** Three-tier validation is essential — see [Testing and Verification](8-testing-and-verification.md).

## API integration (FHIR facade)

A FHIR API layer sits in front of the legacy system and translates requests at query time. Legacy data stays in place; FHIR-enabled consumers see a FHIR interface. No bulk conversion is required.

**Appropriate for:** important historical data accessed occasionally. A bridging strategy during phased migration. Large volumes where the ROI of full conversion is unclear.

**Effort profile:** Medium upfront (typically 2–4 months). Medium-to-high ongoing — two systems to maintain and ongoing conversion logic to update.

**Limitations:** Not optimal for high-volume queries or real-time analytics. AI model training on API-integrated data is technically challenging. Does not resolve the underlying data quality limitation long-term.

## Strategic archiving

Data is moved to long-term storage — searchable and accessible but not in live clinical systems.

**Appropriate for:** administrative data with no ongoing clinical use. Very old routine clinical data. Data required for compliance or audit but rarely retrieved. Not appropriate for allergies, chronic conditions, surgical history, immunisation records, or any data that could affect current care, regardless of age.

**Effort profile:** Low upfront and ongoing. Where possible, archive in FHIR format to preserve future compatibility.

## Hybrid approach

Most real-world migrations combine all three strategies, applied by data type and age. A representative hybrid:

| Data type | Recent (0–5 years) | Historical (5–15 years) | Older |
|---|---|---|---|
| Active diagnoses and medications | Full conversion | API integration | Archive |
| Lab results | Full conversion | API integration | Archive |
| Allergies | Full conversion | Full conversion | Full conversion |
| Administrative data | API integration (if needed) | Archive | Archive |

The hybrid approach typically reduces total cost by 30–50% compared to universal full conversion, while directing effort at the data types and time periods where clinical value is highest.

## Five principles that apply to every strategy

**Retain the original data.** Converted records are derivatives. The original has stronger medico-legal standing and is essential for re-conversion if mapping errors are discovered. Do not overwrite or delete source data during or after migration.

**Preserve clinical context.** The same SNOMED CT concept code means different things in different clinical contexts. A myocardial infarction code in a current problem list means the patient has the condition now; in a past-medical-history field it means they had it; in a differential diagnosis it is a possibility being considered. FHIR structured elements (clinicalStatus, verificationStatus, category) and SNOMED CT post-coordination must be used to carry this context correctly. Losing it is a patient safety issue.

**Track provenance.** Every converted record should carry a FHIR Provenance resource or equivalent documenting: the source system and original record identifier, the conversion date and process version, the mapping rules applied, and the validation outcome. In modern FHIR implementations, provenance is expected, not optional.

**Validate at all three tiers.** Automated validation catches technical errors. Standards validation catches FHIR conformance failures and SNOMED CT semantic errors. Clinical validation catches medical-appropriateness issues and context loss. Skipping any tier leaves a category of error undetected.

**Plan for ongoing change.** SNOMED CT releases twice yearly. FHIR standards evolve. Implementation guides update. Regulatory requirements change. Migration is not finished at go-live. Mature organisations have formal governance processes for each terminology update cycle, applied throughout the operational life of the system.
