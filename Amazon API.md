## Amazon API Gateway
> Amazon API Gateway is a fully managed service that enables you to create and expose RESTful, WebSocket, and HTTP APIs to applications running on the web, mobile, or on AWS.

It acts as a "front door" for applications to access backend services like:

AWS Lambda

EC2

DynamoDB

Any HTTP endpoint

## Key Features
Supports REST, HTTP, and WebSocket APIs

Built-in authorization and throttling

Custom domain names and SSL support

Caching with API Gateway cache

Monitoring with CloudWatch

SDK generation for clients

Request validation and transformation

Native integration with AWS Lambda

## Types of APIs
| API Type | Use Case |
| -------- | -------- |
|REST API |	Traditional RESTful endpoints with fine-grained features |
| HTTP API | Lightweight, faster, and cheaper alternative to REST APIs |
| WebSocket API | Real-time, two-way communication (e.g., chat apps, dashboards) |

## API Gateway Architecture
arduino
Copy
Edit
Client → API Gateway → Backend (Lambda, EC2, HTTP, DynamoDB, etc.)

## Components of API Gateway
| Component | Description |
| --------- | ----------- |
| Resource | A URL path (e.g., /users) |
| Method | HTTP verb (GET, POST, PUT, DELETE) on a resource |
| Integration |	Target for the method (Lambda, HTTP endpoint, etc.) |
| Stage	| Deployment environments (e.g., dev, prod) |
| Deployment | A snapshot of your API for a stage |
| Mapping Templates | Transform request/response payloads |
| Models | Define the structure of request/response bodies |
| Authorizers | Custom or AWS Cognito-based authentication |
| Usage Plans |	Define quotas and throttling |
| API Keys | Access control and usage tracking |
| Custom Domain Names | Use your own domain with APIs |

## Backends You Can Integrate
AWS Lambda (serverless compute)

Amazon EC2 (web servers)

AWS Elastic Beanstalk

Amazon DynamoDB

Any public HTTP endpoint

Amazon SQS, SNS (via Lambda proxy)

## Common Use Cases
Expose Lambda functions as REST or HTTP APIs

Build backend services for mobile/web applications

Create real-time WebSocket apps

Integrate with third-party services

Create microservices APIs

Act as a proxy to internal or external services

## API Gateway + Lambda Example (Serverless API)
Architecture:

arduino
Copy
Edit
Client → API Gateway → Lambda → DynamoDB
Example Flow:
Client makes POST request to /users

API Gateway triggers Lambda

Lambda stores user data in DynamoDB

API Gateway returns success message

## Security Options
| Security Mechanism | Description |
| ------------------ | ----------- |
| IAM-based Auth | Secure APIs with IAM policies (used with AWS SDK) |
| Lambda Authorizers | Custom logic to allow or deny requests |
| Amazon Cognito | Add user pools for authentication and tokens |
| API Keys | Identify callers and enforce usage plans |
| Resource Policies | Control who can invoke the API from which IPs or accounts |

## Rate Limiting and Throttling
Defined using usage plans

Control access using:

Rate limit: Max requests per second

Burst limit: Short-term surge handling

Quota: Requests per day/week/month

## Monitoring and Analytics
CloudWatch Logs: View logs for each API call

CloudWatch Metrics: Track latency, 4XX/5XX errors, request counts

X-Ray Tracing: Diagnose performance issues and bottlenecks

Access Logs: Customize logging format to capture client details

## Deployment Process
Define resources and methods

Create a deployment

Assign the deployment to a stage (/dev, /prod)

Test and monitor your API

## Request and Response Mapping
You can customize the payload passed to backend and response returned using:

Mapping Templates (Velocity Template Language - VTL)

Models for schema validation

Binary support for images and files

## Caching
Enable caching at the stage level

Reduce backend load

Improve latency

Configurable TTL and per-method caching

## Custom Domain Setup
bash
Copy
Edit
# Associate domain with your API
aws apigateway create-domain-name \
  --domain-name api.mydomain.com \
  --certificate-arn arn:aws:acm:...

# Map domain to API stage
aws apigateway create-base-path-mapping \
  --domain-name api.mydomain.com \
  --rest-api-id abc123 \
  --stage prod

## Pricing Overview
Number of API calls

Data transferred out

Caching (if used)

WebSocket connections (per minute)

HTTP APIs are cheaper than REST APIs

Free tier includes:

1M REST or HTTP API calls/month

1M messages for WebSocket/month

## Creating an API with AWS CLI (Quick Example)
bash
Copy
Edit
aws apigateway create-rest-api --name 'MyAPI'
bash
Copy
Edit
# Create resource /users
aws apigateway create-resource \
  --rest-api-id <api-id> \
  --parent-id <root-id> \
  --path-part users
bash
Copy
Edit
# Create POST method
aws apigateway put-method \
  --rest-api-id <api-id> \
  --resource-id <resource-id> \
  --http-method POST \
  --authorization-type NONE
bash
Copy
Edit
# Integrate with Lambda
aws apigateway put-integration \
  --rest-api-id <api-id> \
  --resource-id <resource-id> \
  --http-method POST \
  --type AWS_PROXY \
  --integration-http-method POST \
  --uri arn:aws:apigateway:region:lambda:path/2015-03-31/functions/arn:aws:lambda:.../invocations

## Best Practices
Use HTTP APIs for simple use cases to save cost

Enable throttling and quotas to protect your backend

Use Lambda authorizers for custom authentication logic

Deploy APIs to multiple stages (dev, test, prod)

Secure sensitive APIs with IAM, Cognito, or Lambda auth

Leverage API caching to improve performance

Use models and validation to protect backends

## Conclusion
Amazon API Gateway is a powerful tool for building secure, scalable, and serverless APIs. It integrates seamlessly with AWS services, offers flexible authorization, and supports real-time applications with WebSocket support.

