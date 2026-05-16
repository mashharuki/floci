# Floci Suggested Commands

## Build & Run
```bash
./mvnw quarkus:dev                    # hot reload dev mode on port 4566
./mvnw clean package                  # full build
./mvnw clean package -DskipTests      # build skipping tests
```

## Testing
```bash
./mvnw test                                          # all tests
./mvnw test -Dtest=SsmIntegrationTest                # single test class
./mvnw test -Dtest=SsmIntegrationTest#putParameter   # single test method
```

## Git / Utilities (Linux)
```bash
git checkout -b feature/my-feature   # create feature branch
git log --oneline                    # compact log
find src -name "*.java"              # find Java files
grep -r "ClassName" src/             # search in source
```

## Docker
```bash
docker compose up                    # start Floci via docker-compose.yml
```
