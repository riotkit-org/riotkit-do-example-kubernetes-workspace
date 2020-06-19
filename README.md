K8S Workspace
=============

Create Kubernetes/OKD deployments without duplicating the code. 
Use JINJA2 templating to share blocks between YAMLS, that's EASY!

Given you have an application "hello-world", create a common file, parametrize it, then create environments eg. env, dev, prod with just variables to fill up.

```yaml
{%- set APP_NAME = "hello-dev" -%}
{%- set APP_NAMESPACE = "default" -%}
{%- set APP_DOCKER_IMAGE = "nginx:1.19" -%}
{%- set APP_URL = "hello-dev.local" -%}

{% extends "templates/spring-boot-common/common-deployment.yaml.j2" %}
```

Usage locally or at CI
----------------------

```bash
rkd :k8s:yaml hello-world --env=hello-dev
rkd :k8s:apply hello-world --env=hello-dev

# or with a multiple tasks combined
rkd @ hello-world --env=hello-dev :k8s:yaml :k8s:apply

# combined with a dry run
rkd @ hello-world --env=hello-dev :k8s:yaml :k8s:apply --dry-run
```
