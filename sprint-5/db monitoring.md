

# Alerting Rules and Process for Database Monitoring
<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/e6fd940b-65da-44f2-953f-8a025fbf42da" />


## Author Information

| Created by | Created on | Version | Last Updated On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------- | ---------- | ------- | --------------- | ------------ | ----------- | ----------- | ----------- |
| Sonal      | 17-09-2025 | V 1.0   | 17-09-2025      | Neelesh      |             |             |             |

         
# Table of Content: 

- [Introduction](#introduction)
- [Alerting Rules](#alerting-rules)
- [Notification Channels](#notification-channels)
- [Escalation Process](#escalation-process)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [Reference](#reference)



# Introduction

This document defines the alerting rules and operational processes for monitoring database systems. By establishing well-defined alerts, notification channels, and escalation steps, the goal is to ensure high availability, data integrity, and optimal performance of critical databases.

The guidelines outlined here help the DBA team and stakeholders proactively identify and resolve potential issues before they impact business operations.



# Alerting Rules

| **Metric**         | **Condition**                         | **Severity** | **Threshold**            | **Duration**    | **Notification Message**                                 |
|--------------------|--------------------------------------|-------------|--------------------------|----------------|--------------------------------------------------------|
| CPU Utilization    | CPU usage exceeds limit              | Medium      | > 80%                   | 5 min         | "CPU utilization has exceeded 80% for 5 minutes on DB instance." |
| Memory Usage       | Memory usage exceeds limit           | High        | > 75%                   | 10 min        | "Memory usage has exceeded 75% for 10 minutes on DB instance." |
| Disk Space Usage   | Disk usage exceeds limit             | High        | > 85%                   | Immediate     | "Disk space usage has exceeded 85% on DB instance."    |
| Query Performance  | Avg. query time exceeds limit        | Medium      | > 200 ms               | 15 min        | "Average query execution time has exceeded 200 ms on DB instance." |
| Connection Errors  | Connection errors exceed count      | High        | > 10 errors in 5 min | 5 min         | "Connection errors exceeded 10 in last 5 minutes on DB instance." |
| Replication Lag    | Replication delay exceeds limit      | High        | > 5 min               | 10 min        | "Replication lag exceeded 5 minutes for last 10 minutes on DB instance." |
| Deadlocks          | Deadlocks exceed count               | High        | > 10/hour            | 1 hour       | "More than 10 deadlocks detected in last hour on DB instance." |
| Backup Failures    | Backup job fails                     | High        | Any failure           | Immediate     | "Scheduled backup failed on DB instance."               |


#  Notification Channels

- **Email:** Alerts are sent to the DBA team email list .
- **Slack:** Alerts are posted in the #db-alerts channel.
- **PagerDuty:** Critical alerts trigger PagerDuty notifications to on-call DBAs.
- **SMS:** High-severity alerts are also sent via SMS to on-call personnel.

#  Escalation Process

**First Level Response:**
- **On-Call DBA:** Receives the alert and investigates within 15 minutes.
- **Actions:** Initial troubleshooting, log analysis, and basic remediation steps.

**Second Level Response:**
- **Senior DBA:** Escalation if the issue is not resolved within 30 minutes.
- **Actions:** Deeper investigation, applying patches or workarounds, engaging other teams if necessary.

**Third Level Response:**
- **Database Team Lead:** Escalation if the issue remains unresolved after 1 hour.
- **Actions:** Full incident management, involving stakeholders, coordinating with other departments, and making critical decisions.



#  Conclusion

Effective database alerting and monitoring are critical for maintaining data integrity and service availability. By following these defined rules and processes, teams can minimize downtime, improve response times, and enhance overall reliability. Continuous review and refinement help adapt to evolving environments and ensure proactive incident management.


#  Contact Information


| Name  | Email                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Sonal | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |


#  Reference

| **Link**                                                                 | **Description**                                      |
|--------------------------------------------------------------------------|------------------------------------------------------|
| [AlertManager](https://medium.com/devops-dudes/prometheus-alerting-with-alertmanager-e1bbba8e6a8e)%7C Alert manager|
| [Metrics Monitoring and Alerting System Design](https://medium.com/@guptagoutam2021/how-to-design-a-metrics-monitoring-and-alerting-system-87c02e990dd1)%7CMetrics Monitoring and Alerting System Design|
