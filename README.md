# Papercusp official blueprints

The official [Papercusp](https://papercusp.com) harness blueprints, published to
the Cupboard as `kind=blueprint` listings — one listing per blueprint,
`listing_ref` = the blueprint id (the top-level directory name here).

| Blueprint | Description |
|---|---|
| `audit` | The G2 user-protection gate: a read-only adversarial auditor screens a remote-authored feature and emits an admit/reject verdict; a reject quarantines the feature behind a blocker escalation until a human resolves it. |
| `base` | Abstract base blueprint — common knobs + defaults. Not directly runnable; extended by concrete blueprints. |
| `calibration` | Deterministic learning loop: mature open calibration bets against their domain probes, resolving or voiding past the grace window (the calibration-markets resolution sweep) on a cadence. Pure SQL, no agent. |
| `change-ledger` | Deterministic recorder: git-log the prompt-source roots over a trailing window and offer one behavior-change-ledger row per (commit, file) (the change-ledger repo-edit scan) on a cadence. Pure bookkeeping — git + SQL, no agent, no LLM. |
| `coding` | The Hive/Hive operator — the Queen in charge of the bee fleet. Wakes on its own self-declared schedule (or an event it subscribed to), surveys the work frontier and bee slots, places ranked tasks onto bees (free slot / graceful-evict+fresh / warm-inject), attaches situational briefs, and declares its next wake. Two roles, both carrying the full Queen role (two-plane coordination, steer-don't-dispatch): the `operator` (the canonical full-role judgment layer, the default decider) and the `queen` (the same role with the dial turned toward placement automation). |
| `coding-factory` | RETIRED — NOT ACTIVE (2026-06-24, by owner decision). Preserved-but-dormant: its `director` autoloop last fired 2026-05-01 and nothing currently instantiates it. Do NOT treat this as "the active/default coding harness" and do NOT wire new work to it. (It is the per-feature coding spine: director → scoper → architect → worker → validator → reviewer → documenter → curator, opt-in gates tester / security / crosscheck / ui-qa.) Kept intact for future revival — to revive, re-enable instantiation (generate-from-repo `extends`) and restore the director dispatch. |
| `coding-solo` | Baseline A internal ablation: the coding harness with the multi-agent spine collapsed to a single end-to-end worker — identical model / base tools / infra / budget to the full coding spine, only orchestration OFF. The single-agent generation unit for the impartial benchmark suite (also the per-sample unit Baseline C best-of-N samples). |
| `content-fix` | Fix a git-sync content-guard quarantine: a content-fixer agent fixes ONLY the syntax of the named files so they pass their content detector (an .mdx that won't compile, a curly quote used as code), changes nothing else, leaves the tree clean, and does not push. |
| `cup` | Launch one generic Pot worker (the `cup` role) — a plain implementation agent the Mug places ranked work + a brief onto. Decoupled from the pipeline guards (no chunk, no spine); the brief rides `extras`, the persona is prompts/cup.md. A cup is kind:'harness' (NOT a pot). |
| `deferral-interest` | Deterministic learning loop: backfill realized deferral costs from history and re-fit the learned deferral-pricing model the queue ranker reads (the deferral-interest refit) on a cadence. Pure SQL + math, no agent. |
| `deliberate` | Resolve a decision via the uncertainty ladder: ask the owner, then a diverse vote if unanswered, then a curated escalation if the vote is split. |
| `deploy` | The release-gate deploy launch: the release-manager agent reviews the gathered deploy plan + staged migrations, makes the go/no-go call, runs the deploy, reads health, and decides rollback. Opus-4.8 @ xhigh — the blast radius is the fleet. |
| `dist-blackboard` | Stigmergic distributed coordination: N peer workers self-claim from a shared queue (no Queen) and coordinate ONLY via a shared blackboard (work-item/scratchpad state) — no direct messaging. |
| `dist-broadcast` | Flat-distributed coordination: N peer workers self-claim from a shared queue (no Queen) and broadcast findings to peers. The fully-distributed pole of the central-vs-distributed study. |
| `dist-peer-review` | Flat-distributed coordination with a peer-review gate: N peer workers self-claim from a shared queue (no Queen); each result is reviewed by a nominated peer before submit. |
| `dist-repo-huddle` | Distributed per-repo huddle: N peer workers self-claim (no Queen); same-repo agents form a group that shares repo-understanding + peer-reviews within the repo — coordination scoped to overlap. |
| `doc-steward` | Bring drifted docs back in sync with the code: a doc-steward re-verifies/regenerates each stale doc the freshness sweep flagged (code is truth; preserve historical runbook knowledge), harness_docs:verify to clear the flag, leave the tree clean, and does NOT push. |
| `ensemble-solve` | Ensemble: N agents solve the same task independently (no coordination during), then a judge picks the best solution. The aggregation-after control arm for the coordination-topology study. |
| `external-bench` | The full Papercusp arm of the impartial benchmark suite: the complete coding spine + coordination substrate run autonomously to DONE over one cloned public benchmark task, under an iso-budget cap, graded by the benchmark's OWN external harness. The spine-ON pole of the `coding-solo` causal-isolation pairing (arm 'papercusp'); we neither author nor grade. Spun by the `instantiateBenchHarness` port (./run-loop.ts). |
| `fleet-ekg` | Deterministic learning loop: embed recent agent sessions into behavioral vectors, detect fleet-wide distribution shifts vs the trailing baseline, attribute against the behavior-change ledger, and alarm unattributable MAJOR shifts (the Fleet EKG) on a cadence. Pure SQL, no agent. |
| `gaia-agent` | General-assistant GAIA solver: one agent researches a question with native web_search/fetch/bash/file tools and writes its FINAL ANSWER to answer.txt. The non-coding single-agent bench unit placed by the su-independent pool or the real Queen. |
| `graduation` | Deterministic learning loop: count per-class clean auto-passes over the outcome rails and file an owner ratification report for any class that crosses the graduation threshold (the graduation tracker) on a cadence. Pure SQL, no agent; files an owner report — never auto-widens autoKinds. |
| `gym` | A meta-harness that optimizes another harness's blueprint: a gym-director drives generate-tasks → run-target-variant (sub-harness) → judge → propose → A/B-gate → accept (commit the target blueprint). The target declares its own gym rubric. |
| `hier-lead-worker` | Hierarchical elected-lead team: one lead runs a coordination pass (plan/assign/strategize) over the team backlog, then workers execute under it. The in-team-coordinator pole between flat-distributed and the Queen. |
| `implement` | Auto-implement an eligible captured improvement (kind=bug): reproduce, fix with a regression test, keep it self/inline-sized; lands via the release gate. Flag-gated OFF + seeded inactive. |
| `iq-battery` | Monthly IQ-battery benchmark: when the code SHA changed, run one owner-budget-capped generation (solver/judge bees through the governed chokepoint) beside gen-0 in the beekeeper trend — the "is the system improving" yardstick. |
| `memory-live-recall-canary` | Daily memory recall canary: replay frozen known-item queries against the live memory stack (read-only), record recall@10 vs baseline, and alert on degradation — so live-store silent failures surface within a day, not whenever someone notices recall feels off. |
| `memory-precision` | Weekly memory-precision monitoring: replay the frozen gold set against the production hybrid backend at the push floor and record FP@5 / R@10 / precision — so the injection floor (solved) is monitored, not benchmarked-once. |
| `merge-resolution` | Resolve a git-sync auto-merge conflict: a merge-resolver agent redoes the merge fresh on main, resolves, commits, leaves the tree clean, and does not push. |
| `migration` | A migration/codemod harness: a migration-director drives a discoverer (find all sites matching the pattern), a worktree-isolated transformer (transform ONE site), and a verifier (tests/build green per site + overall) — safe large mechanical change. |
| `negative-space` | Deterministic learning loop: recompute the zero-hit-search demand map and file the capped missing-knowledge candidates (the negative-space miner) on a cadence. Pure-SQL, no agent — the simplest deterministic blueprint. |
| `neologism` | Deterministic learning loop: mine coord traffic + the insights corpus for emergent recurring vocabulary with no corresponding primitive and file the capped abstraction-proposal candidates (the neologism miner) on a cadence. Pure SQL/fs, no agent. |
| `operator.audience-engineer` | IDENTITY (abstract — a layer, never runnable alone): the engineer-mode AUDIENCE for the desktop OPERATOR chat role — an ENGINEER — peer-to-peer, terse, full technical vocabulary. Fills the exclusive `audience` mode axis (P-021 / D-008). |
| `operator.audience-novice` | IDENTITY (abstract — a layer, never runnable alone): the novice-mode AUDIENCE for the desktop OPERATOR chat role — a NOVICE — a domain expert / founder who does not make technical decisions. Fills the exclusive `audience` mode axis (P-021 / D-008). |
| `pair` | Driver/navigator pair: two agents on one task — a driver writes, a navigator continuously reviews + corrects. The tightest real-time peer-correction loop in the topology study. |
| `papercup` | Launch one fleet WATCHER (the `papercup` role) — the read-mostly observer split out of the overloaded operator (D-004). It sweeps fleet liveness, the coord substrate, and harness health, and raises alarms via coord:escalate/send. It never acts (no spawn/cancel/mutate) — the Mug steers, the papercup watches. |
| `papercup.audience-engineer` | IDENTITY (abstract — a layer, never runnable alone): the engineer-mode AUDIENCE for the PAPERCUP fleet-blackboard chat role — an ENGINEER — peer-to-peer, terse, full technical vocabulary. Fills the exclusive `audience` mode axis (P-021 / D-008). |
| `papercup.audience-novice` | IDENTITY (abstract — a layer, never runnable alone): the novice-mode AUDIENCE for the PAPERCUP fleet-blackboard chat role — a NOVICE — a domain expert / founder who does not make technical decisions. Fills the exclusive `audience` mode axis (P-021 / D-008). |
| `papercusp-engineer` | IDENTITY (abstract — a layer, never runnable alone): the software-engineering profession. Fills the exclusive `domain` slot with su.md's engineering discipline, extracted verbatim by P-002; P-023 makes it the coding hive's domain document. |
| `pot-eval` | Monthly Pot-run evaluation: when the code SHA changed, run one owner-budget-capped SCORED generation of the seeded scenario corpus (whole-Pot runs graded on outcome quality / efficiency / speed by the un-gameable gate) — the acceptance yardstick for whether mug-execution / wave-dispatch / autonomy made the Pot better. |
| `prompt-ablation` | Prompt sedimentology: shadow-ablate ONE SU-playbook governance rule and replay the llm-testing `su` suite baseline-vs-ablated, recording the behavioral-delta evidence — on a weekly cadence. Never mutates a live prompt. |
| `red-queen` | Red-queen vaccination: plant a known synthetic friction in the SANDBOX, detect + heal it with a real watchdog, and record MTTSH + the zero-leak assertion — one drill cycle per cadence tick. |
| `regret` | Regret miner: select bad historical sessions, price candidate rule changes via a governed counterfactual replay, and file scored what-would-have-helped reports. |
| `release-fix` | Fix a green-checkpoint gate failure: a release-fixer agent reads the checkpoint log, reproduces the failing test to classify regression-vs-flake, then fixes the code or removes a proven flake (hermetic / tier-out / accountable quarantine), leaves the tree clean, and does not push. |
| `research` | A minimal research harness: a research-director drives a single researcher per research task, with searcher/verifier as reactive helpers. Repo-less. |
| `research-steward` | IDENTITY (abstract — a layer, never runnable alone): research and documentation stewardship for a repo-less task pipeline. |
| `review` | A review/audit harness: a review-director drives one dimension-reviewer per review dimension, an adversarial finding-verifier refutes each finding before it counts, and a findings-synthesizer dedups + ranks the survivors into one report. |
| `scan` | Proactive workspace scan: the scanner sweeps for latent problems + improvement opportunities no agent flagged and captures each as a tracked work-item (kind=change|improvement) into the self-improvement triage backlog. |
| `scout` | Scout autonomous-ideation cadence: idle/friction-gated, budgeted ideation cycles (ideator → critic → route to draft plans / the gym / improvements) on a frequent heartbeat. The op runs the same self-gated tick as the bespoke routine. |
| `single-agent` | Abstract parent for single-role run-to-done launches — the shared single-role spine (one decider role + DONE/ESCALATE/IDLE edges + inline planner) plus the governed + durable launch contract. Not directly runnable; extended by implement / scan / merge-resolution / deploy. |
| `su-collaborator` | IDENTITY (abstract — a layer, never runnable alone): the interactive su's collaborator stance toward the owner. Fills the exclusive `collaboration-stance` slot with su.md's Who-you-are address rule, Default-posture ask gate and Delivery discipline, extracted verbatim by P-002. |
| `su.fleet-leader` | IDENTITY (abstract — a layer, never runnable alone): the fleet LEADER posture — the monitoring / benching / claim-spec / kickoff / spawn-announcement craft of leading a fleet. Fills the exclusive `fleet-posture` slot with su.md's leader tiles, extracted verbatim by P-002 and made an identity by P-020; attached by fleet:take-leadership. |
| `su.fleet-member` | IDENTITY (abstract — a layer, never runnable alone): the fleet MEMBER posture — how an su operates under a fleet leader. Fills the exclusive `fleet-posture` slot with su.md's member operating loop, extracted verbatim by P-002 and made an identity by P-020; attached by fleet:launch-on-plan / fleet:join. |
| `su.mode-audit` | IDENTITY (abstract — a layer, never runnable alone): the AUDIT mode definition — a verdict on a whole program, census → ledger truth → flow → liveness → mechanisms → delivered report. Fills the exclusive `audit` mode axis; read-only enforcement stays kernel (P-021 / D-008). |
| `su.mode-auto` | IDENTITY (abstract — a layer, never runnable alone): the AUTO mode definition — the owner's standing "act, don't ask" grant read in the su's vocabulary. Fills the exclusive `autonomy` mode axis; bound for `auto` and `cold-auto`; attached by mode:set, detached on exit (P-021 / D-008). |
| `su.mode-drain` | IDENTITY (abstract — a layer, never runnable alone): the DRAIN mode definition — drive the agreed backlog to terminal as a fleet leader, completion integrity over burn-down speed. Fills the exclusive `objective` mode axis; DRAIN ⇒ AUTO stays a kernel implication (P-021 / D-008). |
| `su.mode-ideate` | IDENTITY (abstract — a layer, never runnable alone): the IDEATE mode definition — the owner's "invent net-new, don't just patch" switch read in the su's vocabulary. Fills the exclusive `ideation` mode axis; stacks with `autonomy` (P-021 / D-008). |
| `transfer` | Transfer harness: distill transferable lessons from the day's transcripts (admitted probationary), then student-transfer-test them via a governed replay battery to promote/demote/retire — on a nightly cadence. |
| `vote` | Decide between options via a diverse-lens, confidence-weighted vote: one voter per lens + an advocate arguing against the lead; resolve decisively or escalate a curated split to the human. |
| `work` | A generic (non-coding) Hive — the Queen places research / analysis / deliberation work onto a fleet of bees that produce DELIVERABLES (reports, decisions, documents). "Done" is decided by an LLM judge against a rubric; output lands in the artifacts store; the Queen co-locates work by topic, not file. Repo-less. The non-coding counterpart of the coding `hive`. |

## Install

Through the Cupboard UI (the listing's **Fork** action), or directly:

```
POST /api/cupboard/install-blueprint { "listingId": "<cupboard listing id>" }
POST /api/cupboard/install-blueprint { "githubUrl": "https://github.com/Papercusp/blueprints", "listingRef": "<id>" }
```

The install validates the blueprint (schema + semantics + declared
`dependencies.{tools,plugins}` against your host) and places it under
`~/.papercusp/blueprints/<id>/` — the *installed* tier of the
local → installed → built-in `extends` resolution.

## Provenance

Source of truth: the `papercup` monorepo
(`libs/papercusp/packages/harness/blueprints/` plus
`apps/operator/prompts/`, projected under `base/prompts/`). This repo is a generated
mirror — synced by `scripts/publish-official-blueprints.mts sync`; do not edit
here. Prompt projection refuses every destination collision before writing, so
blueprint-local prompt content cannot be silently overwritten. The same
blueprints also ship bundled inside Papercusp as the bootstrap/offline floor; a
Cupboard-installed copy shadows the bundled one.
