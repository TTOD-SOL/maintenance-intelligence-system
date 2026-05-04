# Maintenance Intelligence & Predictive Repair System

Predictive maintenance platform that fuses equipment sensor behavior, repair history, and technician feedback into a single intelligence layer for high-throughput automated environments.

**Built by a working maintenance technician with daily ground-truth exposure to the failure modes the system is designed to predict.**

---

## The Problem

In a high-volume automated facility, equipment downtime compounds. A failing bearing on one conveyor stalls upstream sortation; a misreading sensor triggers spurious alerts that get ignored, masking the real ones. Most predictive-maintenance systems are built by software engineers who have never put hands on the equipment they're modeling — so the models are accurate in theory but useless in practice.

This project takes the opposite approach: model the *workflow* a technician actually performs, and build the intelligence layer around it.

---

## What It Does

The system is organized as a four-layer stack:

| Layer | Function |
|---|---|
| **Sensor anomaly detection** | Identify abnormal patterns in multivariate sensor signals (vibration, temperature, current) |
| **Fault classification** | Estimate the most likely mechanical issue given the anomaly signature |
| **Repair-time estimation** | Predict expected repair duration from historical maintenance records |
| **Parts recommendation** | Suggest the parts most likely needed given the diagnosis |
| **Feedback learning loop** | Capture technician confirmation/correction after each diagnosis to retrain the classifier |

The result: when an anomaly fires, the technician doesn't just see "alert on Sensor 47." They see *"likely bearing degradation on motor M-12, expected repair 45 minutes, pull part #BR-2241 from stock,"* with confidence scores and the option to confirm or correct after the fact.

---

## Why The Feedback Loop Matters

Most predictive-maintenance systems train once and freeze. Real equipment behavior drifts — environmental conditions change, parts are replaced with different tolerances, new failure modes emerge. The technician feedback layer is what keeps the model aligned with reality:

```
Anomaly → Diagnosis → Technician confirms/corrects → Retrain
```

Each diagnosed failure becomes a labeled training example. Over time, the system gets better at the failure modes specific to *your* facility, not the failure modes of some generic sensor dataset.

---

## Architecture

```
maintenance-intelligence-system/
├── src/
│   ├── data/             # Sensor ingestion + repair history loaders
│   ├── models/           # Anomaly detection, fault classifier, repair estimator
│   ├── intelligence/     # Cross-layer fusion: combines outputs into a diagnosis
│   ├── feedback/         # Technician feedback capture + retraining hooks
│   └── api/              # Diagnosis service interface
├── notebooks/            # Exploratory analysis + model evaluation
├── data/synthetic/       # Synthetic sensor + repair data for portfolio demos
├── reports/              # Evaluation metrics, confusion matrices
└── assets/
```

### Tech Stack

- **Python · Pandas · NumPy** — data manipulation and feature engineering
- **Scikit-learn** — anomaly detection (Isolation Forest, robust statistics) and fault classification
- **Time-series analysis** — windowed feature extraction, rolling statistics, FFT for vibration signals
- **Jupyter** — exploratory analysis and model evaluation

---

## Status

This repository contains the system architecture and core models trained on synthetic sensor data representative of automated material-handling equipment. It is structured as a portfolio-grade reference implementation; production deployment requires wiring to a live sensor ingestion source and a real repair-history database.

The design draws directly from daily operational experience as a maintenance technician at a high-volume FedEx Ground facility — modeling the actual diagnostic workflow, not a textbook abstraction.

---

## Related Work

This project is part of a broader portfolio of industrial intelligence systems:

- [precise-anomaly-detection-v01](https://github.com/TTOD-SOL/precise-anomaly-detection-v01) — precision-first anomaly detection for multivariate sensor data
- [downtime-analytics-pipeline-V01](https://github.com/TTOD-SOL/downtime-analytics-pipeline-V01) — ETL pipeline for reliability KPIs (MTBF/MTTR) and failure-mode insights

---

## About

Built by Onoray Davis III. U.S. Air Force veteran (Tactical Aircraft Maintenance), FedEx Ground maintenance technician, and AI/ML engineer focused on systems that turn industrial sensor data into actionable maintenance intelligence.

Contact: trusiv1@gmail.com
