# 
### README.md


# CloudPulse Alerting System

A fully serverless pipeline for custom metric ingestion and threshold‑based alerting on AWS.

## 🛠 Technologies
- AWS Lambda (Python 3.9)  
- Amazon CloudWatch (Metrics & Alarms)  
- Amazon SNS (notifications)  
- AWS SAM / CloudFormation (infra as code)  
- Python boto3 SDK

## 📂 Structure
- **lambda/handler.py** – Lambda function writes `ErrorRate` and `LatencyMs` metrics to CloudWatch  
- **lambda/requirements.txt** – boto3 dependency  
- **infra/template.yaml** – SAM/CloudFormation template defining:
  - `MonitoringFunction` (API Gateway + Lambda)  
  - `HighErrorAlarm` & `HighLatencyAlarm` (CloudWatch alarms)  
  - `SNSTopic` for alerting  
- **infra/alarm-config.yml** – overrideable thresholds for error rate and latency

## 🔧 Setup & Deploy

1. **Install SAM CLI**  
   ```bash
   # macOS
   brew install aws-sam-cli
   # Windows
   choco install aws-sam-cli
