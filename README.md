# Products

Java 21 / Spring Boot 4.1.2, JdbcClient and explicit SQL, Thymeleaf, Flyway and PostgreSQL/pgvector. No ORM or SPA.

```bash
bash mvnw package
docker build --platform linux/amd64 -t products:w1 .
docker run --rm -p 127.0.0.1:8080:8080 products:w1 --spring.profiles.active=inspect
```

Inspect mode exposes startup information and health without Azure. The real `azure` profile requires `APP_CONFIG_ENDPOINT` / `APP_CONFIG_LABEL`, workload identity, mounted TLS files in `/tls`, and the workshop's provisioned dependencies. Settings and Key Vault secrets load at startup.

Tests: `bash mvnw test`. Set `TEST_DATABASE_URL` to a disposable PostgreSQL database with pgvector to run the four database/HTTP integration tests. Without it those integration tests are skipped. The workshop's `verify-local.sh` prepares the fixture.

Products commits the product before blob upload. Questions use a persistent outbox; correlated replies and browser polling persist in PostgreSQL. Upload/chat writes require CSRF/session state.

Deployment, sample manuals and the full walkthrough: https://github.com/tuba-labs/ai200/tree/main/workshop
