# Use a lightweight Ubuntu base
FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Set environment variables to allow non-interactive installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    # ---- Core Build Tools ----
    latexmk \
    chktex \
    texlive-extra-utils \
    \
    # ---- Dependencies for Formatter (Perl) ----
    # (Note: Java is removed)
    libyaml-tiny-perl \
    libfile-homedir-perl \
    \
    # ---- LaTeX Packages ----
    texlive-latex-base \
    texlive-latex-recommended \
    texlive-fonts-recommended \
    texlive-latex-extra \
    texlive-bibtex-extra \
    biber \
    texlive-lang-european \
    \
    # ---- Cleanup ----
    && apt-get autoremove -y && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Revert DEBIAN_FRONTEND to default
ENV DEBIAN_FRONTEND=dialog