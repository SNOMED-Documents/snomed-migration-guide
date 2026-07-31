# The Architectural Context

SNOMED CT is a clinical terminology. It defines the meaning of clinical information. The information standards, messaging protocols, and infrastructure surrounding it can take several forms — and the same SNOMED CT codes work inside all of them.

Understanding the architectural context matters for migration planning because it determines which standards a migration plan must address. Most real organisations run more than one architecture simultaneously.

## FHIR

HL7 FHIR (Fast Healthcare Interoperability Resources) is the most prominent modern interoperability standard. Most national digital-health programmes have published FHIR implementation guides as their recommended or mandated exchange format. Examples include US Core in the United States, NHS England's FHIR profiles in the UK, the Australian Digital Health Agency's implementation guides, and Canada Health Infoway's specifications.

Open-source FHIR servers (HAPI, Firely) and managed cloud services (Azure API for FHIR, AWS HealthLake, Google Cloud Healthcare) make the FHIR stack relatively inexpensive and straightforward to deploy.

FHIR is the interoperability layer — it defines what clinical data looks like when it moves between systems. It is not necessarily what the data looks like when stored inside a given system, and it is not the only modern way to implement SNOMED CT.

## openEHR

openEHR is an open specification for electronic health record information models based on Archetypes and Templates. Archetypes are formal, structured models of clinical concepts — a blood pressure measurement Archetype, for example, has separate structured fields for systolic pressure, diastolic pressure, cuff size, and patient position, all defined to a shared international specification. Archetypes combine into Templates for specific clinical use cases. SNOMED CT is bound in as the terminology layer.

openEHR has national deployments in Slovenia and Norway, adoption in parts of the UK NHS, parts of Spain, parts of Australia, and growing use across parts of Asia. A common mature pattern pairs openEHR for clinical persistence and modelling with FHIR for interoperability and exchange — both bound to the same SNOMED CT edition through the same terminology infrastructure. openEHR and FHIR are complementary, not competing.

## HL7 V2

HL7 V2 has been deployed in clinical systems since the late 1980s and still carries the majority of hospital interface messages worldwide. Integration engines routing V2 messages have decades of operational maturity. For most established organisations doing a SNOMED CT migration, V2 interfaces will coexist with newer FHIR infrastructure rather than being replaced by it.

V2 carries SNOMED CT natively in its CWE (Coded with Exceptions) and CE (Coded Element) data types. A SNOMED CT code in a V2 message looks like: `233604007^Pneumonia^SCT` — the concept ID, the display text, and the code-system identifier, separated by carets in a single field. Many integration engines already support terminology lookups at message-creation time, making it feasible to add SNOMED CT to outbound V2 messages without rearchitecting the interface layer.

## Other standards

**HL7 CDA** carries SNOMED CT in clinical documents — discharge summaries, referral letters, consultation notes — and remains widely used for cross-organisational document exchange.

**DICOM** carries SNOMED CT for findings, procedures, anatomic regions, and structured reports in radiology and pathology.

**OMOP CDM** (Observational Medical Outcomes Partnership Common Data Model) uses SNOMED CT in clinical research and pharmacovigilance data.

**ISO 13606** is an ISO standard for EHR communication that is conceptually similar to openEHR and used in some national programmes.

Real organisations typically run combinations of these alongside FHIR and V2. SNOMED CT is the shared terminology layer that gives coherent clinical meaning across all of them.

For guidance on terminology servers and on running SNOMED CT without one, see [Terminology Infrastructure](2.1-terminology-infrastructure.md).
