# Planning a Migration

A SNOMED CT migration plan should address five dimensions. Working through each one before technical work begins produces a defensible, realistic scope story and reduces the risk of misaligned expectations.

## Dimension 1: Scope

Scope is not a binary decision. Each data type and time period should be assessed through two lenses: clinical value (how important is this data for ongoing patient care?) and conversion effort (how complex is the mapping, how large is the volume, how clean is the source data?).

A value-effort matrix helps structure this:

<table data-search="false"><thead><tr><th>Effort / Clinical value</th><th>High clinical value</th><th>Low clinical value</th></tr></thead><tbody><tr><td><strong>Low conversion effort</strong></td><td>Convert fully - priority category</td><td>Convert opportunistically or via API integration</td></tr><tr><td><strong>High conversion effort</strong></td><td>Assess carefully - phased or AI-assisted conversion</td><td>Archive or defer</td></tr></tbody></table>

Data essential for ongoing care (active diagnoses, current medications, allergies, surgical history) with clean, structured source data is a strong candidate for full conversion. Data rarely accessed and structurally messy is a candidate for archiving. Most organisations' data falls between these extremes, which is why hybrid approaches are most common.

Key scope questions: How many patient records, across how many source systems? Which code systems are in use (ICD-9, ICD-10, READ codes, CPT, local codes)? Which data types are in scope? What time span does the migration need to cover? Which FHIR implementation guides or target standards apply? Do standard maps exist for the source code systems, and are they appropriate for the intended use?

## Dimension 2: Functional requirements

Functional requirements define what must continue working after migration, what should improve, and what becomes newly possible.

**Preserve:** Clinical decision support alerts. Quality measure calculations. Regulatory reporting. Clinical documentation workflows. Data exchange with existing partners. All of these must work correctly at go-live - regression on any of them is not acceptable.

**Improve:** More precise clinical documentation where primary terminology is introduced. Semantic search across records. Better decision support using SNOMED CT relationships. Standards-based FHIR exchange with partner organisations.

**Enable:** AI-powered clinical intelligence. Ambient documentation. Cross-organisational analytics. Predictive population health models. These capabilities require SNOMED CT-coded data of sufficient quality and coverage to be effective.

## Dimension 3: Risk assessment

Five risk categories apply to most SNOMED CT migrations.

**Patient safety risks.** The highest priority. Allergies not triggering alerts post-migration. Drug interaction checks failing. Decision support producing incorrect results. Mitigation: comprehensive three-tier testing (see [Testing and Verification](8-testing-and-verification.md)), parallel running during go-live, and a lower-acuity pilot department before clinical areas with highest patient risk.

**Interoperability risks.** FHIR conformance failures, broken exchange with partner organisations, semantic mismatches in exchanged resources. Mitigation: FHIR validation before go-live, interoperability testing with each partner, staged exchange enablement.

**Data quality risks.** Context loss in conversion, mapping errors, semantic drift in analytics queries. Mitigation: provenance tracking from the start, expert clinical review of converted data samples, comparison testing between source and converted records.

**Operational risks.** User workflow disruption, performance degradation, system downtime. Mitigation: phased rollout, clinical training, performance testing under realistic load.

**Compliance risks.** Regulatory reporting failures, audit trail gaps. Mitigation: original data retention throughout, provenance documentation, validation against regulatory requirements before go-live.

## Dimension 4: Timing and approach

This dimension addresses how quickly and in what sequence the work proceeds. For the related question of what changes - the underlying data, the system clinicians use, or both - see the four patterns in [System and Data Migration](4-system-and-data-migration.md).

Four migration timing patterns suit different organisations.

**API-first bridge.** A FHIR API layer is deployed quickly (typically weeks), providing standards-based access to existing legacy data while full data conversion is planned and executed over months. Suitable for organisations that need rapid interoperability participation before conversion is complete.

**Microservices migration.** The terminology service is migrated first, then one clinical domain at a time. Suitable for organisations with a microservices architecture.

**Big bang with safety net.** All conversion logic is prepared and thoroughly tested, then a single cutover event with parallel running of the old and new systems. Suitable for smaller organisations with bounded, clean migration scope.

**Phased departmental.** One department is piloted, lessons are learned and the approach is refined, then the migration is expanded. The most common pattern for larger organisations. It manages change at a pace clinical teams can absorb and contains risk during the learning period.

## Dimension 5: Skills and resources

**Core team roles every migration requires.** A SNOMED CT terminology specialist (map design, semantic validation, clinical review). A FHIR implementation specialist (resource structure, conformance, API design). Clinical subject matter experts (validate mapping appropriateness, review converted data). A legacy system expert (source data structures, extraction logic, local coding patterns). An integration architect (integration design, data flow, system connectivity).

**Extended team roles depending on scope.** DevOps engineer (automated testing, staged deployment). Data quality analyst (quality assessment, post-migration monitoring). Change management specialist (training, communication, adoption). Cloud architect (cloud deployment and scalability, where applicable). AI/ML specialist (where AI capabilities are a migration objective).

**Key tools.** A FHIR server (EHR Datastore). A terminology server with SNOMED CT. A FHIR validator. A mapping tool. An automated testing framework. A CI/CD pipeline for staged deployment.
