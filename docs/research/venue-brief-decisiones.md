# Approved paper-venue decisions

The author approved adding `paper-venue` and amending AGENTS.md rule 6. The
reasoning review reached APPROVE on 2026-10-27. This record summarizes the
decisions that implementation must satisfy.

1. `paper-venue` is the sole intake exception to W- skill traceability. It
   records external venue facts under C- with field provenance. It writes no
   paper prose, gives no communication advice, and adds no rubric criterion.
2. `readership` records only what the venue declares in its aims and scope or
   call for papers; it is `UNKNOWN` otherwise. Vocabulary choices belong to
   the writing skills.
3. The evidence gate in `paper-contributions` runs first. `paper-venue` then
   produces a ready brief before outline, opening, ending, restructuring,
   venue adaptation, or submission checks. A narrow local edit that does not
   touch sections, abstract, closing, or venue rules may record
   `venue_brief: none`.
4. Intake offers three explicit choices: named venue, generic work, or a
   candidate shortlist. `shortlist-requested` is pending until the author
   chooses a named venue or explicitly chooses generic work. A ready brief has
   `mode: named-venue` or `mode: generic`.
5. The author supplies the guide when possible. If standard web access exists
   and the author named a venue, the agent may read the official guide; such
   fields remain `agent-read-unconfirmed` until the author confirms them.
   Unknown rules remain `UNKNOWN`.
6. Every brief field records source, access date, and state. The integer
   `brief_version` changes when a field changes. Downstream skills identify
   changed fields and affected output before rewriting; the author confirms
   affected changes. Language and optional secondary abstract language are
   recorded in the brief, never guessed by downstream skills.
7. The four writing skills remain the treatment arm in evaluation. Intake runs
   before both arms and supplies the same brief. The current MVP has no skill
   for drafting technical body sections or executing the graph principle.

These decisions are implemented in `docs/plan-paper-venue.md` and the skill
contracts. A venue-compliance claim requires `mode: named-venue` and known,
applicable rules; generic work makes no such claim.
