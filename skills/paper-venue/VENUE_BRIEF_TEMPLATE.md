# VENUE_BRIEF_TEMPLATE.md

One field per line. Each venue field carries `value | source | accessed | state`,
where state is `author-supplied` / `agent-read-unconfirmed` / `UNKNOWN`.
Never invented; never "verified by agent".

## Header
brief_version: <integer, starts at 1; increments on ANY field change>
mode: value: <`named-venue` | `generic`> | source: <author's explicit choice> | accessed: <YYYY-MM-DD> | state: author-supplied (`shortlist-requested` is pending intake, never a ready brief)
language: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (paper language declared for the venue, e.g. English, Spanish)
secondary_abstract_language: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (optional; only when the venue requires an abstract in a second language)
readership: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (readership the venue itself declares in aims & scope / call for papers)

## Venue identification
venue_name: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
venue_type: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (journal / conference / transaction / workshop)
publisher: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>

## Venue requirements
paper_type_track_subcommittee: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
mandatory_sections_and_order: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
abstract_format_and_length: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
keywords_classification: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (e.g. ACM CCS)
page_or_word_limit: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
template: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (IEEE, ACM, LNCS, Elsevier, …)
citation_and_bibliography_style: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
anonymity: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (double-blind / single-blind / none)
mandatory_disclosures: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (data/code, ethics/IRB, AI/LLM use, conflicts, reproducibility checklist)
figure_table_requirements: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
supplementary_material_rules: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN>
results_presentation_rules: value: <…> | source: <…> | accessed: <YYYY-MM-DD> | state: <author-supplied | agent-read-unconfirmed | UNKNOWN> (required limitations section, claims vs. results form, …)
