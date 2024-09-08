# Use the official image as a parent image
FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu

# Install common dependencies
RUN apt-get update && apt-get install -y \
  wget \
  git \
  curl \
  unzip \
  build-essential \
  pkg-config \
  libssl-dev \
  fonts-noto-cjk \
  fonts-ipafont-gothic \
  fonts-ipafont-mincho \
  fonts-unfonts-core \
  && rm -rf /var/lib/apt/lists/*

# # Install Quarto
ARG QUARTO_VERSION="1.5.57"
RUN wget https://github.com/quarto-dev/quarto-cli/releases/download/v${QUARTO_VERSION}/quarto-${QUARTO_VERSION}-linux-amd64.deb && \
    dpkg -i quarto-${QUARTO_VERSION}-linux-amd64.deb && \
    rm quarto-${QUARTO_VERSION}-linux-amd64.deb

# Install Rust and Cargo
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH=/root/.cargo/bin:$PATH

# Clone Typst repository and build
RUN git clone https://github.com/typst/typst.git && \
    cd typst && \
    cargo build --release && \
    mv target/release/typst /usr/local/bin/typst && \
    cd .. && rm -rf typst

RUN apt-get update && apt-get install -y curl fontconfig unzip \
    && curl -O https://noto-website.storage.googleapis.com/pkgs/NotoSansCJKjp-hinted.zip \
    && mkdir -p /usr/share/fonts/NotoSansCJKjp \
    && unzip NotoSansCJKjp-hinted.zip -d /usr/share/fonts/NotoSansCJKjp/ \
    && rm NotoSansCJKjp-hinted.zip \
    && fc-cache -fv


# Verify installations
RUN typst --version
