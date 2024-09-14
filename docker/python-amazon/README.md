## Python Amazon 3.9.19 docker image

This repository houses a Docker image equipped with Python under amazon linux architecture, designed to be versatile
across different pipeline solutions.
This image adheres to the [3musketeers](https://3musketeersdev.netlify.app) pattern, ensuring compatibility and
promoting a standardized approach to tool usage.

## How to use this image

Given a docker compose file in the root of your project

docker-compose.yml

```yaml
version: '3'

services:
  python-amazon:
    image: ghcr.io/mulecode/tool-set-python-amazon:latest
    working_dir: /opt/app
    volumes:
      - .:/opt/app
    environment:
      - AWS_REGION=us-east-1
      - AWS_DEFAULT_REGION=us-east-1
      - AWS_ACCESS_KEY_ID=dummy-access-key
      - AWS_SECRET_ACCESS_KEY=dummy-access-key-secret
```

Makefile

```makefile
COMPOSE_RUN_PYTHON = docker-compose run --no-deps --rm python-amazon
COMPOSE_RUN_PYTHON_MAKE = docker-compose run --no-deps --entrypoint "make" --rm python-amazon

.PHONY: version
version: ## Python version with docker run pattern
	$(COMPOSE_RUN_PYTHON) --version

.PHONY: version_make
version_make: ## Python version with make pattern
	$(COMPOSE_RUN_PYTHON_MAKE) _version_make

_version_make:
	@echo "Python version with make pattern"
	@python3 --version
```

## Docker run commands

Python version

```bash
docker run -it --rm ghcr.io/mulecode/tool-set-python-amazon:latest --version
```


