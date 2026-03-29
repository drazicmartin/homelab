FROM node:slim

RUN apt update && apt install -y --no-install-recommends \
    # Core utilities needed for setup and the curl install script
    wget \
    vim \
    ca-certificates \
    curl \
    unzip \
    gnupg \
    sudo \
    git

ARG OPENCODE_VERSION=latest
# install opencode globally
RUN npm install -g opencode-ai@${OPENCODE_VERSION}

ARG REPO_URL
ARG REPO_BRANCH=main
ARG GITHUB_TOKEN

RUN echo "value is $GITHUB_TOKEN"

RUN mkdir /workspace
RUN if [ -n "$REPO_URL" ]; then \
      cd /workspace && \
      git clone --branch ${REPO_BRANCH} https://${GITHUB_TOKEN}@${REPO_URL#https://}; \
    fi

EXPOSE 4096

CMD ["opencode", "web", "--port", "4096", "--hostname", "0.0.0.0", "--log-level", "DEBUG"]
