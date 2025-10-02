

# Infra Monitoring with Alert Manager

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/2a7a1d76-92a4-46f9-9645-eeb87b12903a" />


## Author Information

| Created by | Created on | Version | Last Updated On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------- | ---------- | ------- | --------------- | ------------ | ----------- | ----------- | ----------- |
| Sonal      | 17-09-2025 | V 1.0   | 17-09-2025      | Neelesh      |             |             |             |




# Introduction
This document provides a detailed guide on setting up and using Grafana with alerting rules and the Alert Manager for infrastructure monitoring. It covers alerting rules, configuration, and best practices to ensure timely issue detection and resolution.


# Monitoring Tools
- **Prometheus**: Collects and stores metrics.
- **Grafana**: Visualizes metrics and sets up dashboards.
- **Alert Manager**: Manages alerts, routes them to the appropriate channels, and sends notifications.


# Steps to Create Alerting Rules
1. **Identify Key Metrics**: Determine which metrics are crucial for your infrastructure's health (e.g., CPU usage, memory usage, disk space, network latency, etc.).
2. **Define Thresholds**: Set thresholds for these metrics that will trigger alerts. For example, disk space usage above 75%-80% might trigger a warning, while above 80% could trigger a critical alert.
3. **Create Alerting Rules in Prometheus**: Write alerting rules using Prometheus's PromQL. Example:
    ```yaml
    groups:
    - name: CPU-alerts
      rules:
      - alert: HighCPUUsage
        expr: 100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage detected on instance {{ $labels.instance }}"
          description: "CPU usage has exceeded 80% for more than 5 minutes."
      - alert: HighMemoryUsage
        expr: (node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100 > 80
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High Memory usage detected on instance {{ $labels.instance }}"
          description: "Memory usage has exceeded 80% for more than 5 minutes."
      - alert: DiskSpaceUsage
        expr: node_filesystem_avail_bytes{mountpoint="/"} / node_filesystem_size_bytes{mountpoint="/"} * 100 < 20
        for: 10m
        labels:
          severity: lowd-disk-warning
        annotations:
          summary: "Low disk space on instance {{ $labels.instance }}"
          description: "Disk space is less than 20% available for more than 10 minutes."
      - alert: HighNetworkLatency
        expr: rate(node_network_receive_errs_total[5m]) > 1
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High network latency detected on instance {{ $labels.instance }}"
          description: "Network receive errors have exceeded 1 per second for more than 5 minutes."
      - alert: ServiceDown
        expr: up{job="my-service"} == 0
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "Service {{ $labels.job }} is down on instance {{ $labels.instance }}"
          description: "The service has been down for more than 2 minutes."
    ```
    This rule triggers if CPU usage exceeds 80% for more than 5 minutes.
4. **Test Alerting Rules**: Test the rules in a staging environment to ensure they trigger correctly.
5. **Deploy Rules**: Once tested, deploy the alerting rules in your production environment.
6. **Document Thresholds**: Clearly document the thresholds and the rationale behind them to ensure they are understood and maintained correctly.

# Steps to Configure Alert Manager
Begin by setting up the basic configuration in the `alertmanager.yml` file. This includes defining routes, receivers, and notification channels. 

   ```
global:
      resolve_timeout: 5m

    route:
      group_by: ['alertname']
      group_wait: 30s
      group_interval: 5m
      repeat_interval: 3h
      receiver: 'email_notifications'

    receivers:
    - name: 'email_notifications'
      email_configs:
      - to: 'anitha.annem.snaatak@gmail.com'
        from: 'alertmanager@opstree.com'
        smarthost: 'smtp.opstree.com:587'
        auth_username: 'alertmanager@opstree.com'
        auth_password: 'password@123'

    inhibit_rules:
    - source_match:
        severity: 'critical'
      target_match:
        severity: 'warning'
      equal: ['alertname', 'instance']
```
-  **Routing Alerts**: Set up routing rules to determine which alerts go to which receivers. 
-  **Notification Channels**: Configure various notification channels such as email, Slack, or PagerDuty. This ensures alerts reach the appropriate teams quickly.
-  **Grouping and Inhibition**: Group similar alerts to avoid alert fatigue. Use inhibition rules to suppress alerts that are less important when a related, more critical alert is active.
-  **Test Configuration**: Test the entire setup by triggering sample alerts. Verify that the alerts are received correctly and routed to the right channels.

# Step-by-Step Usage
1. **Monitoring**: Alert Manager continuously monitors incoming alerts from Prometheus. It checks the alert labels and routes them according to your configuration.
2. **Alert Deduplication**: When multiple alerts of the same type are triggered, Alert Manager deduplicates them, ensuring you don't receive multiple notifications for the same issue.
3. **Alert Grouping**: Alerts are grouped based on your configuration (e.g., by alert name, instance, or severity). This helps in managing alerts more effectively.
4. **Notification**: Once an alert is grouped and processed, Alert Manager sends notifications via the configured channels.
5. **Silencing Alerts**: If you're performing maintenance or are aware of an issue that's already being handled, you can silence alerts temporarily. This prevents unnecessary notifications.
6. **Inhibition**: Alerts can be suppressed based on inhibition rules. For instance, if a critical alert is active, related warning alerts might be inhibited to reduce noise.

# Severity Levels

| Level        | Meaning                              | Example Rules                     | Target Response Time |
| ------------ | ------------------------------------ | --------------------------------- | -------------------- |
| **Critical** | Immediate action; risk of outage     | `HighCPUUsage`, `LowDiskSpace`    | 15 min (PagerDuty)   |
| **Warning**  | Needs attention soon; degrade likely | `HighSwapUsage`, `HighDiskIOWait` | 1 h (Slack)          |
| **Info**     | Informational; no direct action      | Deployment annotations            | As needed            |



# Notification Channels

| Channel                 | Used For                   | Tool / Route                 |
| ----------------------- | -------------------------- | ---------------------------- |
| **PagerDuty**           | Critical alerts            | 24×7 on‑call rotation        |
| **Slack #infra-alerts** | Warning alerts, summaries  | Alertmanager webhook → Slack |
| **Email Ops DL**        | Info alerts, daily digests | Alertmanager email receiver  |

# Best Practices

| Practice                | Description                                 |
|-------------------------|---------------------------------------------|
| **Actionable Alerts**   | Focus on alerts that require immediate action. |
| **Tune Thresholds**     | Regularly refine to reduce false positives. |
| **Clear Documentation** | Keep alert rules and processes up to date.  |
| **Test Regularly**      | Validate alerts and notification flows.     |
| **Team Training**       | Ensure the team knows how to respond.       |

# Conclusion
A well-configured Alert Manager is critical for maintaining infrastructure reliability and minimizing downtime. By designing clear, actionable alerts, routinely refining configurations, and ensuring strong team readiness, you can empower your operations to detect and resolve incidents proactively. This approach not only enhances system stability but also builds confidence in monitoring and incident response processes.

## Contact Information

| Name  | Email                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Sonal | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |
# References

| Reference                               | Description                                      |
|-----------------------------------------|--------------------------------------------------|
| [Prometheus Documentation](https://prometheus.io/docs/) | Official documentation for Prometheus.            |
| [Grafana Documentation](https://grafana.com/docs/)     | Official documentation for Grafana.               |
| [Alert Manager Documentation](https://prometheus.io/docs/alerting/latest/alertmanager/) | Official documentation for Alert Manager.         |
