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

## 3. Anomaly Detection Analysis
* **Anomalies Detected:** The detector successfully flagged the observations at `10:05:00` and `10:06:00` as anomalies. 
* **Relevant Metric/Log Information:**
  * At `10:05:00`, it flagged "High response time" (610ms).
  * At `10:06:00`, it flagged "High response time" (640ms), "High CPU utilization" (94%), and "High memory utilization" (91%).
* **Missed Anomalies:** Yes, expected anomalies were missed. Both anomalous records contain an `"ERROR"` log level, but the detector failed to flag them because the code contains a bug that incorrectly checks for a `"WARNING"` log level instead. 
* **Incorrectly Flagged Normal Events:** No normal events were incorrectly flagged.
* **Limitation and Improvement:** 
  * **Limitation:** The current detection logic relies on static, hardcoded thresholds (e.g., CPU > 80%, response time > 500ms). In a real-world scenario, traffic fluctuates naturally, and rigid thresholds lead to alert fatigue from false positives.
  * **Improvement:** Implement dynamic baselining using statistical methods (such as rolling averages or z-scores) or machine learning anomaly detection models (such as an Isolation Forest) to adaptively learn normal system behavior over time.