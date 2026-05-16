# Floci Project Overview

## Purpose
Floci is a Java-based local AWS emulator — an open-source alternative to LocalStack Community.
Its goal is full AWS SDK and AWS CLI compatibility through real AWS wire protocols.

- Port: 4566
- Docker image: `floci/floci:latest`
- License: MIT

## Tech Stack
- Java 25
- Quarkus 3.34.6 (RESTEasy Reactive / JAX-RS)
- JUnit 5
- RestAssured
- Jackson (JSON)
- Maven (with `./mvnw` wrapper)
- Docker (for Lambda, RDS, ElastiCache integration tests)

## Supported AWS Services
ACM, API Gateway, API Gateway V2, AppConfig, Athena, AutoScaling, Backup, BCM Data Exports,
Bedrock Runtime, CE, CloudFormation, CloudWatch, CodeBuild, CodeDeploy, Cognito, CUR,
DynamoDB, EC2, ECR, ECS, EKS, ElastiCache, ELBv2, EventBridge, Firehose, Glue, IAM,
Kinesis, KMS, Lambda, MSK, OpenSearch, Pipes, Pricing, RDS, Resource Groups Tagging,
Route53, S3, Scheduler, Secrets Manager, SES, SNS, SQS, SSM, Step Functions, Textract,
Transcribe, Transfer

## Key Agent Instructions File
`AGENT.md` — canonical instructions for AI coding agents in this repository.
