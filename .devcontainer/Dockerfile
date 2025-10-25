# Use a standard Debian base image for Dev Containers
FROM mcr.microsoft.com/devcontainers/base:bullseye

# Set environment variables to allow non-interactive installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install a curated set of TeX Live packages
# This is much smaller than texlive-full but is tailored for math and beamer.
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    # ---- Core Build Tool ----
    latexmk \
    chktex \
    texlive-extra-utils\
    \
    # ---- Base System & Common Packages ----
    # Includes the LaTeX kernel, article/book classes, graphicx, etc.
    texlive-latex-base \
    texlive-latex-recommended \
    \
    # ---- Fonts ----
    # Provides a good set of standard fonts for text and math
    texlive-fonts-recommended \
    \
    # ---- Bibliography ----
    # biber is the backend for the modern biblatex package
    biber \
    # texlive-bibtex-extra contains biblatex
    texlive-bibtex-extra \
    \
    # ---- Math & Presentations (Beamer) ----
    # This is a key package. It includes the beamer class for presentations,
    # plus a huge collection of other useful packages for advanced mathematics,
    # tables, and graphics (like amsmath, geometry, etc.).
    texlive-latex-extra \
    \
    # ---- Language Support (Optional but recommended) ----
    # For papers in languages other than English
    texlive-lang-european \
    && \
    # Clean up APT cache to keep the image size down
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Revert DEBIAN_FRONTEND to default
ENV DEBIAN_FRONTEND=dialog

