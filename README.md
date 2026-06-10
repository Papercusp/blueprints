# Papercusp official blueprints

The official [Papercusp](https://papercusp.com) harness blueprints, published to
the Cupboard as `kind=blueprint` listings — one listing per blueprint,
`listing_ref` = the blueprint id (the top-level directory name here).

| Blueprint | Description |
|---|---|
| `audit` | The G2 user-protection gate: a read-only adversarial auditor screens a remote-authored feature and emits an admit/reject verdict; a reject quarantines the feature behind a blocker escalation until a human resolves it. |
| `base` | Abstract base blueprint — common knobs + defaults. Not directly runnable; extended by concrete blueprints. |
| `bee` | Launch one generic Hive worker (the `bee` role) — a plain implementation agent the Queen places ranked work + a brief onto. Decoupled from the pipeline guards (no chunk, no spine); the brief rides `extras`, the persona is prompts/bee.md. A bee is kind:'harness' (NOT a hive). |
| `coding` | The default coding harness: a per-feature director drives scoper → architect → worker → validator → reviewer → documenter → curator, with opt-in quality gates (tester / security / crosscheck / ui-qa). |
| `deliberate` | Resolve a decision via the uncertainty ladder: ask the owner, then a diverse vote if unanswered, then a curated escalation if the vote is split. |
| `deploy` | The release-gate deploy launch: the release-manager agent reviews the gathered deploy plan + staged migrations, makes the go/no-go call, runs the deploy, reads health, and decides rollback. Opus-4.8 @ xhigh — the blast radius is the fleet. |
| `gym` | A meta-harness that optimizes another harness's blueprint: a gym-director drives generate-tasks → run-target-variant (sub-harness) → judge → propose → A/B-gate → accept (commit the target blueprint). The target declares its own gym rubric. |
| `hive` | The Hive/Hive operator — the Queen in charge of the bee fleet. Wakes on its own self-declared schedule (or an event it subscribed to), surveys the work frontier and bee slots, places ranked tasks onto bees (free slot / graceful-evict+fresh / warm-inject), attaches situational briefs, and declares its next wake. Two roles, both carrying the full Queen role (two-plane coordination, steer-don't-dispatch): the `operator` (the canonical full-role judgment layer, the default decider) and the `queen` (the same role with the dial turned toward placement automation). |
| `implement` | Auto-implement an eligible captured improvement (kind=bug): reproduce, fix with a regression test, keep it self/inline-sized; lands via the release gate. Flag-gated OFF + seeded inactive. |
| `merge-resolution` | Resolve a git-sync auto-merge conflict: a merge-resolver agent redoes the merge fresh on main, resolves, commits, leaves the tree clean, and does not push. |
| `migration` | A migration/codemod harness: a migration-director drives a discoverer (find all sites matching the pattern), a worktree-isolated transformer (transform ONE site), and a verifier (tests/build green per site + overall) — safe large mechanical change. |
| `release-fix` | Fix a green-checkpoint gate failure: a release-fixer agent reads the checkpoint log, reproduces the failing test to classify regression-vs-flake, then fixes the code or removes a proven flake (hermetic / tier-out / accountable quarantine), leaves the tree clean, and does not push. |
| `research` | A minimal research harness: a research-director drives a single researcher per research-task, with searcher/verifier as reactive helpers. Repo-less. |
| `review` | A review/audit harness: a review-director drives one dimension-reviewer per review dimension, an adversarial finding-verifier refutes each finding before it counts, and a findings-synthesizer dedups + ranks the survivors into one report. |
| `scan` | Proactive workspace scan: the scanner sweeps for latent problems + improvement opportunities no agent flagged and captures each as a tracked work-item (kind=change|improvement) into the self-improvement triage backlog. |
| `sentinel` | Launch one fleet WATCHER (the `sentinel` role) — the read-mostly observer split out of the overloaded operator (D-004). It sweeps fleet liveness, the coord substrate, and harness health, and raises alarms via coord:escalate/send. It never acts (no spawn/cancel/mutate) — the Queen steers, the sentinel watches. |
| `single-agent` | Abstract parent for single-role run-to-done launches — the shared single-role spine (one decider role + DONE/ESCALATE/IDLE edges + inline planner) plus the governed + durable launch contract. Not directly runnable; extended by implement / scan / merge-resolution / deploy. |
| `vote` | Decide between options via a diverse-lens, confidence-weighted vote: one voter per lens + an advocate arguing against the lead; resolve decisively or escalate a curated split to the human. |

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
(`libs/papercusp/packages/harness/blueprints/`). This repo is a generated
mirror — synced by `scripts/publish-official-blueprints.mts sync`; do not edit
here. The same blueprints also ship bundled inside Papercusp as the
bootstrap/offline floor; a Cupboard-installed copy shadows the bundled one.
