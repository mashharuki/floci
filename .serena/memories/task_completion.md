# Floci Task Completion Checklist

After completing a coding task in Floci, verify:

## Code Quality
- [ ] Controllers are thin; business logic is in Services
- [ ] `AwsException` / `AwsExceptionMapper` used for errors (not raw HTTP exceptions)
- [ ] Storage accessed only via `StorageFactory`
- [ ] XML responses use `XmlBuilder` + `AwsNamespaces`
- [ ] JSON errors follow AWS error structures

## AWS Compatibility
- [ ] AWS wire protocol is preserved (Query/JSON 1.1/REST JSON/REST XML/TCP)
- [ ] Response shape matches real AWS
- [ ] Request parsing matches real AWS SDK expectations

## Configuration (if changed)
- [ ] `EmulatorConfig` updated
- [ ] `src/main/resources/application.yml` updated
- [ ] `src/test/resources/application.yml` updated if needed
- [ ] Docs updated if user-facing

## Testing
```bash
./mvnw test
```
- [ ] Add / update `*IntegrationTest.java` for compatibility-sensitive behavior
- [ ] Prefer AWS SDK-based tests over raw HTTP

## Commit Message (Conventional Commits)
- `feat:` new API action or service → minor bump
- `fix:` bug fix / AWS compat fix → patch bump
- `perf:` performance improvement → patch bump
- `docs:` documentation only → no bump
- `chore:` build/CI/deps → no bump
- `BREAKING CHANGE:` footer or `!` → major bump
- Do NOT add `Co-Authored-By` trailers for AI tools
