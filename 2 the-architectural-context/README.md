# The Architectural Context

SNOMED CT is a clinical terminology. It defines the meaning of clinical information. The information standards, messaging protocols, and infrastructure surrounding it can take several forms — and the same SNOMED CT codes work inside all of them.

Understanding the architectural context matters for migration planning because it determines which standards a migration plan must address. Most real organisations run more than one architecture simultaneously.

## FHIR

HL7 FHIR (Fast Healthcare Interoperability Resources) is the most prominent modern interoperability standard. Most national digital-health programmes have published FHIR implementation guides as their recommended or mandated exchange format. Examples include US Core in the United States, NHS England's FHIR profiles in the UK, the Australian Digital Health Agency's implementation guides, and Canada Health Infoway's specifications.

Open-source FHIR servers (HAPI, Firely) and managed cloud services (Azure API for FHIR, AWS HealthLake, Google Cloud Healthcare) make the FHIR stack relatively inexpensive and straightforward to deploy.

FHIR is the interoperability layer — it defines what clinical data looks like when it moves between systems. It is not necessarily what the data looks like when stored inside a given system, and it is not the only modern way to implement SNOMED CT.

**How SNOMED CT binds in.** SNOMED CT concepts populate `CodeableConcept.coding` elements throughout FHIR resources (`Condition.code`, `Procedure.code`, `AllergyIntolerance.code`, and others), identified by the system URI `http://snomed.info/sct`. `ValueSet` and `CodeSystem` resources define which concepts are valid in a given context, `ConceptMap` resources express translations to and from legacy code systems, and terminology servers expose the `$expand`, `$validate-code` and `$translate` operations that a FHIR-based migration calls at run time.

**Migration implications.** A migration plan needs to pin a FHIR version (R4 remains the baseline most national implementation guides target) and validate every converted resource against the applicable implementation guide's required SNOMED CT bindings, not just against base FHIR. Legacy-to-SNOMED CT translation is usually expressed as a `ConceptMap`, so that mapping decisions are inspectable and testable rather than buried in ETL code. Because SNOMED CT itself changes twice yearly, resources should reference a specific edition and version (via the module and version parameters in the code system URI) so that a record converted today remains correctly interpretable after later SNOMED CT releases.

**Specification:** [HL7 FHIR](https://www.hl7.org/fhir/) · [Using SNOMED CT with FHIR](https://www.hl7.org/fhir/snomedct.html)

## openEHR

openEHR is an open specification for electronic health record information models based on Archetypes and Templates. Archetypes are formal, structured models of clinical concepts — a blood pressure measurement Archetype, for example, has separate structured fields for systolic pressure, diastolic pressure, cuff size, and patient position, all defined to a shared international specification. Archetypes combine into Templates for specific clinical use cases. SNOMED CT is bound in as the terminology layer.

openEHR has national deployments in Slovenia and Norway, adoption in parts of the UK NHS, parts of Spain, parts of Australia, and growing use across parts of Asia. A common mature pattern pairs openEHR for clinical persistence and modelling with FHIR for interoperability and exchange — both bound to the same SNOMED CT edition through the same terminology infrastructure. openEHR and FHIR are complementary, not competing.

**How SNOMED CT binds in.** Each coded data node in an Archetype (identified by an `at`-code, such as `at0002`) can carry a terminology binding to one or more SNOMED CT concepts, maintained separately from the Archetype's structural definition. Bindings for internationally published Archetypes are curated in the Clinical Knowledge Manager (CKM) and can be revised as SNOMED CT content changes without altering the Archetype itself.

**Migration implications.** A migration onto openEHR involves two largely independent decisions: which Archetypes and Templates to adopt (reusing internationally published ones from CKM where possible, rather than authoring local equivalents), and which SNOMED CT bindings to apply at each coded node. Keeping the binding layer separate — typically managed through a terminology server — means SNOMED CT content updates do not require Template or software changes, but it also means binding governance needs its own review cycle aligned to each biannual SNOMED CT release.

**Specification:** [openEHR specifications](https://specifications.openehr.org/) · [Clinical Knowledge Manager](https://ckm.openehr.org/)

## HL7 V2

HL7 V2 has been deployed in clinical systems since the late 1980s and still carries the majority of hospital interface messages worldwide. Integration engines routing V2 messages have decades of operational maturity. For most established organisations doing a SNOMED CT migration, V2 interfaces will coexist with newer FHIR infrastructure rather than being replaced by it.

V2 carries SNOMED CT natively in its CWE (Coded with Exceptions) and CE (Coded Element) data types. A SNOMED CT code in a V2 message looks like: `233604007^Pneumonia^SCT` — the concept ID, the display text, and the code-system identifier, separated by carets in a single field. Many integration engines already support terminology lookups at message-creation time, making it feasible to add SNOMED CT to outbound V2 messages without rearchitecting the interface layer.

**Migration implications.** Adding SNOMED CT to V2 traffic is usually an integration-engine change rather than a source-system change: the engine calls the terminology server or mapping table when constructing the outbound message and populates the CWE/CE field's SNOMED CT triplet alongside — not instead of — the existing local code, using the data type's alternate-coding components. This lets receiving systems that only understand local codes keep working unchanged during the transition, while systems that can consume SNOMED CT pick it up from the same message. `SCT` is a registered value in V2's external code system table (HL7 Table 0396), which is what makes this coexistence standards-conformant rather than a local convention.

**Specification:** [HL7 V2](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=185)

## Other standards

**HL7 CDA** carries SNOMED CT in clinical documents — discharge summaries, referral letters, consultation notes — and remains widely used for cross-organisational document exchange. In the US C-CDA implementation, templates such as the Problem Observation require a SNOMED CT code as the primary coding, with an ICD-10 translation held alongside for billing — so a migration producing C-CDA documents needs the same legacy-to-SNOMED CT mapping used elsewhere in the migration, applied consistently at the document layer. Specification: [HL7 CDA](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=7).

**DICOM** carries SNOMED CT for findings, procedures, anatomic regions, and structured reports in radiology and pathology, identified by the Coding Scheme Designator `SCT` in DICOM Structured Report (SR) content items. This matters for migrations that touch imaging or pathology systems: bringing radiology reports into a SNOMED CT-coded clinical record means mapping the DICOM SR coded entries into the same SNOMED CT edition used elsewhere, rather than treating imaging as a separate coding silo. Specification: [DICOM Standard](https://www.dicomstandard.org/).

**OMOP CDM** (Observational Medical Outcomes Partnership Common Data Model) uses SNOMED CT as its standard vocabulary for the Condition domain, and analytics-oriented migrations map source codes into OMOP standard concepts using OHDSI tooling — Usagi for candidate mapping, Athena for browsing the standardised vocabularies. Because the OMOP mapping and a clinical-system SNOMED CT mapping are produced independently, a migration that feeds both an operational EHR and a research/analytics platform should reconcile the two mappings rather than assume they agree. Specification: [OMOP Common Data Model](https://ohdsi.github.io/CommonDataModel/) · [Athena vocabulary browser](https://athena.ohdsi.org/).

**ISO 13606** is an ISO standard for EHR communication that is conceptually similar to openEHR — it uses the same Archetype-based approach and the same style of external terminology binding to SNOMED CT — and is used in some national programmes, often alongside or as a precursor to an openEHR deployment. Specification: [ISO 13606-1:2019](https://www.iso.org/standard/67868.html).

Real organisations typically run combinations of these alongside FHIR and V2. SNOMED CT is the shared terminology layer that gives coherent clinical meaning across all of them — the concept for *myocardial infarction* is the same concept whether it arrives in a FHIR `Condition`, an openEHR-persisted Archetype, a V2 message, or a DICOM structured report, which is precisely what allows a migration to treat these as one clinical record rather than as separate, unreconciled systems.

For guidance on terminology servers and on running SNOMED CT without one, see [Terminology Infrastructure](2.1-terminology-infrastructure.md).
