# Exponentiation Calculator

This project implements a serverless application for exponentiation using **AWS Amplify**, **API Gateway**, **Lambda**, **DynamoDB**, and **IAM**.

---

## Architecture Design

![Architecture Diagram](https://github.com/user-attachments/assets/6635fe89-caf2-45e5-b608-3a4cea225288)

---

## Application Workflow

1. **Frontend**:  
   Deployed using AWS Amplify for hosting and application management.

2. **Backend**:  
   - API Gateway creates a RESTful endpoint for communication between the frontend and backend.  
   - AWS Lambda handles the computation of exponentiation.

3. **Database**:  
   DynamoDB stores computation results for future reference.

4. **Security**:  
   IAM ensures that only authorized services and roles can access resources.

---

## Steps and Implementation

### 1. Frontend Deployment with AWS Amplify
- Deployed the frontend website code using **AWS Amplify**, which handles hosting, domain management, and scaling automatically.  
![Amplify Deployment](https://github.com/user-attachments/assets/df9b21f6-270d-4b11-b4c5-4fb3bb53beee)

![Website](https://github.com/user-attachments/assets/0082aca1-f1f9-4d4e-9d98-e04079232914)

![Website Result](https://github.com/user-attachments/assets/d863fb8d-8f4e-4812-ac02-13224004bc61)

---

### 2. API Gateway: RESTful Endpoint Creation
- Configured **API Gateway** to create a RESTful endpoint for user interactions.  
- Enabled **CORS** to ensure seamless communication between the frontend and backend.  
![API Gateway Setup](https://github.com/user-attachments/assets/d1f297fd-88db-448c-b1c0-fecf3a02b4da)

---

### 3. Backend Logic with AWS Lambda
- Wrote the backend computation for exponentiation in **Python**, deployed as an AWS Lambda function.
- Integrated **DynamoDB** to log results with timestamps for tracking.

#### Lambda Function Code:
```python
import json
import math
import boto3
from time import gmtime, strftime

# Create DynamoDB resource
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('PowerofMathDatabase')

# Current timestamp
now = strftime("%a, %d %b %Y %H:%M:%S +0000", gmtime())

def lambda_handler(event, context):
    # Perform exponentiation
    mathResult = math.pow(int(event['base']), int(event['exponent']))
    
    # Store result in DynamoDB
    response = table.put_item(
        Item={
            'ID': str(mathResult),  # Unique identifier
            'LatestGreetingTime': now  # Timestamp
        }
    )
    
    # Return the result
    return {
        'statusCode': 200,
        'body': json.dumps(f'Your result is {mathResult}')
    }
```

---

### 4. IAM Role and Policies
Created an IAM role for the Lambda function with an inline policy that allows the following DynamoDB actions:
- Insert (`PutItem`)  
- Delete (`DeleteItem`)  
- Retrieve (`GetItem`, `Query`, `Scan`)  
- Update (`UpdateItem`)  

#### IAM Policy:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "dynamodb:PutItem",
                "dynamodb:DeleteItem",
                "dynamodb:GetItem",
                "dynamodb:Scan",
                "dynamodb:Query",
                "dynamodb:UpdateItem"
            ],
            "Resource": "arn:aws:dynamodb:ap-south-1:471112537693:table/PowerofMathDatabase"
        }
    ]
}
```

---

### 5. Database: AWS DynamoDB
Created a DynamoDB table named **PowerofMathDatabase** to log computation results and timestamps for reference.

#### Sample Database Record:
| ID       | LatestGreetingTime               |  
|----------|----------------------------------|  
| 1024.0   | Tue, 17 Dec 2024 14:35:50 +0000 |  

---

## Testing and Results

### Lambda Function Execution
The function executes correctly, computing the power of numbers based on inputs provided via API Gateway.  
![Lambda Execution](https://github.com/user-attachments/assets/d471a86b-96f8-45e4-b94b-799b256c7aa2)

---

### Database Logs
Computation results, along with timestamps, are stored in DynamoDB for future reference.  
![DynamoDB Logs](https://github.com/user-attachments/assets/261b0d13-9ca0-4b3e-be41-1911470feadc)
