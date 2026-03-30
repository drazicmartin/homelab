FROM node:slim

RUN apt update && apt install -y --no-install-recommends \
    wget vim ca-certificates curl unzip gnupg sudo git \
    && rm -rf /var/lib/apt/lists/*

ARG OPENCODE_VERSION=latest
RUN npm install -g opencode-ai@${OPENCODE_VERSION}

ARG REPO_URL
ARG REPO_BRANCH=main
ARG GITHUB_TOKEN

ARG GIT_USER_NAME="Drazic OpenCode Agent"
ARG GIT_USER_EMAIL="drazic@opencode.fr"
RUN git config --global user.name "${GIT_USER_NAME}" && \
    git config --global user.email "${GIT_USER_EMAIL}"

RUN git config --global credential.helper store

RUN mkdir /workspace
RUN if [ -n "$REPO_URL" ]; then \
      cd /workspace && \
      git clone --branch ${REPO_BRANCH} https://${GITHUB_TOKEN}@${REPO_URL#https://}; \
      # Store credentials for future pushes
      # echo "https://${GITHUB_TOKEN}:x-oauth-basic@github.com" \
      #  > /root/.git-credentials; \
    fi

# OpenCode config with GitHub token baked in
RUN mkdir -p /root/.config/opencode
COPY opencode.json /root/.config/opencode/opencode.json

EXPOSE 4096
CMD ["opencode", "web", "--port", "4096", "--hostname", "0.0.0.0", "--log-level", "DEBUG"]
