# Spring Cloud Config Server Bundle

This bundle contains:
- `config-service/` → Spring Cloud Config Server (Java 17, Spring Boot 3, Spring Cloud 2023.x)
- `config-repo/configs/` → configuration files for `flight-search-service` (default, dev, prod)

## Quick Start (Native Filesystem)

1) Determine the absolute path to `config-repo/` on your machine.
2) Edit `config-service/src/main/resources/bootstrap.yml` and replace `#{CONFIG_REPO_ABS_PARENT}` with that absolute path.
   - It should point to the **parent** of `config-repo` (because `search-locations` will read that directory).
3) Run the server:
   ```
   cd config-service
   mvn spring-boot:run
   ```
4) Test in a browser or curl:
   ```
   curl http://localhost:8888/flight-search-service/default
   curl http://localhost:8888/flight-search-service/dev
   curl http://localhost:8888/flight-search-service/prod
   ```

## Alternative (Git Backend)

1) Initialize a Git repo in `config-repo` and commit.
2) Switch `spring.profiles.active` (remove `native`) so `application.yml` is used.
3) Set `spring.cloud.config.server.git.uri` to the Git URL of your repo in `config-service/src/main/resources/application.yml`.
   - Keep `search-paths: configs` (files are under `config-repo/configs/`).

## Client Reminder

A Spring Boot client must have:
```yaml
spring:
  application:
    name: flight-search-service
  profiles:
    active: dev  # or default/prod
  cloud:
    config:
      uri: http://localhost:8888
```
This leverages Convention over Configuration: `{application}-{profile}.yml` is resolved automatically.
