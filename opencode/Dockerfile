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

EXPOSE 4096

CMD ["opencode", "web", "--port", "4096", "--hostname", "0.0.0.0"]
