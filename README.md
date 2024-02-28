# Google Cloud Run with Pulumi

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/usrbinkat/pulumi-iac-gcp-cloud-run?quickstart=1&devcontainer_path=.devcontainer%2Fextra%2Fdevcontainer.json)

[![License](https://img.shields.io/github/license/usrbinkat/iac-mesh-pac)]() [![Pulumi](https://img.shields.io/badge/pulumi-v3.107.0-blueviolet)](https://www.pulumi.com/docs/get-started/install/)

## Powered by Pulumi + Devcontainers

The Pulumi [Devcontainer](https://code.visualstudio.com/docs/devcontainers/containers) is designed with deep [VS Code](https://code.visualstudio.com) and [Github Codespaces](https://github.com/features/codespaces) integration to streamline common Pulumi IaC development environments.

# Getting Started

- [Pulumi Dev Container](#pulumi-dev-container)
- [Getting Started](#getting-started)
- [Github CodeSpaces](#github-codespaces)
  - [First time setup](#first-time-setup)
- [VS Code Dev Container](#vs-code-dev-container)
- [Git Submodule](#git-submodule)

# Dev Environment

## Github Codespaces

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/pulumi/devcontainer?quickstart=1)

Codespaces is the easiest way to get started quickly. Simply click the button above to open this repository in a new Codespace and then follow the [First time setup](#first-time-setup) instructions below.

## VSCode Devcontainer

To use this repo with VSCode in a local Devcontainer with Docker, clone this repository and open in VSCode, follow prompts on screen to open in the Devcontainer.

To use the Dev Container in VS Code, you will need to install the [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension, and follow the [official tutorial here](https://code.visualstudio.com/docs/devcontainers/tutorial) to begin.

## Local Environment

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

# Git Submodule

The pulumi Dev Container repository can be added as a submodule to an existing project to provide an easy and consistent development environment that is maintained upstream.

To add this repository as a submodule to your project, run the following commands:

```bash
git submodule add https://github.com/pulumi/devcontainer .github/devcontainer
git submodule update --init --recursive .github/devcontainer
mkdir -p .devcontainer
rsync -av .github/devcontainer/devcontainer/* .devcontainer
```

To update the devcontainer submodule in consuming repos:

```bash
git submodule update --remote --merge .github/devcontainer
rsync -av .github/devcontainer/devcontainer/* .devcontainer
```

After the submodule is added, you can open your project in VS Code and it will automatically detect the Dev Container configuration and prompt you to open the project in a container, or you can open the project in Github CodeSpaces.

# References

Demo code based on original work by [@xiangshen-dk](https://github.com/xiangshen-dk) from [github.com/shenxiang-demo/microservices-demo/.../serverless/pulumi](https://github.com/shenxiang-demo/microservices-demo/tree/pulumi-cloudrun-one-ilb/serverless/pulumi)
