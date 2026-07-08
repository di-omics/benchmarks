# di-omics · autonomous-lab benchmark scoreboard

**Two bars, both high.**

An autonomous lab, trained by a domain expert to hit senior-scientist bars: a preset statistical framework, physical-AI QC baked in, and closed-loop feedback control with agentic feedback. The bar to clear is the physical biology and chemistry and the bioinformatics, both proven. Not a green software log. Proof, or it does not count.

**Live board: https://di-omics.github.io/benchmarks/**

## The two bars

**Bar 1, Science: the result is real.** The physical biology and chemistry executed correctly, and the bioinformatics recovers ground truth, scored on a statistical framework fixed before the run. Rules out passing in silico while the wet step silently failed.

**Bar 2, Autonomy: the machine did it, unattended.** Physical-AI QC baked in, error handling that fails closed, and closed-loop feedback where the agent reads QC, corrects, and re-runs. Rules out a demo that only works with a human quietly saving it.

## The infra that proves it

| Pillar | What it is | State |
|---|---|---|
| Liquid-handling QC | Rhodamine B for per-well CV%, Qubit / PicoGreen for yield. Upfront, fail-closed. | Verified |
| Computer-vision QC | Physical AI reads wells, pipetting, and steps from bench video. Ground-truth-validated. | Verified |
| Error handling | Guards, do-not-over-dry limits, one approval before purchase. Fails closed on readiness. | Verified |
| Robust bioinformatics | Reproducible fastq-to-result pipelines: scanpy, BJ-WGS Nextflow, versioned. | Verified |
| Preset statistics | Metric and acceptance threshold fixed before the run. Plant ground truth, recover, score. | Verified |
| Closed-loop agentic feedback | Agent reads QC and CV, corrects the deck, and re-runs without a human in the path. | Building |

## How we do not get fooled

- **Threshold before the run.** The metric and the pass line are fixed up front, never chosen after the numbers land.
- **Physical execution is measured, not trusted.** Rhodamine B, Qubit, and computer vision confirm the wet step actually happened correctly.
- **In silico alone does not clear the science bar.** A recovery score on synthetic data is a start, not a pass. The chemistry has to be shown.

## Per-capability status

| Capability | Science bar (physical + bioinformatics) | Autonomy bar (QC + closed loop) | Graded by (preset) | Expert in loop |
|---|---|---|---|---|
| [fullstack-omics](https://github.com/di-omics/fullstack-omics) | UMI counts, low-input recovery, coverage; wet chemistry to run on deck. Building | End to end in the PyLabRobot simulator; scWGS 10/10 tests. Verified | scanpy, BJ-WGS concordance | operator at deck |
| [plr-mcp](https://github.com/di-omics/plr-mcp) | Actions execute on liquid handler, reader, cycler, shaker. Verified | MCP tool-call round-trip; CI green on 3.10-3.13. Verified | simulator + hardware handshake | agent proposes, operator confirms |
| [omics-demos](https://github.com/di-omics/omics-demos) | Recovery vs. planted ground truth across nine assays. Verified | Blind run, per-assay recovery score. Verified | recovery score, threshold preset | none, automated eval |
| [plr-minimum-effective](https://github.com/di-omics/plr-minimum-effective) | Yield held at reduced reagent; wet confirmation pending. Building | Bayesian optimization, held-out recovery. Verified | cross-validated recovery | expert sets acceptance floor |
| [plr-clarity](https://github.com/di-omics/plr-clarity) | Rhodamine-B validation ladder on a real deck; biovalidated tier. Building | Plan text compiled into a runnable method. Verified | validation tier reached | expert signs each tier |
| [lab-cv](https://github.com/di-omics/lab-cv) | Wells filled vs. empty, pipetting correct. Verified | ROI motion QC + detection on protocol video, CPU-only. Verified | ground-truth-validated frames | reviewer adjudicates |

Verified is runnable and checkable now. Building means the infra is in place and the wet number is next to land. This board is the daily target: turn one cell Verified with a real run at a time. Numbers are never invented. A Building cell names the metric and waits for a measured value.

Source: [github.com/di-omics](https://github.com/di-omics)
