# System and Data Migration

The second decision that shapes every migration is what the migration is actually changing. Two things can happen in a project described as a "SNOMED CT migration," and projects that conflate them create misaligned expectations and avoidable failure.

**Data migration** changes the underlying records. Legacy code systems are mapped or replaced; SNOMED CT codes appear in the clinical data; FHIR resources, openEHR Archetypes, or equivalent structures appear in the target system. This is primarily technical work.

**System migration** changes the system clinicians use. New user interfaces, new workflows, new capture screens, potentially a whole new EHR. This is primarily change-management work. Clinicians experience it directly.

Every real migration involves some of both. Getting the balance between them named explicitly - rather than leaving it as a shared assumption - is one of the most consequential planning steps.

## The four patterns

The simplest way to understand the landscape is as a two-by-two:

| System / Data        | Data changes                | Data unchanged                                 |
| -------------------- | --------------------------- | ---------------------------------------------- |
| **System changes**   | Full modernisation          | UI refresh only (rare in SNOMED CT migrations) |
| **System unchanged** | Behind-the-scenes migration | Status quo                                     |

Each cell describes a genuinely different project with different costs, timelines, risks, and clinical-team asks. Most real migrations combine elements from more than one cell, particularly in large or phased programmes.

**Full modernisation** - both system and data change. New interfaces driven by SNOMED CT primary terminology, new workflows, new data structures. Highest ambition, highest change-management cost, cleanest end state. This pattern is most accessible to greenfield sites or organisations undertaking a full EHR replacement.

**Behind-the-scenes migration** - data changes, system unchanged. Clinicians see nothing different. SNOMED CT codes are added behind every record via reference terminology binding and batch mapping. The system they use on go-live morning looks and behaves exactly as it did the day before. This is the minimum-viable-migration pattern - see below.

**Partial system migration** - a common middle ground in established organisations. All historical data is converted (full data migration), while system changes are targeted at the workflows where clinical granularity matters most, leaving other workflows unchanged.

**Phased hybrid** - the standard pattern for large regional and national programmes. Data migration first (establishing the SNOMED CT layer with minimal clinical disruption), then progressive system modernisation at a pace that clinical teams can absorb.

## Minimum viable migration

A minimum viable migration delivers regulatory conformance and standards-based data exchange with no clinical workflow disruption, on the shortest timeline and lowest budget possible. This is the behind-the-scenes pattern, executed with discipline.

**What it involves.** A terminology server or equivalent mapping infrastructure is established. Each legacy code used in the organisation is mapped to a SNOMED CT concept via a pre-built mapping table. Every record leaving the system for national exchange or partner connectivity is SNOMED CT-coded and (where required) FHIR-conformant. The existing EHR, its interfaces, and all clinical workflows are unchanged.

**What it delivers.** Regulatory conformance. Standards-based data exchange. A working SNOMED CT layer that can be extended in subsequent phases. No clinical disruption on go-live.

**What it does not deliver.** Clinical granularity beyond what the map provides. Decision support driven by SNOMED CT semantic relationships. Primary-terminology workflows. Data quality that benefits from clinician engagement with SNOMED CT concepts.

## Choosing among the four patterns

Two questions do most of the work in placing a migration on the system-data spectrum.

**What is driving the migration?** A regulatory or interoperability deadline points toward the behind-the-scenes pattern, with system changes optional. A clinical-modernisation ambition - better decision support, semantic search, AI capabilities - requires system-migration elements to deliver those benefits. A greenfield or rip-and-replace opportunity opens the full-modernisation option. A multi-provider programme almost always results in a phased hybrid.

**What is the executive sponsor expecting?** A visible, clinically-transformative change to SNOMED CT requires system-migration elements. Data migration alone will not meet that expectation, however technically successful it is. Standards compliance without disrupting operations is precisely what the behind-the-scenes pattern delivers.

The remaining factors that shape this decision - clinical team readiness, the precise data in scope, and budget and timeline constraints - are covered as part of the five planning dimensions in [Planning a Migration](5-planning-a-migration.md).
