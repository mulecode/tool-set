## OpenAPI docker image

This repository houses a Docker image equipped with OpenAPI tools under amazon linux architecture, designed to be
versatile
across different pipeline solutions.
This image adheres to the [3musketeers](https://3musketeersdev.netlify.app) pattern, ensuring compatibility and
promoting a standardized approach to tool usage.

## How to use this image

Given a docker compose file in the root of your project

docker-compose.yml

```yaml
version: '3'

services:
  openapi:
    image: ghcr.io/mulecode/tool-set-openapi:test
    working_dir: /opt/app
    volumes:
      - .:/opt/app
```

Makefile

```makefile
$(VERBOSE).SILENT:
.DEFAULT_GOAL := help

COMPOSE_RUN_OPENAPI_MAKE = docker-compose run --entrypoint "make" --no-deps --rm openapi

MODULE_NAME := $(notdir $(CURDIR))
MODULE_PATH := /opt/app/modules/$(MODULE_NAME)
SRC_PATH := /opt/app/modules/$(MODULE_NAME)/src
YAML_FILES := $(wildcard $(SRC_PATH)/*.yaml)

.PHONY: lint
lint: ## Validate OpenAPIs files
	$(COMPOSE_RUN_OPENAPI_MAKE) -C $(MODULE_PATH) _lint

_lint:
	for ITEM in $(YAML_FILES); do \
		echo "Lint $$ITEM"; \
		redocly lint "$$ITEM"; \
	done

.PHONY: bundle
bundle: ## bundle OpenAPIs files
	$(COMPOSE_RUN_OPENAPI_MAKE) -C $(MODULE_PATH) _bundle

_bundle:
	for ITEM in $(YAML_FILES); do \
		echo "bundling $$ITEM"; \
		FILE_NAME=$$(basename $$ITEM); \
		redocly bundle "$$ITEM" --output "./out/$$FILE_NAME"; \
	done

.PHONY: build-docs
build-docs: ## Build documentation of API's
	$(COMPOSE_RUN_OPENAPI_MAKE) -C $(MODULE_PATH) _build-docs

_build-docs:
	for ITEM in $(YAML_FILES); do \
		echo "build-docs $$ITEM"; \
		FILE_NAME=$$(basename $$ITEM .yaml); \
		redocly build-docs "$$ITEM" --output "./out/$$FILE_NAME.html"; \
	done
```

Folder structure

```text
project/
│
├── modules/
│   └── openapi/
│       ├── src/
│       │   ├── components/
│       │   │   ├── schemas/
│       │   │   │   ├── ObjectSchema1.yaml
│       │   │   │   └── ObjectSchema2.yaml
│       │   └── service-v1-api.yaml
│       │   redocly.yaml
│       └── Makefile  
│
└── docker-compose.yml
```
