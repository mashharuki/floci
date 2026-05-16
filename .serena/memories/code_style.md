# Floci Code Style & Conventions

## Language & Tooling
- Java 25
- Quarkus CDI: `@ApplicationScoped`, `@Inject`
- No Lombok (use standard Java records/POJOs)
- Jackson for JSON serialization
- JUnit 5 + RestAssured for tests

## Naming Conventions
- Classes: `PascalCase`
- Methods/fields: `camelCase`
- Constants: `UPPER_SNAKE_CASE`
- Test classes: `*IntegrationTest.java` or `*ServiceTest.java`
- XML namespace constants in `AwsNamespaces`

## File / Package Structure
- One service per package under `services/<svc>/`
- Controller, Service, and `model/` subpackage per service
- Copy an existing similar service pattern before creating new ones

## Design Principles
1. Preserve AWS protocol compatibility above all else
2. Match AWS SDK and CLI behavior
3. Reuse existing Floci patterns (don't reinvent)
4. Prefer correctness over convenience
5. Keep changes narrow and testable — no broad refactors unless explicitly required

## Anti-Patterns to Avoid
- Custom (non-AWS) endpoint shapes
- Changing request/response formats for convenience
- Instantiating storage implementations directly (use `StorageFactory`)
- Using regex for XML parsing (use `XmlParser`)
- Adding `Co-Authored-By` AI attribution in commits
