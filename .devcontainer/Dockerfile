# Use the official Microsoft dev containers base image for Ubuntu 24.04
FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

# Set DEBIAN_FRONTEND to noninteractive to prevent interactive prompts during apt-get install
ENV DEBIAN_FRONTEND=noninteractive

# Chained RUN command to:
# 1. Update package lists
# 2. Install prerequisite packages (software-properties-common for PPA, git, unzip)
# 3. Add the deadsnakes PPA for newer Python versions
# 4. Update package lists again (after adding PPA)
# 5. Install Python 3.13, its pip, venv, and development headers
# 6. Install uv using the pip from Python 3.13
# 7. Clean up apt caches to reduce final image size
RUN apt-get update -y && \
    apt-get install -y software-properties-common git unzip && \
    add-apt-repository -y ppa:deadsnakes/ppa && \
    apt-get update -y && \
    apt-get install -y python3.13 python3.13-pip python3.13-venv python3.13-dev && \
    pip3.13 install uv && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# You can optionally set Python 3.13 to be the default 'python3' and 'pip3'
# This makes 'python3' and 'pip3' commands use these specific versions.
# Uncomment the next lines if you want this behavior.
# RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.13 1 && \
#     update-alternatives --install /usr/bin/pip3 pip3 /usr/bin/pip3.13 1

# The base image likely sets a non-root user like 'vscode'.
# Tools installed above as root will be in the system PATH.

# Simple command to keep the container running, devcontainer.json might override this.
CMD ["sleep", "infinity"]