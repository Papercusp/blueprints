## Working as a fleet MEMBER — the member operating loop

When you work under a fleet leader (launched via `fleet:launch-on-plan`, joined with
`--fleet`, or handed a lane by a leader), this contract is yours NATIVELY — a leader's
kickoff adds mission specifics, never this:

- **Wake bootstrap:** `coord:orient { intent, planSlug, planItems }` — one call declares
  you, claims your lane, and folds inbox + recall. Plan-bound and idle with no kickoff?
  Don't wait — read the plan's `## Now` and begin.
- **PULL work via `scheduler:get_next` — the leader feeds by claim-SPEC, never by hand.**
  An empty result is SIGNAL, not a fault: the lane is drained, DAG-blocked, or scoped
  away from you. Don't spin on it, and don't cherry-pick the raw backlog around it —
  but eligible work beside an available member requires action or a verified, accountable
  blocker. Diagnose effective claim limits and counted ids, typed blockers, member-specific
  permissions, runtime failures and wake delivery as well as the spec; report the evidence
  to the leader. Parking alone is not a justification, and a fleet-wide count is not proof
  that your own admission rules permit a claim. Preserve owner-only/held-item-only fences.
  When the claim returns `freshness.lane:'validation'`, run the cheapest current-HEAD
  reproduction or focused test BEFORE implementation. The score is a routing hint, never
  closure evidence: an already-fixed result still closes only with the verification you ran.
- **Claim via a `wip`-flip or the work-items pull — never hand-edit plan files** beyond
  status flips. An ad-hoc unit gets its work-item ATOMICALLY: `work_items:create { kind,
  title, assign_to: self }` (creates AND claims in one write — no create→claim race).
  Pick `kind` by what the unit IS: `change` for a code edit (the default for coding
  work), `bug` for broken code, `task` ONLY for non-code work.
- **Persist with `loop:arm`; each wake pull + advance one unit. Lane drained? Register
  the standing wake watch
  `watch:create { pattern:'work-item:claimable', wake:true, once:false,
  payload_filter:<your claim spec's view> }`, then re-run `scheduler:get_next` BEFORE
  `loop:end`** — registering observes future transitions, so the second pull closes the
  gap for work that existed before registration or arrived during it. If it claims work,
  continue; only a verified miss permits sleep, with the standing watch retained. Do not pass
  `targetKind` with `wake:true`; this watch never expires and re-invokes you on
  every matching claimable transition, so it survives the wake that consumes a
  one-shot await. The wake is a HINT; `get_next` on the wake turn stays the
  authoritative claim, and a re-miss does not require re-registering. Don't burn
  empty wakes. If AUTO (or another autonomy-implying mode) remains active without
  that deliberate await, pass
  `acknowledgeOpenDirectives:true, acknowledgeWakeLessAutonomy:true` to `loop:end`.
  Blocked? **PUSH beats polling:** if the
  blocker has a completion event — or its owner can DECLARE one (declare-first
  pair-emit: they `events:emit { announce:true }`, you await the RETURNED key; never
  re-type a key from chat — drift strands you) — `events:await { event }` and END YOUR
  TURN; the wake carries the payload. Only when no event exists for the condition,
  re-arm at a longer interval sized to the blocker and RESTORE the cadence the instant
  it clears.
- **Report exceptions to the LEADER via `coord:send`.** A successful
  `work_items:complete` already routes its structured completion to the current fleet
  leader — do NOT send a second completion FYI. Send blockers WITH diagnosis, cross-lane
  rulings, and anything fleet-wide (a shared-tree fault you hit — broken deps, a wedged
  service — is the leader's to fix fleet-wide: say so, don't route around it silently).
