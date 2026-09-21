# AIOps Assessment - Basic AIOps Monitoring & Event Processing

## 1. AIOps Scenario
* **The service being monitored:** A backend `payment-service` that generates operational telemetry, specifically CPU usage, memory usage, response times, and log levels.
* **The operational problem being addressed:** Manually sifting through continuous metrics and logs to identify unusual behavior or system degradation is inefficient. The operations team needs an automated way to identify abnormal resource consumption and error states.
* **The purpose of AIOps in this assessment:** To simulate an automated pipeline that ingests operational data, evaluates it against baseline thresholds to detect anomalies, and streams these findings as actionable events through a simulated producer-consumer architecture for the operations team.

## 2. Operational Data Observations
* **Metrics:** The fields `response_time_ms` (response time in milliseconds), `cpu_percent` (CPU utilization percentage), and `memory_percent` (memory utilization percentage) represent quantitative metric data.
* **Logs:** The fields `log_level` (e.g., INFO, ERROR) and `message` (e.g., "Payment request processed successfully") represent qualitative log information.
* **Timestamps:** The `timestamp` field uses an ISO 8601 format (e.g., `2026-09-20T10:00:00`) and is recorded at exactly one-minute intervals to track the chronological state and performance trend of the service.
* **Normal Behaviour:** Under normal conditions, the service processes requests successfully with a response time between 120ms and 150ms, CPU utilization between 42% and 50%, and memory utilization between 51% and 57%. Logs during this time report an "INFO" level.
* **Unusual Behaviour:** Unusual behavior occurs at `10:05:00` and `10:06:00`. Response times spike over 600ms, and CPU/memory utilization surge (reaching up to 94% CPU and 91% memory). During these spikes, the log level changes to "ERROR" with messages indicating a "Payment service timeout" and a "Database connection timeout".