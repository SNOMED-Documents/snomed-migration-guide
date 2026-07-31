# Quick Reference

## Terminology glossary

| Term | Meaning |
|---|---|
| Reference terminology | SNOMED CT attached to clinical data behind the scenes; clinicians use familiar interfaces unchanged |
| Primary terminology | SNOMED CT used directly at the point of data entry; clinicians search and select concepts |
| Interface terminology binding | Pre-built map between clinician-facing terms and SNOMED CT concepts, embedded in the clinical system as a configuration table or FHIR ValueSet |
| Batch mapping | Bulk conversion of historical records from legacy codes to SNOMED CT |
| Terminology server | Centralised infrastructure providing SNOMED CT lookup, value-set expansion, code validation, and cross-map translation |
| FHIR | Fast Healthcare Interoperability Resources - the dominant modern interoperability standard for clinical data exchange |
| openEHR | Open specification for clinical health record information models based on Archetypes and Templates |
| HL7 V2 | Older clinical messaging standard, still in widespread use globally for hospital interfaces |
| CWE | HL7 V2 "Coded with Exceptions" data type - carries a SNOMED CT concept ID, display text, and code-system identifier in a single structured field |
| FHIR Provenance | FHIR resource documenting the origin, conversion process, and audit trail for a clinical record |
| Post-coordination | Combining SNOMED CT concepts to express a more specific clinical meaning not available as a single pre-coordinated concept |
| National extension | Country-specific additions to the international SNOMED CT edition, managed by the national release centre |
| Snowstorm | Open-source SNOMED CT terminology server, developed and maintained by SNOMED International |

## Migration pattern summary

| Pattern | System changes | Data changes | Typical context | Timeline | Indicative cost |
|---|---|---|---|---|---|
| Full modernisation | All workflows | Full conversion | Greenfield or rip-and-replace | 2–6 years | Tens of millions |
| Partial system + full data | Targeted workflows | Full conversion | Established hospitals, partial change | 18–36 months | Single-digit millions |
| Minimum viable / behind-the-scenes | None | Full conversion | Regulatory deadline, no disruption | 6–12 months | Low six figures |
| Phased hybrid | Phased by year | Phased by year | Regional programmes, multiple providers | 3–5 years | Tens of millions, spread across budgets |

## Data strategy summary

| Strategy | Best suited to | Upfront effort | Ongoing maintenance |
|---|---|---|---|
| Full FHIR conversion | Essential clinical data; AI/analytics use cases | High | Low once complete |
| API integration (facade) | Important historical data, occasional access | Medium | Medium to high |
| Strategic archiving | Low-clinical-value data, compliance retention | Low | Very low |
| Hybrid | Most real-world migrations | Medium–high | Medium |

---

*This guide draws on the SNOMED International Migrating to SNOMED CT learning module, the SNOMED CT Beyond FHIR companion guidance, the Minimum Viable Migration guidance, and the System and Data Migration companion document. The case studies in the [Case Studies](<10 case-studies/README.md>) section are composite organisations based on observed migration patterns and do not represent individual organisations. For terminology authoring and content management guidance, see SNOMED International's editorial documentation. For EHR procurement guidance, see the EHR Requirements for Procurement Support document.*
