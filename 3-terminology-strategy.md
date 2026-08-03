# Terminology Strategy

The first decision that shapes every SNOMED CT migration is how SNOMED CT will be used in clinical workflows - whether clinicians engage with it directly at the point of data entry, or whether it sits behind the scenes, attached to data after the fact. This is the terminology strategy decision.

## The reference-to-primary spectrum

**SNOMED CT as a reference terminology** means that clinicians continue using the familiar search boxes, pick lists, and templates they currently use. SNOMED CT codes are attached automatically - either at entry time via a pre-built mapping table, or applied in bulk to historical records. The clinician does not see SNOMED CT and their workflow does not change.

**SNOMED CT as a primary terminology** means that clinicians engage with SNOMED CT directly. When recording a clinical observation, a clinician types a term into a search box, sees a ranked list of SNOMED CT concepts, and selects the concept that best matches what they have observed. The stored record contains that specific SNOMED CT concept, with no translation layer in between.

Most organisations sit somewhere between these two ends, and the right position varies by workflow. Different clinical processes within the same organisation often sit at different points on the spectrum - and that position can shift over time as clinical confidence and tooling mature.

## How SNOMED CT operates as a reference terminology

In a migration context, two reference-terminology mechanisms account for most of the practical work.

**Interface terminology binding.** Each clinician-facing term is pre-mapped to a SNOMED CT concept in a binding table embedded in the clinical system. When a clinician picks a familiar term, the corresponding SNOMED CT concept is stored automatically. The binding is authored in advance by a terminology team and expressed as a configuration table or a FHIR ValueSet. No real-time terminology lookup is involved.

**Batch mapping.** Historical records are converted from legacy code systems to SNOMED CT in bulk. The same kind of pre-built mapping applied in interface binding is applied systematically across a body of existing data. The result is that historical records carry SNOMED CT codes without any change to the system clinicians use.

Four further reference-terminology patterns apply in specific contexts:

* **At-exchange translation.** Local codes are converted to SNOMED CT only when data leaves the system - for exchange with partner organisations, national reporting, or FHIR APIs. The system continues to store local codes internally.
* **Decision support.** SNOMED CT's hierarchy defines which patients trigger alerts and order sets. A drug-allergy alert based on SNOMED CT hierarchy fires for all relevant descendants of the allergen concept, not just the codes explicitly listed.
* **Analytics and reporting.** SNOMED CT concepts are used to query and group data from mixed coding systems, enabling consistent population-level analysis.
* **Cross-map hub.** SNOMED CT bridges between two other terminologies - for example, mapping ICD-10 diagnoses to RxNorm drugs via a SNOMED CT intermediary concept.

### What reference terminology delivers - and what it does not

Reference terminology enables SNOMED CT-coded exchange, standards-based interoperability, analytics, and decision support without requiring clinicians to change how they work. The limitation is that coding granularity is constrained by the map: clinicians cannot record a more specific SNOMED CT concept than the map provides, and mapping errors produce silent coding errors in clinical data.

Reference terminology also requires ongoing maintenance. Maps age - SNOMED CT releases every month, legacy code systems evolve independently, and value sets added after the map was authored are not covered. Map governance is as important as map creation.

## How SNOMED CT operates as a primary terminology

When SNOMED CT is used as a primary terminology, the clinical workflow centres on SNOMED CT concept search and selection. Clinicians develop SNOMED CT fluency over time. The stored record carries the exact concept the clinician selected, with no mapping layer.

This delivers higher clinical granularity - the difference between _chest pain_ and _unstable angina_ is recorded, not lost. It enables more precise decision support, richer semantic search, and data that is directly usable by AI tools without pre-processing. The trade-off is that it requires clinical training, change management, and typically a longer path to go-live than reference terminology.

## Choosing the right position for each workflow

The strategic question is not "reference or primary for our whole organisation?" It is "which workflows benefit most from the granularity and precision of primary terminology, and which workflows are better served by the stability and lower change-management cost of reference terminology?" The answer is different for different workflows and will likely evolve over the life of the implementation.

A typical pattern in a mid-sized general hospital: problem lists and allergy capture at primary terminology (where clinical specificity directly affects decision support quality); medications at reference terminology (where clinicians use familiar drug pickers and SNOMED CT codes are added in the background); encounter diagnoses at reference terminology in the coding workflow with downstream mapping to ICD-10 for billing.
