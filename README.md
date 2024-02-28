# Google Cloud Run with Pulumi

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/usrbinkat/pulumi-iac-gcp-cloud-run?quickstart=1&devcontainer_path=.devcontainer%2Fextra%2Fdevcontainer.json)

[![License](https://img.shields.io/github/license/usrbinkat/iac-mesh-pac)]() [![Pulumi](https://img.shields.io/badge/pulumi-v3.107.0-blueviolet)](https://www.pulumi.com/docs/get-started/install/)

## Powered by Pulumi + Devcontainers

The Pulumi [Devcontainer](https://code.visualstudio.com/docs/devcontainers/containers) is designed with deep [VS Code](https://code.visualstudio.com) and [Github Codespaces](https://github.com/features/codespaces) integration to streamline common Pulumi IaC development environments.

# Getting Started

- [Overview](#overview)
  - [Objectives](#objectives)
  - [Architecture](#architecture)
- [Dev Environment](#dev-environment)
  - [Github Codespaces](#github-codespaces)
  - [VSCode Devcontainer](#vscode-devcontainer)
  - [Local Environment](#local-environment)
- [Setup](#setup)
- [Deploy](#deploy)
- [Clean Up](#clean-up)
- [Reference](#reference)

## Overview

This document describes building and deploying the microservices demo application(`Online Boutique`) to Cloud Run.

### Objectives

- Minimize code changes.
- Ensure the internal microservices are private and keep the network traffic inside the Google network (serverless VPC connectors will be used).
- Redis cache will be deployed to [Memorystore(Redis)](https://cloud.google.com/memorystore/docs/redis).
- Use Infrastructure-as-code([Pulumi](https://www.pulumi.com/)) to deploy the solution.

### Architecture

![Architecture](./microservices-cloudrun-arch.svg)

## Dev Environment

### Github Codespaces

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/pulumi/devcontainer?quickstart=1)

Codespaces is the easiest way to get started quickly. Simply click the button above to open this repository in a new Codespace and then follow the [First time setup](#first-time-setup) instructions below.

### VSCode Devcontainer

To use this repo with VSCode in a local Devcontainer with Docker, clone this repository and open in VSCode, follow prompts on screen to open in the Devcontainer.

To use the Dev Container in VS Code, you will need to install the [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension, and follow the [official tutorial here](https://code.visualstudio.com/docs/devcontainers/tutorial) to begin.

### Local Environment

Alternatively, use this IaC repository locally as is and maintain your dependencies according to your own preferences and requirements.

Once your IaC and dependencies are met, proceed to [Setup](#setup).

## Setup

1. Pulumi Login

```bash
pulumi login
```

2. Create a new stack

```bash
pulumi stack select --create --stack workshop-cloudrun
```

3. Install NPM dependencies

```bash
npm install
```

4. Google Cloud login

```bash
# Setup gcloud cli
gcloud init

# Configure gcloud cli
# Set GCP project ID:
# - eg: export PROJECT_ID=<YOUR GCP PROJECT ID>
export PROJECT_ID='pulumi-devrel'
gcloud config set project $PROJECT_ID
gcloud auth application-default login
gcloud auth configure-docker
```

5. Pulumi configure stack `gcp:project` value

```
pulumi config set gcp:project $PROJECT_ID
```

## Deploy

```
pulumi up -y
```

By default, the service deployments will use the container images listed in the [release/kubernetes-manifests.yaml](./release/kubernetes-manifests.yaml) file.

If you want to build the container images from the source code, you can set the flag `build_image_from_src` to true using the following command:

```
pulumi config set build_image_from_src true
```

**Note:** This step will **NOT** work in CloudShell since CloudShell does not have sufficient disk space to build all the container images.

## Clean up

If you don't want to delete the whole project, run the following command to delete the resources:

```
pulumi destroy -y
```

---

# Reference

Demo code based on original work by [@xiangshen-dk](https://github.com/xiangshen-dk) from [github.com/shenxiang-demo/microservices-demo/.../serverless/pulumi](https://github.com/shenxiang-demo/microservices-demo/tree/pulumi-cloudrun-one-ilb/serverless/pulumi)
