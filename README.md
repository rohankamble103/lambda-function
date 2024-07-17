# AWS Lambda and S3 Integration Project

This project demonstrates a workflow using AWS Lambda, S3, and RDS to fetch data from a MySQL/RDS database, convert it into an `.xlsx` file, and manage file transfers between S3 buckets.

## Sequence Diagram

![Sequence Diagram](/diagram.png)


## Workflow Overview

1. **Source S3 Bucket Creation**:
   - Created an S3 bucket (Bucket1 - Source).

2. **Lambda Function 1**:
   - Created a Lambda function (Lambda Function 1) to:
     - Fetch data from the MySQL/RDS database.
     - Convert the data into an `.xlsx` file.
     - Upload the `.xlsx` file to the source S3 bucket (Bucket1).
   - Created and attached an IAM role to Lambda Function 1 with permissions to access RDS and S3.

3. **Destination S3 Bucket Creation**:
   - Created another S3 bucket (Bucket2 - Destination).

4. **Lambda Function 2**:
   - Created a second Lambda function (Lambda Function 2) to:
     - Be triggered by new `.xlsx` files uploaded to the source S3 bucket (Bucket1).
     - Copy the `.xlsx` file from the source S3 bucket (Bucket1) to the destination S3 bucket (Bucket2).
   - Created and attached an IAM role to Lambda Function 2 with permissions to access both S3 buckets.

5. **S3 Trigger Configuration**:
   - Set up a trigger on the source S3 bucket (Bucket1) to invoke Lambda Function 2 whenever a new `.xlsx` file is uploaded.

## Sequence of Operations

1. **User** creates an S3 bucket (`Bucket1 - Source`).
2. **User** creates an IAM role with RDS and S3 access and attaches it to **Lambda Function 1**.
3. **User** creates **Lambda Function 1**:
   - **Lambda Function 1** fetches data from the RDS database, converts it into an `.xlsx` file, and uploads it to `Bucket1`.
4. **User** creates another S3 bucket (`Bucket2 - Destination`).
5. **User** creates **Lambda Function 2**:
   - **Lambda Function 2** is triggered by the addition of new `.xlsx` files in `Bucket1`.
   - **Lambda Function 2** copies the `.xlsx` files from `Bucket1` to `Bucket2`.
6. **User** sets up an S3 trigger on `Bucket1` to invoke **Lambda Function 2** upon new `.xlsx` file uploads.

## Dependencies

- **AWS SDK**
- **boto3** for Python
- **pandas** and **openpyxl** for handling `.xlsx` files
- **pymysql** for connecting to RDS MySQL databases

Ensure all dependencies are packaged with your Lambda function code or included in a Lambda layer.

## Setup Instructions

1. **Create the S3 Buckets**:
    - Create two S3 buckets: one as the source (Bucket1) and one as the destination (Bucket2).

2. **Create and Attach IAM Roles**:
    - Create an IAM role with permissions for S3 and RDS access.
    - Attach this IAM role to Lambda Function 1.
    - Create another IAM role with permissions for S3 access.
    - Attach this IAM role to Lambda Function 2.

3. **Create Lambda Functions**:
    - Create two Lambda functions:
        - Lambda Function 1: Fetches data from RDS, converts it to an `.xlsx` file, and uploads it to Bucket1.
        - Lambda Function 2: Copies `.xlsx` files from Bucket1 to Bucket2.

4. **Configure S3 Trigger**:
    - Set up an S3 trigger on Bucket1 to invoke Lambda Function 2 whenever an `.xlsx` file is uploaded.

5. **Deploy and Test**:
    - Deploy your Lambda functions and ensure they are configured correctly.
    - Test the setup by uploading an `.xlsx` file to Bucket1 and verifying it is copied to Bucket2.
  

