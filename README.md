
# AWS CloudWatch Dashboards for Centralized Monitoring

This project showcases the implementation of **custom AWS CloudWatch Dashboards** to centrally monitor key AWS resources such as billing, network traffic, logs, and security metrics. It aims to improve operational visibility, help in real-time monitoring, and provide a consolidated view for DevOps teams.

---

## 🎯 Project Objective

To build a **centralized monitoring system** using Amazon CloudWatch that provides insights into:

- 💰 Billing and Cost
- 🛡️ Security (IAM, GuardDuty, etc.)
- 🌐 Network Performance (VPC, ELB, etc.)
- 📄 Log Insights (from EC2, Lambda, etc.)

---

## 🧩 Components Used

| Service         | Purpose                                      |
|------------------|----------------------------------------------|
| **CloudWatch**     | Dashboard, Metrics, Alarms, Logs             |
| **S3**             | Log storage (for centralized access)         |
| **IAM**            | Access control for metrics and dashboards    |
| **Lambda (optional)** | Custom metric generation                    |
| **Billing Console** | Used to integrate cost metrics into dashboard |

---

## 📁 Project Structure

```

cloudwatch-central-dashboard/
├── dashboard-template.json      # Sample JSON for dashboard configuration
├── create\_dashboard.sh          # AWS CLI script to deploy dashboard
├── screenshots/                 # Screenshots of live dashboards (optional)
└── README.md                    # Project documentation

````

---

## 🚀 Setup Instructions

### 1️⃣ Prerequisites

- AWS CLI configured (`aws configure`)
- Required permissions to access CloudWatch and billing metrics

### 2️⃣ Enable Billing Metrics

Go to:  
**AWS Console → Billing → Preferences → Enable "Receive Billing Alerts"**

Then enable the following:

```bash
aws ce enable-cost-explorer
````

### 3️⃣ Create Dashboard Using AWS CLI

Use the script or manually run:

```bash
aws cloudwatch put-dashboard \
  --dashboard-name "Central-Monitoring-Dashboard" \
  --dashboard-body file://dashboard-template.json
```

---

## 📊 Dashboard Sections

### 💰 **Billing & Cost Monitoring**

* Monthly estimated charges (overall + per service)
* Linked accounts billing (for orgs)

### 📄 **Logs Monitoring**

* Number of logs from EC2, Lambda, and VPC
* CloudWatch log group ingestion volume

### 🌐 **Network Monitoring**

* VPC Flow Logs metrics
* ELB request count and latency
* NAT Gateway traffic

### 🛡️ **Security Monitoring**

* GuardDuty finding count
* Unusual IAM activity
* Root user usage alert

---

## 🔔 Optional: Add Alarms

Create alarms for critical thresholds (e.g., cost > ₹5000 or CPU > 80%)

```bash
aws cloudwatch put-metric-alarm \
  --alarm-name "High-CPU-Alert" \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 2 \
  --alarm-actions <SNS_TOPIC_ARN> \
  --dimensions Name=InstanceId,Value=<EC2_ID>
```

---

## ✅ Benefits

* Central view of AWS health and cost
* Real-time performance and security insights
* Faster troubleshooting and audit readiness

---

