# Central Regional Health Board - Reference terminology at scale

**Organisation.** A large regional health authority covering multiple provider organisations, multiple EHR vendors, and a diverse clinical workforce. Workflow stability was the primary requirement - the authority could not afford to disrupt clinical operations across dozens of sites simultaneously.

  **Approach.** Reference terminology throughout. A regional terminology server was established, hosting SNOMED CT alongside ICD-10, LOINC, and local code systems. Interface binding tables were built for each EHR product in the authority, covering the primary clinical workflows. Historical data was batch-mapped to SNOMED CT.

  **System and data migration.** Data migration with system unchanged across all sites. Clinicians saw no change to their interfaces or workflows on go-live.

  **Outcomes.** Standards-based exchange enabled with partner organisations in the region. SNOMED CT-coded data available for population health analytics for the first time. Regulatory conformance achieved ahead of deadline. Zero go-live incidents attributable to the migration.

  **Lessons.** Deploying reference terminology uniformly across a mixed-EHR environment requires strong governance of the binding tables - particularly ensuring that the same clinical concept is bound to the same SNOMED CT concept across different EHR products. Inconsistency in binding is the most common source of cross-system analytics errors in large reference-terminology deployments.
