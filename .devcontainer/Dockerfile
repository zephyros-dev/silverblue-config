# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.205.2/containers/debian/.devcontainer/base.Dockerfile

# [Choice] Debian version (use bullseye or stretch on local arm64/Apple Silicon): bullseye, buster, stretch
ARG VARIANT="buster"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}
# Base packages for setup
ARG DEBIAN_FRONTEND=noninteractive
RUN apt update \
    && apt install -y --no-install-recommends \
    curl \
    fish \
    python3-pip \
    sshpass \
    tmux \
    unzip \
    whois \
    && rm -rf /var/lib/apt/lists/* \
    && apt autoremove -y \
    && apt clean -y
# Ansible
ARG ANSIBLE_VERSION="5.0.1"
ARG ANSIBLE_LINT_VERSION="5.3.0"
RUN pip install --no-cache-dir ansible==${ANSIBLE_VERSION} ansible-lint==${ANSIBLE_LINT_VERSION}
# age
RUN apt update \
    && apt install -y --no-install-recommends \
    age \
    && rm -rf /var/lib/apt/lists/* \
    && apt autoremove -y \
    && apt clean -y
# sops
ARG SOPS_VERSION="3.7.1"
RUN curl -L -o sops.deb "https://github.com/mozilla/sops/releases/download/v${SOPS_VERSION}/sops_${SOPS_VERSION}_amd64.deb" \
    && apt install -y --no-install-recommends ./sops.deb \
    && git config --global diff.sopsdiffer.textconv "sops -d" \
    && rm -r sops.deb \
    && rm -rf /var/lib/apt/lists/* \
    && apt autoremove -y \
    && apt clean -y