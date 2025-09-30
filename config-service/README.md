# Config Service (Spring Cloud Config Server)

This is a Spring Cloud Config Server for centralizing configuration.

## Run

- Java 17 + Maven required.

```bash
mvn spring-boot:run
# Server on http://localhost:8888
```

## Backends

Two options are pre-wired (choose one):

1) **Native filesystem** (active by default via `bootstrap.yml`):
   - Edit `bootstrap.yml` to point `search-locations` to the parent folder of your config repo.
   - Example replacement for `#{CONFIG_REPO_ABS_PARENT}` with your absolute path.

2) **Git backend**:
   - Switch `spring.profiles.active` to default (remove `native`) and set `spring.cloud.config.server.git.uri` in `application.yml`.
   - Uses `search-paths: configs` so files are expected under `config-repo/configs/`.

## Test URLs

```
http://localhost:8888/flight-search-service/default
http://localhost:8888/flight-search-service/dev
http://localhost:8888/flight-search-service/prod
```
