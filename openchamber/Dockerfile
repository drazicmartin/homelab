FROM oven/bun:1

# Install required dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
  curl \
  bash \
  ca-certificates \
  git \
  less \
  openssh-client \
  python3 \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /home/openchamber

ENV NODE_ENV=production
ARG OPENCHAMBER_CONFIG_DIR=/home/openchamber/.config/openchamber
ENV OPENCHAMBER_CONFIG_DIR=${OPENCHAMBER_CONFIG_DIR}
ARG OPENCODE_CONFIG_DIR=/home/openchamber/.config/opencode
ENV OPENCODE_CONFIG_DIR=${OPENCODE_CONFIG_DIR}
ENV HOME=/home/openchamber

ARG OPENCODE_VERSION=latest
# Install opencode
RUN bun add -g opencode-ai@${OPENCODE_VERSION}

ARG OPENCHAMBER_VERSION=latest
# Install OpenChamber
RUN bun add -g @openchamber/web@${OPENCHAMBER_VERSION}

# Install oh-my-opencode and configure it
RUN bunx oh-my-opencode install --no-tui --claude=no --openai=no --gemini=no --copilot=no --opencode-zen=no --zai-coding-plan=no --kimi-for-coding=no --skip-auth

# Expose default port (adjust if needed)
EXPOSE 8080

ENV PATH="/home/openchamber/.bun/bin:${PATH}"

CMD [ "openchamber", "serve", "--foreground", "--port", "8080" ]
