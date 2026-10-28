# Opening gap list (reference)

Use when the required venue brief is missing or shortlist selection is pending, the contribution block is missing or stale, no central claim passes the one-claim rule, or a final abstract is requested before its body and required claims are supported. Return this list instead of the blocked introduction or final abstract. A failed noncentral introduction claim may instead be shown as a gap or omitted with the omission recorded as a visible gap while supported introduction prose proceeds.

Venue brief gap: <missing ready brief or pending shortlist; route to `paper-venue`; leave claim rows empty if this is the only gap>.

Body/block gap: <name the missing or stale artifact and the exact material needed to complete it>.

| Opening claim ID | Proposed wording | Claim class | Support status | Resolvable material pointer / gap | Scope the material permits | Author confirmed | Gate result |
|------------------|------------------|-------------|----------------|-----------------------------------|----------------------------|------------------|-------------|
| CL-001 | | | | | | | failed: <reason> |

For each failed claim:

1. Identify the proposed claim (introduction or abstract).
2. State what material is missing.
3. If existing material supports a narrower claim, propose it for author confirmation.

With no supported central claim, emit no paper introduction, no abstract, and no provisional introduction from an idea alone. With an incomplete body or unsupported required abstract claim, emit no final abstract. The blocked output resumes when the author supplies or confirms adequate material.

Source: docs/requirements.md (one-claim rule), docs/use-cases.md (writing cases), docs/principles.md (W-03, W-04).
