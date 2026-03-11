# Automated Incident Response System using CloudWatch Alarms and Lambda Remediation

## Project Overview

This project demonstrates an automated incident response system on AWS.
The system automatically detects issues using CloudWatch alarms and triggers a Lambda function to perform remediation actions without manual intervention.

This helps improve system reliability, reduces downtime, and enables faster incident resolution.

---

## Architecture
1. launch instance 
2. AWS resource generates metrics (CPU usage)
3. CloudWatch monitors these metrics.
4. CloudWatch Alarm is triggered when a threshold is exceeded.
5. The alarm triggers an AWS Lambda function.
6. Lambda performs remediation (for example restarting an EC2 instance).

---

## Technologies Used

* AWS CloudWatch
* AWS Lambda
* AWS EC2
* Python

---

## Workflow

EC2 Instance → CloudWatch Metrics → CloudWatch Alarm → Lambda Trigger → Automated Remediation

Example Scenario:

* CPU usage exceeds threshold
* CloudWatch alarm is triggered
* Lambda function runs automatically
* Lambda restarts the EC2 instance

---

## Implementation Steps

### 1. Launch EC2 Instance

Create an EC2 instance that will be monitored.

### 2. Create Lambda Function

Create a Lambda function that performs remediation.

**Example Python code:**

```
import boto3
import json

ec2 = boto3.client('ec2')

def lambda_handler(event, context):

    instance_id = "i-09ee7872e12ad5ba3"

    try:
        print("CloudWatch Alarm Event:", json.dumps(event))
        print("Restarting instance:", instance_id)

        ec2.reboot_instances(
            InstanceIds=[instance_id]
        )

        print("Instance reboot initiated successfully")

        return {
            'statusCode': 200,
            'body': json.dumps('EC2 reboot triggered successfully!')
        }

    except Exception as e:
        print("Error occurred:", str(e))
        return {
            'statusCode': 500,
            'body': json.dumps('Error rebooting EC2 instance')
        }
```

### 3. Create CloudWatch Alarm

Configure an alarm for a metric such as:

* CPU Utilization > 70%

Set the alarm action to trigger the Lambda function.

### 4. Test the System

Generate load on the EC2 instance so CPU usage increases.

Once the threshold is crossed:

* CloudWatch alarm triggers
* Lambda executes
* EC2 instance is automatically rebooted

---

---

**Implementation Steps**

1. **EC2 Instance**

<img width="1920" height="1008" alt="Instance details _ EC2 _ ap-southeast-1 - Google Chrome 3_11_2026 10_27_33 PM" src="https://github.com/user-attachments/assets/a3d03900-461d-4ed2-b535-93db224aa8af" />

2. **CloudWatch Alarm configuration**
 
![WhatsApp Image 2026-03-11 at 2 55 24 PM](https://github.com/user-attachments/assets/dd55162c-dca3-4872-9dc6-b0aa329f8cf2)

3. **Lambda function configuration**

![WhatsApp Image 2026-03-11 at 3 02 58 PM](https://github.com/user-attachments/assets/5eefc5b9-8b28-4f68-9099-7d7121d4c38b)

4. **Alarm trigger event**

![WhatsApp Image 2026-03-11 at 3 31 04 PM](https://github.com/user-attachments/assets/1f0a8cfa-2458-469d-8c9d-90cbce1caa8b)

5. **Lambda execution logs**

 ![WhatsApp Image 2026-03-11 at 3 43 40 PM](https://github.com/user-attachments/assets/6eefed12-4907-4fad-b3b9-147f83241504)

---

## Conclusion

This project demonstrates how AWS services can be integrated to create an automated incident response system. Using CloudWatch alarms and Lambda functions helps organizations automatically respond to system issues and maintain high availability.

---

