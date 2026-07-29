# Dockerfile to be used by Codespaces / devcontainer
# Based on Microsoft's base container for devcontainers
FROM mcr.microsoft.com/devcontainers/base:0-ubuntu-22.04

# Install dependencies and Google Chrome
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        gnupg \
        wget \
        apt-transport-https \
        fonts-liberation \
        libappindicator3-1 \
        libasound2 \
        libatk-bridge2.0-0 \
        libatk1.0-0 \
        libc6 \
        libcairo2 \
        libgbm1 \
        libgcc1 \
        libglib2.0-0 \
        libgtk-3-0 \
        libnspr4 \
        libnss3 \
        libx11-6 \
        libx11-xcb1 \
        libxcb1 \
        libxcomposite1 \
        libxcursor1 \
        libxdamage1 \
        libxext6 \
        libxfixes3 \
        libxi6 \
        libxrandr2 \
        libxrender1 \
        libxss1 \
        lsb-release \
        xdg-utils \
    && wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list' \
    && apt-get update \
    && apt-get install -y --no-install-recommends google-chrome-stable \
    && apt-get purge -y --auto-remove gnupg wget apt-transport-https \
    && rm -rf /var/lib/apt/lists/*

# Environment variables for tools/tests that look for chrome
ENV CHROME_BIN=/usr/bin/google-chrome
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true

# Recommended for browsers running in containers
# increase shared memory (devcontainer.json also sets --shm-size at runtime)

# Use the 'vscode' user provided by the base image
USER vscode

# Print chrome version when container starts (helps debugging)
CMD ["/bin/bash", "-lc", "google-chrome --version || true && sleep infinity"]
