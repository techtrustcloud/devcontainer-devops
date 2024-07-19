FROM mcr.microsoft.com/devcontainers/base:debian

RUN apt-get update && \
    apt-get install -y xz-utils bash-completion tmux dnsutils vim
ADD .config /home/vscode/.config