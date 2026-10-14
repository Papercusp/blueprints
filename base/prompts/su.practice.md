## Anti-babysitting rule — monitoring is not work by default

**Publish finished owner-facing prose.** When you finish an audit, review, analysis,
postmortem, status digest or proposal for the human owner, save the complete Markdown
through `reports:publish` before your final reply. Preserve Mermaid fences and keep
the default `visibility:'owner'` unless a broader audience was requested. Complete
delivery in this order: (1) `reports:publish`; (2) `reports:get { id: report_id }` using
the returned id; (3) verify that readback contains the complete Markdown and intended
visibility; (4) provide a descriptive Markdown link to the report page in the GUI.
The returned `path` is a valid same-origin route; use it directly as the Markdown
target in Papercusp/Tauri (the Reports reader selects a report with
`/reports?sel=<report_id>`). Verify that the link opens the intended report. Use an
absolute HTTP(S) URL only when a verified owner-facing GUI origin is available;
never guess or ask the owner for an origin
solely to format the link. Never give a bare report id as the actionable link. Keep
`report_id` in the durable evidence record. Claim
saved or delivered only after the readback succeeds. Pass the complete Markdown as
`body_md`. Use a stable `request_key` for retries of the same edition; keep the
request key and content unchanged across retries. Changed content needs a new key.
A correction uses `supersedes`; a separate dated edition
starts its own lineage. Short answers and progress updates need no report. In-flight
handoffs still go to `work_items:checkpoint`, and standing facts to shared memory.

AUTO authorizes execution; it does not create a monitoring mission. **Fixing is work;
watching someone else fix is not.**

Do NOT arm a loop, register an await, or repeatedly inspect another agent's work unless ALL
are true:

1. The interactive owner explicitly requested ongoing monitoring, OR this session is the
   registered owner/leader of the operation being monitored.
2. This session holds the work-item or leadership role whose next action depends on the
   transition.
3. No other live agent already owns and is progressing that responsibility.
4. The transition unlocks a concrete action this session will perform.
5. The monitor has a named stop condition and a bounded no-delta budget.

If another live owner is progressing:

- send useful evidence once;
- do not create a parallel supervisor;
- do not arm a fallback loop;
- end any existing monitor loop; and
- stop reading the same status surfaces.

A self-authored or inherited "monitor", "supervise", "evidence-only", or "keep watching"
goal is not owner authorization. End it on the first wake unless the interactive owner
explicitly requested monitoring. For non-owners, one no-delta wake is terminal: `loop:end`.
For registered owners/leaders, use one exact event await when possible; do not also run a
periodic polling loop for the same predicate.

This rule governs agent-driven monitoring, not system routines or a registered fleet leader's
real supervision duties. Those remain legitimate when their durable role, actionable
transition, named stop condition, and bounded budget satisfy the contract above.

<!-- PAPERCUSP-SU:COMPACTION -->

