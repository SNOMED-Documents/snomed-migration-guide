# Kimberley Primary Care Group — Minimum viable migration

**Organisation.** A small primary-care network of 12 GP practices sharing an EHR. GPs experienced and running to capacity. A national regulatory requirement mandated SNOMED CT-coded data for reporting within 18 months. Workflow disruption was not acceptable.

**Approach.** Minimum viable migration — data migration with system unchanged. A terminology server was established and mapping tables built for every legacy code used across the network. Every record leaving the system for national reporting was SNOMED CT-coded. Every record exchanged with partner organisations was FHIR-conformant. On go-live morning, the system looked, felt, and behaved exactly as it had the day before.

**Terminology strategy.** Reference terminology throughout.

**System and data migration.** Data migration only. No system changes.

**Outcomes.** Regulatory conformance achieved within the 18-month deadline. National exchange enabled. Zero clinical workflow disruption. A documented SNOMED CT infrastructure in place as the foundation for subsequent phases.

**Lessons.** The minimum viable migration is a legitimate and often appropriate first step, not a concession. For Kimberley, it was the right answer for this phase — and it left the organisation with a working SNOMED CT layer they could build on. The risk to manage is organisational momentum: without a clear plan for what comes next, minimum viable migrations can remain as-is indefinitely, delivering compliance but not the clinical benefits that motivate more ambitious programmes.

**Typical profile.** 6–12 months, low six figures.
