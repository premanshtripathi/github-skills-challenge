# AIOps Assessment - Basic AIOps Monitoring & Event Processing

## 1. AIOps Scenario
* **The service being monitored:** A backend `payment-service` that generates operational telemetry, specifically CPU usage, memory usage, response times, and log levels.
* **The operational problem being addressed:** Manually sifting through continuous metrics and logs to identify unusual behavior or system degradation is inefficient. The operations team needs an automated way to identify abnormal resource consumption and error states.
* **The purpose of AIOps in this assessment:** To simulate an automated pipeline that ingests operational data, evaluates it against baseline thresholds to detect anomalies, and streams these findings as actionable events through a simulated producer-consumer architecture for the operations team.