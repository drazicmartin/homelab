FROM node:slim

RUN apt-get update && apt-get install -y --no-install-recommends \
  wget \
  curl \
  bash \
  ca-certificates \
  git \
  less \
  openssh-client \
  python3 \
  gnupg \
  xdg-utils \
  && rm -rf /var/lib/apt/lists/*

ARG OPENCODE_VERSION=latest
RUN npm install -g opencode-ai@${OPENCODE_VERSION}

RUN mkdir /workspace

# OpenCode config with GitHub token baked in
RUN mkdir -p /root/.config/opencode
# COPY opencode.json /root/.config/opencode/opencode.json

EXPOSE 4096
CMD ["opencode", "web", "--port", "4096", "--hostname", "0.0.0.0", "--log-level", "DEBUG", "--cors", "https://oc.summer-games.fr"]
