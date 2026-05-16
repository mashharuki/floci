# Floci Architecture & Conventions

## Three-Layer Architecture
1. **Controller / Handler** — parses AWS protocol input, produces AWS-compatible responses (thin layer)
2. **Service** (`@ApplicationScoped`) — business logic; throws `AwsException`
3. **Model** — domain POJOs

## Package Layout
```
io.github.hectorvent.floci.config
io.github.hectorvent.floci.core.common     ← shared infrastructure
io.github.hectorvent.floci.core.storage    ← storage backends
io.github.hectorvent.floci.lifecycle
io.github.hectorvent.floci.services.<svc>  ← per-service packages
```

Typical service package:
```
services/<svc>/
  *Controller.java
  *Service.java
  model/
```

## Core Infrastructure Classes
- `EmulatorConfig` — all configuration
- `ServiceRegistry` — service metadata / enablement
- `StorageFactory` — always use this; never instantiate storage directly
- `AwsQueryController` — base for Query protocol services
- `AwsJson11Controller` — base for JSON 1.1 protocol services
- `AwsException` + `AwsExceptionMapper` — error handling
- `EmulatorLifecycle` — startup/shutdown hooks
- `XmlBuilder` / `XmlParser` — XML construction/parsing
- `AwsNamespaces` — XML namespace constants
- `ResolvedServiceCatalog` + `ServiceDescriptor` — service catalog

## AWS Protocol Mapping
| Protocol  | Services                                              | Request          | Response | Implementation       |
|-----------|-------------------------------------------------------|------------------|----------|----------------------|
| Query     | SQS, SNS, IAM, STS, RDS, ElastiCache, CloudFormation, CloudWatch Metrics | form-encoded POST + `Action` | XML | `AwsQueryController` |
| JSON 1.1  | SSM, EventBridge, CW Logs, Kinesis, KMS, Cognito, Secrets Manager, ACM | POST + `X-Amz-Target` | JSON | `AwsJson11Controller` |
| REST JSON | Lambda, API Gateway, SES V2                          | REST paths       | JSON     | JAX-RS               |
| REST XML  | S3                                                   | REST paths       | XML      | JAX-RS               |
| TCP       | ElastiCache, RDS                                     | raw protocol     | native   | proxies              |

## Storage Modes
`memory`, `persistent`, `hybrid`, `wal`

When adding storage: update `EmulatorConfig`, `application.yml`, test `application.yml`, `StorageFactory`, lifecycle hooks.

## Configuration
- Lives under `floci.*`
- Environment variables follow `FLOCI_*` convention
- `application.yml` is the source of truth for runtime behavior

## XML / JSON Rules
- Use `XmlBuilder` for XML; `XmlParser` for parsing (no regex)
- Use `AwsNamespaces` constants
- JSON errors must follow AWS error structures

## Adding a New Service (checklist)
1. Create package under `services/<service>/`
2. Add Controller (correct protocol)
3. Add Service (`@ApplicationScoped`) + model POJOs
4. Add config entries in `EmulatorConfig` and `application.yml`
5. Register `ServiceDescriptor` in `ResolvedServiceCatalog`
6. Wire controller/handler dispatch
7. Add integration tests (`*IntegrationTest.java`)
