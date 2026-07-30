# Common Challenges

## Balancing data value against conversion effort

The most common planning mistake is treating all data as equally valuable and applying the same conversion strategy to everything. This results in wasted effort on rarely-accessed data while delaying conversion of high-value data that clinical teams need.

Conduct a formal data assessment before any conversion work begins. Classify each data type by clinical value and conversion effort. Apply the value-effort matrix from [Planning a Migration](5-planning-a-migration.md). Document the rationale — decisions made without documentation are the ones most easily reversed under budget pressure.

## Legacy data quality

Legacy clinical data contains systematic errors (codes used in ways that deviate from their official definitions), inconsistencies (the same code used differently in different departments), context gaps (important clinical information present only in free-text notes), and version drift (records from different code-system versions mixed in the same dataset).

A data quality assessment run before mapping begins will identify the most significant systematic issues. AI-assisted pattern detection can find clusters of similar records with inconsistent coding. Natural language processing can surface context from free-text fields during conversion. Expert clinical review of conversion samples is essential for validating that the mapped output correctly represents the clinical intent of the source records.

Some legacy data quality issues cannot be fully resolved. Acceptable approaches include flagging low-confidence records with quality indicators, retaining original text for human review, and documenting known limitations in a data quality register.

## Code system diversity and mapping complexity

Legacy systems typically use multiple code systems — ICD-9 and ICD-10 for diagnoses, CPT or procedure codes for interventions, RxNorm or local formulary codes for medications, LOINC or local codes for labs, and local codes for everything not covered by a standard system. Mapping all of these to SNOMED CT involves one-to-many relationships (one legacy code maps to multiple SNOMED CT concepts depending on clinical context), many-to-one relationships, SNOMED CT concepts that do not exist at the required level of granularity, and granularity mismatches in both directions.

Standard maps published by SNOMED International and partner organisations (ICD-10-CM to SNOMED CT, RxNorm to SNOMED CT, LOINC to SNOMED CT) are a starting point. They should always be reviewed against the specific clinical use case — they are general-purpose and may not capture context appropriately for decision support or analytics applications.

For large-volume mapping projects, an AI-assisted mapping tool that learns from expert decisions and presents suggestions for validation — rather than requiring experts to build the map from scratch — significantly reduces the time and cost of producing high-quality maps.

## Change management and user adoption

Clinical teams that do not understand what has changed, do not trust the converted data, or find new workflows slower than what they replaced will work around the system. Adoption failure undermines clinical value even when the technical migration is correct.

Senior clinicians with the deepest investment in existing workflows are often the most resistant to change. Involving them early in decisions about which workflows use primary terminology and which retain reference terminology — and giving them genuine influence over those decisions — reduces resistance and improves the quality of the final implementation.
