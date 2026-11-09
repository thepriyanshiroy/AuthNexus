# AuthGateway: rules for any AI agent working in this repo

## Project

AuthGateway is a reusable authentication, authorization and API gateway platform.
This is a learning and portfolio project. The owner must be able to explain every line in an interview.

## Stack

Java 21, Spring Boot 4.1.x, Spring Security 7, Maven (use the mvnw wrapper), PostgreSQL 17,
Flyway, Spring Data JPA (Hibernate), Redis 7, JUnit 5, Mockito, Testcontainers.

## Repository layout

- services/auth-service (port 9000): identity, passwords, tokens. Package com.authgateway.auth.
- services/api-gateway (port 8080): routing only.
- services/sample-orders-service (port 8081): demo business service.
- deploy/docker-compose.yml: PostgreSQL, Redis, Mailpit (dev inbox at http://localhost:8025, SMTP 1025).
- docs/: documentation and docs/adr for decision records.

## auth-service packages (organise by feature)

config, identity, token, notification, login, web.
Class suffixes: Controller, Service, Repository, Request/Response for DTO records, Properties for config.

## Working rules

1. Change only what the current task names. Do not touch other services. Do not refactor working code.
2. Add a dependency only when the task lists it. Mention every dependency you add.
3. Never hardcode a secret. Secrets come from environment variables. .env is never committed.
4. Never log or print a password, a password hash, a one-time token, an OTP or a full email address.
   Log event names and user ids. Records or classes that hold secrets must override toString().
5. Authentication failures return generic messages. Never reveal whether an account exists.
6. Default deny: anything not explicitly permitted needs authentication.
7. Flyway owns the schema. Never edit a migration that already exists; add a new one.
   Hibernate runs with ddl-auto=validate.
8. Spring Boot 4 renamed starters, modules and test packages. If a class or import is not found,
   look it up in the Spring Boot 4.0/4.1 migration guide and reference docs. Do not guess from
   Boot 3 tutorials. Do not downgrade Spring Boot.
9. Do not write your own cryptography. Use SecureRandom, MessageDigest and Spring Security's encoders.
10. Comments explain WHY (the security or design reason), not what a line does.
11. Write tests with the code. Use Testcontainers PostgreSQL for database tests, never H2 and never
    the dev database. Use @MockitoBean, not @MockBean.
12. Run the build and the tests yourself (./mvnw test in the service folder; mvnw.cmd on Windows).
    Never claim a test passed unless you ran it and saw it pass.

## Final report (end every task with this)

1. Files created or changed (paths).
2. Commands you ran and the real result line of each.
3. Anything you were unsure about or chose differently from the task, and why.
4. A plain-English explanation in 5 bullets that the owner could say out loud in an interview.
