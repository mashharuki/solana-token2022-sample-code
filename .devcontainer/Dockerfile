FROM mcr.microsoft.com/devcontainers/rust:1-bullseye

# Install dependencies
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    build-essential \
    pkg-config \
    libssl-dev \
    libudev-dev \
    ca-certificates \
    curl

# Install Solana CLI
RUN sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

# Add Solana to PATH for the following commands
ENV PATH="/root/.local/share/solana/install/active_release/bin:${PATH}"

# Install spl-token CLI
# Note: This might take a while to compile
RUN cargo install spl-token-cli

# Verify installations
RUN solana --version && spl-token --version
