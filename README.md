# di-omics &middot; evaluation notes

How each capability in the [di-omics](https://github.com/di-omics) portfolio is evaluated: the metric it is scored on, the QC that gates it, and which numbers are still pending.

**Rendered: https://di-omics.github.io/benchmarks/**

## Two axes

Each repo is checked on two axes.

**Science: does the result hold?** The physical biology and chemistry executed correctly, and the bioinformatics recovers ground truth, against a metric fixed before the run. This is not cleared by an in-silico recovery score alone; the wet step has to be shown to have run correctly.

**Autonomy: does it run unattended?** Physical-AI QC in the loop, error handling that fails closed, and closed-loop feedback where the agent reads QC, corrects, and re-runs.

## The infrastructure behind the checks

| Pillar | What it is | State |
|---|---|---|
| Liquid-handling QC | Rhodamine B for per-well CV%, Qubit / PicoGreen for yield. Upfront, fail-closed. | Verified |
| Computer-vision QC | Reads wells, pipetting, and steps from bench video. Ground-truth-validated. | Verified |
| Error handling | Guards, do-not-over-dry limits, one approval before purchase. Fails closed on readiness. | Verified |
| Robust bioinformatics | Reproducible fastq-to-result pipelines: scanpy, WGS analysis Nextflow, versioned. | Verified |
| Preset statistics | Metric and acceptance threshold fixed before the run. Plant ground truth, recover, score. | Verified |
| Closed-loop agentic feedback | Agent reads QC and CV, corrects the deck, and re-runs without a human in the path. | Building |

## Guardrails against fooling ourselves

- **Threshold before the run.** The metric and the pass line are fixed up front, not chosen after the numbers land.
- **Physical execution is measured, not trusted.** Rhodamine B, Qubit, and computer vision confirm the wet step actually happened correctly.
- **In silico alone does not clear the science axis.** A recovery score on synthetic data is a start, not a pass.

## Per-capability status

| Capability | Science axis (physical + bioinformatics) | Autonomy axis (QC + closed loop) | Graded by (preset) | Expert in loop |
|---|---|---|---|---|
| [fullstack-omics](https://github.com/di-omics/fullstack-omics) | UMI counts, low-input recovery, coverage; wet chemistry to run on deck. Building | End to end in the PyLabRobot simulator; scWGS 10/10 tests. Verified | scanpy, WGS analysis concordance | operator at deck |
| [plr-mcp](https://github.com/di-omics/plr-mcp) | Actions execute on liquid handler, reader, cycler, shaker. Verified | MCP tool-call round-trip; CI green on 3.10-3.13. Verified | simulator + hardware handshake | agent proposes, operator confirms |
| [omics-demos](https://github.com/di-omics/omics-demos) | Recovery vs. planted ground truth across nine assays. Verified | Blind run, per-assay recovery score. Verified | recovery score, threshold preset | none, automated eval |
| [plr-minimum-effective](https://github.com/di-omics/plr-minimum-effective) | Yield held at reduced reagent; wet confirmation pending. Building | Bayesian optimization, held-out recovery. Verified | cross-validated recovery | expert sets acceptance floor |
| [plr-clarity](https://github.com/di-omics/plr-clarity) | Rhodamine-B validation ladder on a real deck; biovalidated tier. Building | Plan text compiled into a runnable method. Verified | validation tier reached | expert signs each tier |
| [lab-cv](https://github.com/di-omics/lab-cv) | Wells filled vs. empty, pipetting correct. Verified | ROI motion QC + detection on protocol video, CPU-only. Verified | ground-truth-validated frames | reviewer adjudicates |

Verified is runnable and checkable now. Building means the infrastructure is in place and the wet number is next to land. Numbers are never invented: a Building cell names the metric and waits for a measured value.

Source: [github.com/di-omics](https://github.com/di-omics)
