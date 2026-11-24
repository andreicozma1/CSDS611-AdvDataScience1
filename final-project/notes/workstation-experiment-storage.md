# Workstation experiment storage

The approved default is
`/data/acozma/codex-experiments/<project>/YYYY-MM-DD/<study>/`.
Subproject folders are optional. The date identifies when a study began;
continuing work stays in that study directory.

The maintained policy lives in the user-owned AICIP Lab Workstations skill's
`references/storage-and-datasets.md`, with a short deployed guide at
`/data/acozma/AGENTS.md` on each workstation.

## Migration on 2026-11-20

- **com2044:** moved the only existing study from
  `/data/acozma/runs/2026-11-19/csds611-direct-612/` to
  `/data/acozma/codex-experiments/CSDS611-AdvDataScience1/2026-11-19/synthetic-rate-recovery-seed612/`.
- **Status:** the user approved stopping the archived campaign and comparison
  watcher; completed checkpoints and interrupted attempts remain archived.
- **Verification:** 9,657 entries, including 8,751 regular files and 473,424,047
  regular-file bytes, matched before and after an atomic same-filesystem move.
  Hashes, file kinds, symlink targets, hard-link relationships, modes, mtimes,
  and inode identities matched.
- **Evidence:** `migration-2026-11-20/receipt.json`, `stop.json`, and
  `inventory.json.gz` inside the moved bundle; its root `README.md` identifies
  code, inputs, logs, and results.
- **Old parents:** `/data/acozma/runs/2026-11-19/` and `/data/acozma/runs/` were
  removed only after becoming empty; no compatibility aliases were added.
- **com2048:** neither the old `runs/` tree nor any study requiring migration
  existed at inspection.

Historical source and manifests retain their original path strings. Current
navigation and new commands use the canonical location. Relocated environment
activation scripts and executable shebangs can contain old absolute paths;
verify an explicit interpreter before reuse.

## Instruction changes

The skill now covers qualified project/study names, optional hierarchy levels,
study README/manifest discovery, independent detached execution, active-job
migration decisions, preserved evidence, and environment verification.

| Skill document | Before this patch | After this patch | Change |
| --- | ---: | ---: | ---: |
| `SKILL.md` | 3,606 | 3,870 | +264 |
| `references/storage-and-datasets.md` | 5,099 | 7,332 | +2,233 |
| `references/ssh-experiments.md` | 8,650 | 9,044 | +394 |
| `references/workstation-root.AGENTS.md` | 1,214 | 1,767 | +553 |

Concurrent edits to the launch-interview guidance in `SKILL.md` and
`references/ssh-experiments.md` were preserved. These counts describe this
storage patch, not unrelated later edits. The deployed storage guide on both
hosts matches the maintained source at SHA-256
`61fe0187bb555eeb0d3cf7256d01e5aae4b205e2cb865d088afac973c5b3b0da`.

Static verification and manual walkthroughs cover a new study, a continuing
multi-day study, an established project-owned root, and migration of active
work. No agent behavior test was run.

## SciPy comparison

The fresh com2044 RK45/LSODA comparison was launched on 2026-11-20 at
08:23 EST, using default tolerances, one worker, the same five seed-612 rates,
and a 1,800-second cap per call. Its canonical study directory is
`/data/acozma/codex-experiments/CSDS611-AdvDataScience1/2026-11-20/scipy-rk45-lsoda-defaults-halton5/`.
The local uncapped comparison was stopped with four completed calls preserved;
the interrupted third RK45 call has no returned predictions. The remote study
must collect fresh measurements rather than importing those timings.

The user selected detached tmux and a return-after-startup handoff. Session
`csds611-scipy-defaults-halton5` owns the producer. Startup reached the first
real RK45 solve with controller PID 2277071 and worker PID 2277131; a new SSH
connection verified that it continued after the launching connection exited.
At this handoff, no long-call results were yet recorded. The producer writes
incremental tables, `exit-code`, and `COMPLETE`; no attached agent monitor is
retained after the handoff.

See the [study README.md](../benchmarks/2026-11-20/scipy-defaults-five-halton/README.md)
for reconnect and stop commands. `manifest.json`, `check.json`,
`supervision.json`, and `startup-verified.json` are copied beside that local
README for recovery. Predictions, running logs, and later outcomes remain on
com2044 until requested or collected in a later session.
