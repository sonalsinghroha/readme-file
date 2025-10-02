

#  Metrices For Infra Monitoring 
<img width="520" height="280" alt="image" src="https://github.com/user-attachments/assets/b1dedbf9-684c-4112-a946-8dee22ba3fb9" />

## Author Information

| Created by | Created on | Version | Last Updated On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------- | ---------- | ------- | --------------- | ------------ | ----------- | ----------- | ----------- |
| Sonal      | 17-09-2025 | V 1.0   | 17-09-2025      | Neelesh      |             |             |             |

# Introduction
The aim of this project is to set up a robust monitoring system using Grafana and Prometheus to track CPU and memory utilization on EC2 instances. By monitoring these key metrics in real-time, we can identify performance bottlenecks, optimize resource allocation, and ensure the smooth operation of our infrastructure.


# Prerequisites

| Resources                   | Description                        |
|-----------------------------|------------------------------------|
| **Ubuntu Server**           | Version 20.04 or later             |
| **SSH Access to the Server**| Port 22 Open                       |
| **CPU**                     | At least 1 core                    |
| **Memory**                  | Minimum 1 GB RAM                   |
| **Storage**                 | Minimum 2 GB of free disk space    |
| **Instance Type**           | t2.micro                           |

#  Step 1: Install Node Exporter (on target server)

<img width="1496" height="217" alt="image" src="https://github.com/user-attachments/assets/f9942310-b58d-443f-9c77-07d0a40333da" />

### Node Exporter metrics available at: http://<server-ip>:9100/metrics

# Step 2: Install Prometheus

<img width="1482" height="252" alt="image" src="https://github.com/user-attachments/assets/128d2785-dd04-430d-83fd-4b00ff6cd2c0" />

## Configure prometheus.yml
```
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'node_exporter_metrics'
    static_configs:
      - targets: ['<server-ip>:9100']
```

## Run Prometheus
```
./prometheus --config.file=prometheus.yml
```


### Prometheus UI: http://<server-ip>:9090

#  Step 3: Install Grafana
Follow these steps for the installation of Grafana [Grafana Installation](https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/)
<img width="1343" height="67" alt="image" src="https://github.com/user-attachments/assets/446be938-48e0-4126-afac-ec05648eb463" />

### Grafana UI: http://<server-ip>:3000 (default user: admin / admin)


<img width="1566" height="896" alt="image" src="https://github.com/user-attachments/assets/c914bb58-8e5c-454b-9da3-152491c9fea8" />

# Add Alerts in Prometheus

## Create apirules.yml
<img width="1859" height="846" alt="image" src="https://github.com/user-attachments/assets/2f9cd617-820b-4514-8008-41cfc4ba4e9c" />

## Link the Alert Rules in prometheus.yml
<img width="1092" height="419" alt="image" src="https://github.com/user-attachments/assets/50f7f5fb-ac83-41ae-8778-8ad2c2bf8432" />

## Restart Prometheus:
```
./prometheus --config.file=prometheus.yml
 ```
<img width="1904" height="585" alt="image" src="https://github.com/user-attachments/assets/ee098ab4-e1c8-4f42-92fc-e6e799c81a95" />



## Contact Information

| Name  | Email                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Sonal | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |


#  References

| Reference                       | Description                                                        |
|---------------------------------|--------------------------------------------------------------------|
| [Grafana](https://grafana.com/)   | Open-source platform for monitoring and observability, featuring customizable dashboards. |
| [Prometheus](https://prometheus.io/) | Open-source monitoring and alerting toolkit, designed for reliability and scalability. |
