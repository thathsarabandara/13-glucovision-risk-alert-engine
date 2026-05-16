<div align="center">

# 🚨 GlucoVision Risk Alert Engine

**The real-time clinical safety layer that fires hypoglycemia and hyperglycemia alerts.**  
*Kafka event streaming · Predictive alerting · Redis deduplication · WebSocket push*

[![FastAPI](https://img.shields.io/badge/FastAPI-Python-009688?style=for-the-badge&logo=fastapi)](#)
[![Kafka](https://img.shields.io/badge/Kafka-Streaming-231F20?style=for-the-badge&logo=apachekafka)](#)
[![Redis](https://img.shields.io/badge/Redis-Dedup-DC382D?style=for-the-badge&logo=redis)](#)
[![WebSocket](https://img.shields.io/badge/WebSocket-Real--Time-010101?style=for-the-badge)](#)
[![Docker](https://img.shields.io/badge/Docker-Containerised-2496ED?style=for-the-badge&logo=docker)](#)
[![Status](https://img.shields.io/badge/Status-In%20Development-f59e0b?style=for-the-badge)](#)

</div>

---

## 📌 Purpose

GlucoVision Risk Alert Engine fires **real-time glucose alerts before dangerous events materialise**. Sub-second latency, zero downtime, and independent uptime SLA — because a delayed alert can cause a patient to miss hypoglycemia treatment (a medical emergency). Must never share a deployment unit with `12` glucose prediction.

> **99.99% uptime SLA** — alerts must fire even during other service deployments.

---

## 📁 Project Structure

```
13-glucovision-risk-alert-engine/
└── (Git repository initialised — structure to be scaffolded)
```

---

## ✨ Planned Features (by phase)

### Phase 1 — Threshold Monitoring
- [ ] Hypoglycemia detection (< 3.9 mmol/L)
- [ ] Hyperglycemia detection (> 10 mmol/L persistent)
- [ ] Per-patient threshold configuration (clinician-set)
- [ ] Alert history API

### Phase 2 — Predictive Alerting
- [ ] Use `12` forecast to alert before threshold crossed
- [ ] Rate-of-change alerting (rapid glucose drop)
- [ ] Alert severity levels: Low / Medium / High / Critical
- [ ] Redis deduplication (5-min window)

### Phase 3 — Delivery & Integration
- [ ] Kafka alert publishing → `08` notification-service
- [ ] WebSocket real-time alert push to mobile
- [ ] Post-meal spike validation loop
- [ ] Alert feed to `15` recommendation-engine

---

## 🚀 Getting Started

### Prerequisites

- Python ≥ 3.11, Kafka, Redis, MySQL, Docker & Docker Compose

### Setup (once scaffolded)

```bash
pip install -r requirements.txt
uvicorn main:app --reload --port 8008

docker compose up --build
```

---

## 🏗️ Planned Tech Stack

| Layer | Technology |
|---|---|
| Framework | FastAPI (Python) |
| Event Streaming | Apache Kafka (confluent-kafka-python) |
| Real-Time State | Redis (deduplication cache) |
| WebSocket | FastAPI WebSocket endpoint |
| Database | MySQL (alert history, thresholds) |
| Containerisation | Docker |

---

## 🔗 Backend Dependencies

| Service | Interaction |
|---|---|
| `12` glucose-prediction | Forecast data for predictive alerts |
| `14` cgm-integration | Real-time CGM glucose stream |
| `08` notification-service | Delivers push alerts to patients |
| `15` recommendation-engine | Alert context for meal plan adjustment |
| `07` user-service | Patient threshold settings |

---

## 🔐 Security Notes

- Only `12` and `14` can push glucose data (internal auth)
- Glucose values encrypted in transit (TLS)
- Every alert logged immutably — cannot be deleted
- Threshold config restricted to clinician role only

---

## 🧪 Testing (Planned)

```bash
pytest tests/threshold/     # Hypo value → Kafka message
pytest tests/predictive/    # Declining forecast → pre-emptive alert
pytest tests/dedup/         # Same event twice → single alert
pytest tests/latency/       # < 500ms end-to-end
```

---

<div align="center">

*Part of the [GlucoVision Platform](../01-glucovision-platform-architecture) — 21-Repo AI Diabetes Management System*

</div>
