from golangci/golangci-lint:v2.6.2 as golint
from golang:1.25.4

COPY --from=golint /usr/bin/golangci-lint /usr/bin/golangci-lint

# set up user to avoid permissions issues with git repo mounted into container
ARG GID
ENV GID=${GID:-0}
ARG UID
ENV UID=${UID:-0}
run addgroup --gid ${GID} user && adduser --disabled-password --gid ${GID} --uid ${UID} --gecos "" user
user user

workdir /home/user
ENV HOME=/home/user
ENV NVM_DIR=/home/user/.nvm

run curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash && \. "$HOME/.nvm/nvm.sh" && nvm install 24 && npm install --global corepack@latest npm @go-task/cli && corepack enable pnpm

cmd /bin/bash
