# BA documentation standards

## Requirements
- Preserve requirement identifiers from the source.
- If no identifier exists, create provisional IDs (FR-001, BR-001, NFR-001, DATA-001) and label them generated.
- Each functional requirement should state description, rationale if present, actor/trigger, preconditions, inputs, processing, outputs, validations, exceptions and acceptance criteria where supported.
- Do not invent business rules, data attributes, field types, interfaces, SLAs or acceptance criteria.

## Traceability
- Map each FSD requirement to a source BRD page, heading, table or diagram only when the source location is identifiable.
- Mark missing traceability as “Source reference not identifiable”.
- Include unaddressed and ambiguous requirements in the open-questions section.

## Data and integration
- Record source/target systems, entities, attributes, data types, mappings, transformations, frequency and ownership only when stated.
- Distinguish confirmed mappings from proposed mappings.

## Quality
- Check completeness, internal consistency, duplicate IDs, unresolved conflicts, missing assumptions and unsupported statements.
- Do not treat the generated draft as approved.
- Human BA approval is mandatory before final publication.
