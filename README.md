DevOps CLI Development Container

This development container provides a pre-configured environment for DevOps development with essential tools and utilities.

Prerequisites

	•	Docker installed on your machine
	•	Visual Studio Code with the Remote - Containers extension

Configuration

The development container is configured with a devcontainer.json file and a corresponding Dockerfile. The following instructions will guide you through setting up the environment.

Files Structure
```
/path/to/your-project
├── .devcontainer
│   ├── devcontainer.json
│   └── Dockerfile
└── .config
    └── (config files)
```
Dockerfile

The Dockerfile used for building the development container image:
```
# Dockerfile
FROM mcr.microsoft.com/devcontainers/base:debian

RUN apt-get update && \
    apt-get install -y xz-utils bash-completion tmux dnsutils vim

ADD .config /home/vscode/.config
```
devcontainer.json

The devcontainer.json file defines the configuration of the development container:

```json
{
    "name": "DevOps CLI",
    "build": {
        "dockerfile": "Dockerfile"
    },
    "runArgs": [
		"--dns=8.8.8.8",
		"--dns=8.8.4.4"
    ],
    "features": {
        "ghcr.io/devcontainers/features/go:1": {
            "version": "latest",
            "username": "root"
        },
        "ghcr.io/devcontainers/features/kubectl-helm-minikube:1": {
            "version": "latest",
            "helm": "none",
            "minikube": "none"
        },
        "ghcr.io/devcontainers/features/docker-in-docker:2": {},
        "ghcr.io/devcontainers/features/sshd:1": {},
        "ghcr.io/devcontainers/features/python:1": {},
        "./local-features/kubectl-kind": {}
    },
    "mounts": [
        {
            "source": "/home/user/.ssh",
            "target": "/home/vscode/.ssh",
            "type": "bind"
        },
        {
            "source": "/home/user/Repos",
            "target": "/workspaces",
            "type": "bind"
        }
    ]
}
```
Steps to Use the Development Container

1.	Clone your repository to your local machine:
```bash
git clone https://github.com/your-repo/your-project.git
cd your-project
```
2.	Open the project in Visual Studio Code:
```bash
code .
``` 

3.	Open the Command Palette in Visual Studio Code by pressing Ctrl+Shift+P (or Cmd+Shift+P on macOS).
4.	Select Remote-Containers: Reopen in Container. This will build and start the container based on the configuration provided in the devcontainer.json file.

1.	Open a terminal within the development container.
2.	Check settings by running:
```bash

#DNS
cat /etc/resolv.conf 
#Path 
ls /home/vscode/.ssh
#And 
ls /workspaces 
```

Additional Information

For more details about configuring development containers, refer to the following resources:

	•	[Development Containers Specification](https://containers.dev/implementors/spec/)
	•	[Base Debian Image README](https://github.com/devcontainers/images/tree/main/src/base-debian)

This development environment is designed to streamline the development process and ensure consistency across different development setups. Feel free to customize the devcontainer.json file to fit your specific needs.
