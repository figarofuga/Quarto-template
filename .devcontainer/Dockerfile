# Use the official image as a parent image
FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu

# Install common dependencies
RUN apt-get update && apt-get install -y \
  wget \
  git \
  curl \
  fonts-noto-cjk \
  fonts-ipafont-gothic \
  fonts-ipafont-mincho \
  fonts-unfonts-core \
#   texlive-xetex \
#   texlive-lang-cjk && \
  rm -rf /var/lib/apt/lists/*

# # Install Quarto
# ARG QUARTO_VERSION="1.4.0"
# RUN wget https://github.com/quarto-dev/quarto-cli/releases/download/v${QUARTO_VERSION}/quarto-${QUARTO_VERSION}-linux-amd64.deb && \
#     dpkg -i quarto-${QUARTO_VERSION}-linux-amd64.deb && \
#     rm quarto-${QUARTO_VERSION}-linux-amd64.deb

# Install Typst
RUN curl -L https://github.com/typst/typst/releases/latest/download/typst-linux-x86_64.zip -o typst.zip && \
    unzip typst.zip -d typst && \
    mv typst/typst /usr/local/bin/typst && \
    rm -r typst typst.zip

# Verify installations
RUN quarto check install && \
    typst --version
