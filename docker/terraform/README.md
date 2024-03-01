## Terraform 1.7.4 docker image

This repository houses a Docker image equipped with Terraform, designed to be versatile across different pipeline
solutions.
This image adheres to the [3musketeers](https://3musketeersdev.netlify.app) pattern, ensuring compatibility and
promoting a standardized approach to tool usage.

## How to use this image

Given a docker compose file in the root of your project

docker-compose.yml

```yaml
version: '3'

services:
  terraform:
    image: ghcr.io/mulecode/tool-set-terraform:latest
    working_dir: /opt/app
    volumes:
      - .:/opt/app
      - ~/.ssh:/root/.ssh:ro
    environment:
      - AWS_REGION
      - AWS_ACCESS_KEY_ID
      - AWS_SECRET_ACCESS_KEY
      - AWS_SESSION_TOKEN
      - SSH_AUTH_SOCK
```

Makefile

```makefile
COMPOSE_RUN_TERRAFORM = docker-compose run --no-deps --rm terraform
COMPOSE_RUN_TERRAFORM_MAKE = docker-compose run --no-deps --entrypoint "make" --rm terraform

.PHONY: version
version: ## Terraform version with docker run pattern
	$(COMPOSE_RUN_TERRAFORM) --version

.PHONY: version_make
version_make: ## Terraform version with make pattern
	$(COMPOSE_RUN_TERRAFORM_MAKE) _version_make

_version_make:
	@echo "Terraform version with make pattern"
	@terraform --version
```
