# Real-Time Monitoring and Cost Tracking on AWS (CloudWatch + SNS)

## Overview

This project sets up a basic real-time monitoring and cost tracking solution on AWS using **Amazon CloudWatch**, **Amazon SNS**, and simple **billing alerts**.  
The goal is to receive automatic notifications when resource metrics cross defined thresholds or when AWS costs exceed a budget.

**Flow:**

1. AWS resources (e.g., EC2) send **metrics and logs** to CloudWatch.
2. **CloudWatch Alarms** evaluate metrics and enter ALARM state on thresholds.
3. Alarms publish messages to an **SNS Topic**.
4. SNS forwards **email notifications** to subscribed users.
5. Optional: billing / budget alerts for AWS account-level costs.

---

## Prerequisites

- Active AWS account
- Existing AWS resources to monitor (e.g., EC2 instance)
- Valid email address for receiving alerts

---

## Step-by-Step Setup

### 1. Create SNS Topic for Notifications

1. Open **Amazon SNS** in the AWS console.
2. Go to **Topics → Create topic**.
3. Type: `Standard`.
4. Name: `monitoring-alerts`.
5. Click **Create topic**.

### 2. Subscribe Your Email

1. Inside `monitoring-alerts` topic → click **Create subscription**.
2. Protocol: `Email`.
3. Endpoint: your email address.
4. Click **Create subscription**.
5. Check your inbox and **Confirm subscription**.

### 3. Create CloudWatch Alarm for EC2

1. Open **CloudWatch → Alarms → All alarms → Create alarm**.
2. Click **Select metric**.
3. Navigate to: `EC2 → Per-Instance Metrics → CPUUtilization`.
4. Choose the instance you want to monitor.
5. Configure the alarm:
   - Statistic: `Average`
   - Period: `5 minutes`
   - Threshold: `>= 80%` (example)
6. In **Notification** section:
   - Alarm state: `In alarm`
   - Send notification to **SNS topic**: `monitoring-alerts`.
7. Name the alarm (e.g., `high-cpu-ec2`) and create it.

### 4. Add Basic Cost Tracking (Budget Alert)

1. Go to **Billing → Budgets**.
2. Click **Create budget**.
3. Choose **Cost budget**.
4. Set monthly amount (e.g., `$10`).
5. Add an alert threshold (e.g., 80% of budget).
6. Add your email for notifications.
7. Complete creation.

### 5. Test the Setup

- Temporarily lower CPU threshold or generate load on EC2.
- Wait for the alarm to trigger.
- Confirm you receive an email from SNS.
- If cost crosses budget, you’ll receive a budget alert email as well.

---

## Key Learnings

- How to configure CloudWatch metrics and alarms.
- How to use SNS topics and subscriptions for notifications.
- Basic cost tracking using AWS Budgets.
- Building a simple but effective monitoring foundation.

Reference : https://www.youtube.com/watch?v=PcmmvsFieYA

