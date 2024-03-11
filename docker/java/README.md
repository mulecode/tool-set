## Java 21 OpenJDK docker image

This repository houses a Docker image equipped with OpenJDK 21 under alpine linux architecture, designed to be versatile
across different pipeline solutions.
This image adheres to the [3musketeers](https://3musketeersdev.netlify.app) pattern, ensuring compatibility and
promoting a standardized approach to tool usage.

## How to use this image

Given a docker compose file in the root of your project

docker-compose.yml

```yaml
version: '3'

services:
  java:
    image: ghcr.io/mulecode/tool-set-java:latest
    working_dir: /opt/app
    volumes:
      - .:/opt/app
```

Makefile

```makefile
COMPOSE_RUN_JAVA = docker-compose run --no-deps --rm java
COMPOSE_RUN_MVN = docker-compose run --no-deps --entrypoint "mvn" --rm java
COMPOSE_RUN_JAVA_MAKE = docker-compose run --no-deps --entrypoint "make" --rm java

.PHONY: version
version: ## Java version with docker run pattern
	$(COMPOSE_RUN_JAVA) --version

.PHONY: mvn_version
mvn_version: ## Maven version with docker run pattern
	$(COMPOSE_RUN_MVN) --version

.PHONY: version_make
version_make: ## Java version with make pattern
	$(COMPOSE_RUN_JAVA_MAKE) _version_make

_version_make:
	@echo "Java version with make pattern"
	@java --version
```

## Docker run commands

Java version

```bash
docker run -it --rm ghcr.io/mulecode/tool-set-java:latest --version
```

Maven version

```bash
docker run -it --entrypoint "mvn" --rm ghcr.io/mulecode/tool-set-java:latest --version
```
