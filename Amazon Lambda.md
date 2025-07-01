# Amazon Lambda
> AWS Lambda is a serverless, event-driven compute service that lets you run code without provisioning or managing servers. You only pay for the compute time your code uses.

No server management
Automatic scaling
Event-driven execution
Supports many languages

## Key Concepts
| Concept |	Description |
| ------- | ----------- |
| Function | A standalone unit of execution in Lambda |
| Event | A JSON payload that triggers the Lambda function |
| Trigger |	A service/event that invokes the Lambda function (e.g., S3, API Gateway) |
| Execution Role | IAM role that Lambda uses to access other AWS resources |
| Handler | Entry point of your Lambda code |
| Runtime |	Language environment used to run your function |
| Timeout | Maximum time a Lambda function can run (default: 3s, max: 15 mins) |

## Supported Runtimes
Node.js

Python

Java

Go

Ruby

.NET Core

Custom Runtime (using Amazon Linux)

## Common Use Cases
Responding to API requests (via Amazon API Gateway)

Processing files uploaded to S3

Real-time data transformations (e.g., Kinesis, DynamoDB Streams)

Scheduled tasks (cron jobs via EventBridge)

Backend logic for mobile/web apps

Automation and serverless orchestration

## Lambda Function Lifecycle
Create Function via AWS Console, CLI, or SDK.

Define a Trigger (e.g., S3 upload, HTTP request).

Write/Upload Code (inline, zip file, or container).

Configure Settings:

Memory (128 MB to 10 GB)

Timeout (up to 15 minutes)

Environment variables

VPC configuration (if needed)

Deploy & Invoke.

Monitor via CloudWatch logs & metrics.

## Event Sources (Triggers)
| AWS Service | Use Case Example |
| ----------- | ---------------- |
| Amazon S3 |Run code on file upload |
| Amazon DynamoDB | Streams	React to table changes |
| Amazon Kinesis | Real-time stream processing |
| Amazon SQS | Process messages from a queue |
| API Gateway |	Create RESTful APIs |
| EventBridge / CloudWatch Events | Scheduled jobs or event bus |
| Cognito, IoT Core, SNS | Event-driven workflows |

## Permissions and Security
Lambda uses IAM execution roles to access other AWS resources.

Control who can invoke your function with resource-based policies.

Can run inside a VPC for secure access to private subnets/databases.

## Monitoring and Debugging
| Tool | Purpose |
| ---- | ------- |
| CloudWatch Logs | Automatically collects logs from function output |
| CloudWatch Metrics | Memory usage, duration, invocation count, error rate |
| X-Ray | Distributed tracing to see execution path and bottlenecks |
| Lambda Insights | Performance profiling and troubleshooting |

## Pricing
Lambda pricing is based on:

Number of requests: First 1M/month are free

Duration: Based on the time your code runs, rounded to the nearest millisecond

Memory size: More memory = more cost

Free Tier:

1 million requests/month

400,000 GB-seconds/month

## Creating a Lambda Function (Example – Python)
Console Steps:
Go to Lambda Console

Click “Create Function”

Choose:

Runtime: Python 3.9

Role: Create or use existing

Add this code:

python
Copy
Edit
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Hello from Lambda!'
    }
Test the function with sample JSON.

## Deploy via AWS CLI
bash
Copy
Edit
aws lambda create-function \
  --function-name myLambda \
  --runtime python3.9 \
  --handler lambda_function.lambda_handler \
  --role arn:aws:iam::123456789012:role/myLambdaRole \
  --zip-file fileb://function.zip

## Using Environment Variables
python
Copy
Edit
import os

def lambda_handler(event, context):
    value = os.environ['MY_ENV_VAR']
    print("Value is:", value)
Set this in Lambda console under "Environment Variables".

## Error Handling & Retries
Synchronous invocations (e.g., API Gateway): Returns error to caller

Asynchronous invocations (e.g., S3): Retries twice with exponential backoff

Dead Letter Queues and on-failure destinations can capture failed events

## Deployment Methods
Method	Use When...
Inline editor	Simple quick code changes
ZIP file upload	Small projects or CI/CD
S3 deployment	For large functions
Container Image	For custom runtime or dependencies
AWS SAM or CDK	For infrastructure-as-code
Serverless Framework	For multi-cloud/serverless projects

## Lambda Limits
Resource	Limit (default)
Memory allocation	128 MB to 10 GB
Max execution timeout	15 minutes
Package size (zip)	50 MB (compressed), 250 MB (uncompressed)
Environment variables	4 KB
Concurrency (soft limit)	1000 (can request increase)

## Best Practices
Keep functions small and focused (single responsibility)

Use environment variables for config

Minimize package size for faster cold starts

Enable VPC only if needed, as it increases latency

Monitor with CloudWatch & X-Ray

Use layers to share common dependencies

Use versioning and aliases for safe deployments

## Lambda Layers
Allow you to share code and dependencies (e.g., libraries, custom runtimes) across multiple functions.

bash
Copy
Edit
aws lambda publish-layer-version \
  --layer-name my-layer \
  --zip-file fileb://layer.zip \
  --compatible-runtimes python3.
  
## Conclusion
AWS Lambda is a core part of the serverless architecture model, enabling event-driven, scalable, and cost-effective applications. From data pipelines and APIs to automation and real-time file processing, Lambda eliminates server maintenance and scales seamlessly with your workloads.






