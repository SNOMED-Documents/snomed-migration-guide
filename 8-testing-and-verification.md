# Testing and Verification

## Testing framework

Testing for a SNOMED CT migration operates at three tiers, each catching a distinct category of problem.

**Tier 1 — Automated technical testing.** FHIR resource structure validity (using the HL7 FHIR validator), data completeness (record counts before and after conversion), referential integrity, and system performance under realistic load. This tier can and should run continuously throughout the migration and should gate each deployment to production.

**Tier 2 — Standards conformance testing.** Conformance of FHIR resources against the relevant national implementation guides (US Core, NHS England profiles, etc.). SNOMED CT semantic validity — correct hierarchy membership, valid active concept identifiers, appropriate use of post-coordination. Cross-map validation. This tier requires tooling specific to the standards in scope.

**Tier 3 — Clinical validation.** Medical appropriateness of converted records: do the SNOMED CT concepts in the converted data correctly represent the clinical intent of the source records? Context preservation: is a past condition correctly distinguished from a current condition? Decision support: do drug-allergy alerts, drug-interaction checks, and clinical recommendation rules produce the correct outcomes on converted data? This tier requires qualified clinical reviewers. It cannot be automated.

Safety-critical data types — allergies, known drug sensitivities, high-risk medication alerts — require parallel running alongside clinical validation: both the old and new systems operating simultaneously, with outputs compared. Any discrepancy must be investigated and resolved before the legacy system is decommissioned.

## Verification against migration objectives

Verification closes the loop between the original business case and the delivered outcome. The most straightforward approach is to:
1. At the start of the project, select three or four of the eight strategic objectives from [Why Migrate to SNOMED CT](1-why-migrate-to-snomed-ct.md) that the migration is explicitly intended to deliver.
2. Define baseline measurements for each (current state, before the migration).
3. Define target values for each (what the migration is expected to achieve).
4. Measure at go-live, at three months post-go-live, and at twelve months post-go-live.

Examples of measurable verification targets:

- Drug-allergy alert accuracy: percentage of true-positive alerts vs. false positives/negatives compared to the pre-migration baseline.
- FHIR conformance rate: percentage of exported resources passing validation against the relevant implementation guide.
- Data exchange success rate: percentage of exchanges with partner organisations completing without semantic mismatch errors.
- SNOMED CT coverage on the problem list: percentage of entries carrying a SNOMED CT concept vs. free-text only or local code only.
- Semantic search coverage: percentage of clinical search queries returning SNOMED CT-coded results.
