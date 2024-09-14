## Python 3.12 Playwright docker image

This repository houses a Docker image equipped with Python 3.12 and Playwright under Ubuntu linux architecture, 
designed to be versatile across different pipeline solutions.

This image adheres to the [3musketeers](https://3musketeersdev.netlify.app) pattern, ensuring compatibility and
promoting a standardized approach to tool usage.

## How to use this image

Given a docker compose file in the root of your project

docker-compose.yml

```yaml
version: '3'

services:
  python-playwright:
    image: ghcr.io/mulecode/tool-set-python-playwright:latest
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
COMPOSE_RUN_ALPINE = docker-compose run --no-deps --rm python-playwright
COMPOSE_RUN_ALPINE_MAKE = docker-compose run --no-deps --entrypoint "make" --rm python-playwright

.PHONY: version
version: ## Prints current version of python
	$(COMPOSE_RUN_ALPINE)
	
.PHONY: version_make
version_make: ## Version with make pattern
	$(COMPOSE_RUN_ALPINE_MAKE) -C $(MODULE_PATH) _version_make

_version_make:
	@python3 --version
```

## Docker run commands

Python version

```bash
docker run -it --rm ghcr.io/mulecode/tool-set-alpine-python:latest --version
```


