# ANIRBAN-1: IoT Mesh for Autonomous Aircraft Safety

**Integrated Technical Concept Report — Cooperative Trajectory Sharing, Conflict Prediction, and Advisory-Layer Engineering**

[![Status](https://img.shields.io/badge/status-research%20concept-orange)](#status--disclaimer)
[![Revision](https://img.shields.io/badge/revision-1.0-blue)](#)
[![Use](https://img.shields.io/badge/use-not%20for%20operational%20use-red)](#status--disclaimer)

---

## Status & Disclaimer

> **Research Concept — Not for Operational Use.**
>
> This repository contains a **research architecture and concept report**. It is **not** an installation manual, a certified design, an operational flight procedure, or evidence of compliance with any standard named in it.
>
> **Naming a standard does not establish compliance.** Any real-aircraft modification must be designed and approved by qualified aviation specialists and the responsible authority.
>
> ANIRBAN-1 is a **simulation-first, advisory-only** concept. It does **not** command flight controls, and it does **not** replace, disable, or contradict existing TCAS/ACAS, ADS-B, ATC, or established operating procedures. No claim is made that the proposed system is safer, more accurate, more reliable, or more effective than existing aviation systems.

---

## Overview

ANIRBAN-1 proposes a cooperative, **advisory-only** aircraft safety overlay. Participating aircraft would:

1. Exchange state and **planned-trajectory intent**
2. Predict potential conflicts over a declared horizon
3. Evaluate candidate resolutions against explicit constraints
4. Present an **explainable recommendation** to a pilot or operator

Existing collision-avoidance and air-traffic functions remain **independent and unmodified** throughout.

### The Research Question

> Can a carefully engineered, fault-aware cooperative trajectory-sharing and conflict-prediction layer demonstrate measurable benefits beyond existing aviation surveillance, collision avoidance, and trajectory-management approaches — where "benefits" are defined by pre-declared metrics, measured against named baselines, and attributed by ablation?

**Honest current answer:** the question is *testable* and the testbed is *inexpensive* — but the benefit remains **undemonstrated**. No public evidence establishes that such a layer already exceeds the ACAS X / DAIDALUS / trajectory-based-operations class of systems.

The defensible research frontier is narrower than a typical concept pitch assumes: **not smarter avoidance logic, and not a new network, but whether aircraft can share intent and coordinate under fault, uncertainty and disagreement without ever making their existing safety depend on that cooperation.**

---

## What This Report Is Not

- ❌ Not a replacement for TCAS/ACAS, ADS-B, radar, ATC, or the flight management system
- ❌ Not an autopilot or flight-control integration
- ❌ Not a claim of certification compliance
- ❌ Not a claim that LiDAR/cameras detect all non-cooperative traffic
- ❌ Not dependent on 6G, cloud connectivity, or blockchain for local conflict detection
- ❌ Not evidence that all aircraft carry ANIRBAN equipment

Six common misconceptions are corrected explicitly in Section 2 of the report:

| Misconception | Correction |
|---|---|
| "TCAS is a last-second panic button" | ACAS II / TCAS II operates independently of ground ATC and issues Traffic and vertical Resolution Advisories. It is a complement ANIRBAN-1 must **never contradict**. |
| "Ground radar is obsolete" | ADS-B complements surveillance, but visibility depends on equipage, coverage and reception, and carries no native authentication. |
| "6G is an available aviation safety network" | IMT-2030 requirements were drafted in Feb 2026 with commercial framing around 2030. Future research, not a prototype dependency. |
| "Consensus/ledgers can establish sensor truth" | Authentication proves message **origin and integrity only**. Blockchain consensus is removed from the time-critical loop. |
| "LiDAR, cameras and radar are universal detectors" | Airborne small-target detection is a bounded research question requiring measured probability-of-detection and false-alarm characteristics. |
| "The mesh itself is the invention" | IEEE 1920.1 already defines infrastructure-free air-to-air ad hoc networking. The contribution sits **above** the transport layer. |

---

## Report Contents

The full report is a single self-contained HTML document (`final report for anirban 1.html`) with 10 hand-authored inline SVG figures and 25 tables.

| § | Section |
|---|---|
| 1 | Document Status and Scope |
| 2 | Executive Summary |
| 3 | Introduction, Motivation, Problem Statement, Research Question |
| 4 | System Scope, Objectives, Assumptions, Non-Goals |
| 5 | System Architecture and Requirements |
| 6 | Surveillance Inputs, Sensors, Non-Cooperative Object Detection |
| 7 | Communications, Message Formats, Coordination, Failure Behaviour |
| 8 | Onboard Software Modules and Processing Workflow |
| 9 | Human Factors and the Advisory Interface |
| 10 | Preliminary Hazard Analysis, Safety, Cybersecurity |
| 11 | Applicable Standards and Potential Certification Pathway |
| 12 | Validation Methodology, Baselines, Metrics, Acceptance Criteria |
| 13 | Development Roadmap and Evidence Gates |
| 14 | Discussion, Research Gap, Proposed Contributions, Limitations |
| 15 | Decisions Made During Revision of the Original Concept |
| 16 | Conclusions and Next Steps |
| 17 | References |
| 18 | Glossary |
| 19 | Contributor Statements |

### Selected Highlights

- **Ten system requirements (SYS-001 to SYS-010)** — two are hard gates: no flight-control output (SYS-007) and fail-closed suppression of advice when inputs are inadequate (SYS-006).
- **Layered architecture L0–L6** — with an independent safety monitor (L5) sitting *between* planning and display, so an unchecked candidate cannot reach the pilot via the planner alone.
- **Six declared operating states** — BOOT, PASSIVE_MONITORING, ADVISORY_AVAILABLE, DEGRADED, SUGGESTION_SUPPRESSED, DISABLED — with eleven numbered transitions.
- **Fourteen hazards (HZ-01 to HZ-14)** — six arise from data and sensing quality, a direct consequence of adding no new actuation.
- **Validation stages V0–V6** — each with declared exit *evidence*, not dates.
- **Three baselines** — (A) constant-velocity extrapolation, (B) DAIDALUS-style detect-and-avoid, (C) published 4D trajectory CD&R — plus **mandatory ablation runs** that disable one feature at a time so improvements are attributed rather than asserted.
- **Four candidate contributions (C1–C4)** stated strictly as hypotheses, each paired with the evidence it would require.

---

## Novelty Position (Stated Conservatively)

| Territory | Status |
|---|---|
| Trajectory mathematics | Occupied |
| Conflict screening / detection | Occupied |
| Manoeuvre optimization (incl. learning-based) | Occupied |
| Alerting & guidance logic with formal verification | Occupied (DAIDALUS, ACAS X) |
| Intent sharing to ground services (TBO) | Under active deployment |
| Air-to-air broadcast of current state | Fielded (ADS-B) |
| Air-to-air ad hoc networking services | Standardized in draft (IEEE 1920.1) |
| **Fault-aware peer coordination semantics** | **Open — the candidate contribution** |

---

## Repository Structure

```
.
├── README.md
├── final report for anirban 1.html    # The full integrated report
└── LICENSE
```

The report is a **single self-contained HTML file**: no remote scripts, no CDN dependencies, no external chart libraries. All figures are inline SVG, so they render correctly offline and in PDF export. Open it directly in any modern browser.

---

## Viewing the Report

**Option 1 — Locally:** open the HTML file in any browser.

**Option 2 — GitHub Pages:** enable Pages on this repo (Settings → Pages → Deploy from branch → `main` / root), then visit `https://<username>.github.io/<repo>/final%20report%20for%20anirban%201.html`.

> 💡 **Tip:** consider renaming the file to something URL-friendly like `index.html` or `anirban-1-report.html` before enabling Pages — spaces in filenames get percent-encoded and look ugly in links.

**Printing / PDF:** the stylesheet includes print rules (A4, page numbers, running header) — just use the browser's Print → Save as PDF.

---

## Unverified Figures

The following were present in the original concept material but could **not** be verified, and are recorded as unverified or removed rather than replaced with invented estimates:

- Per-aircraft cost bands and itemized vendor pricing
- Power draw and fuel-burn impact
- Communication uptime targets and mesh latency figures
- Alert lead-time figures
- Certification timelines
- Assigned development assurance levels (DAL A)

Section 15 of the report lists every such decision with its rationale. Sensor range figures that conflict between the concept body and its own comparison table are **both** recorded and flagged for measurement rather than averaged.

---

## Roadmap

Advancement is governed by **evidence gates, not calendar dates**:

| Phase | Scope | Exit Gate |
|---|---|---|
| 0 | Concept baseline | ConOps, system boundary, initial requirements |
| 1 | Simulation MVP | Repeatable scenarios, baseline metrics |
| 2 | Robustness & network | Protocol spec, threat model, failure-state evidence |
| 3 | HIL prototype | Interface/timing reports, independent design review |
| 4 | Research aviation study | Aircraft-specific feasibility, certification-basis dialogue |
| 5 | Authorized trials | Only after approvals; passive/record-only first |
| 6 | Operationalization study | Only if evidence justifies it |

**Immediate next steps:** freeze Version 0.1 requirements and message schema; stand up Baseline A/B harness with the ablation switchboard; run the fault-injection catalogue; document the threat model; draft the human-factors protocol; open decision records Q1–Q7.

---

## Open Decisions

| # | Question |
|---|---|
| Q1 | First target platform: airliner, research aircraft, or unmanned aircraft? |
| Q2 | Which separation / well-clear criterion governs? |
| Q3 | Which traffic and intent standard is exchanged? |
| Q4 | How are uncertainty and unknown data represented? |
| Q5 | What is the safest coordination outcome under disagreement? |
| Q6 | Which sensor target envelope is in scope? |
| Q7 | Which authority and certification basis applies? |

---

## Contributors

| Name | Contribution |
|---|---|
| **Abu Kayes Huda** | Conceived the entire concept and designed the full system. Developed the IoT mesh architecture, node communication, real-time data routing, redundancy/failover, autonomous aircraft safety logic, and system integration. |
| **Jaidul Islam Alvi** | Participated in early discussions and provided feedback on `[Idea and System Architecture]`. Reviewed draft material. |
| **MD Sakib Hasan** | Participated in discussions and provided input on `[System Architecture and Core Concept]`. Reviewed the final report/presentation. |

*Contributor statement placeholders are reproduced verbatim from the source material and remain author-action items.*

---

## Citation

```bibtex
@techreport{huda2026anirban1,
  title       = {ANIRBAN-1: IoT Mesh for Autonomous Aircraft Safety ---
                 Integrated Technical Concept Report},
  author      = {Huda, Abu Kayes and Alvi, Jaidul Islam and Hasan, MD Sakib},
  year        = {2026},
  month       = {October},
  revision    = {1.0},
  type        = {Research Concept Report},
  note        = {Advisory-only, simulation-first research concept.
                 Not for operational use.}
}
```

---

## License

Add a license appropriate to your intent. For a research concept document, **CC BY 4.0** (documentation) or **MIT** (if you later add code) are common choices. Until a license is added, all rights are reserved by default.

**No license granted here implies any airworthiness, certification, or operational approval.**

---

## Verification Note

A public-name check found **no aviation-system usage** of the project designation across academic and government platforms — only unrelated personal-name matches. This is consistent with a private research project and means no external corroboration of project-specific claims is available. All ANIRBAN-1 features and expected benefits remain **proposals** until they are defined and measured in a controlled study.
