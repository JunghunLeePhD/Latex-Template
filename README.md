# LaTeX Dev Container for Math & Beamer Presentations

This repository is a GitHub template for creating a complete, lightweight, and reproducible development environment for LaTeX. It is specifically optimized for academic work, with a curated set of packages perfect for mathematical papers and Beamer presentations.

The entire environment is containerized using Docker, which solves the "it works on my machine" problem and ensures that anyone can start a new project with a single click.

## ✨ Features

* **Reproducible Environment**: Powered by Docker, it works exactly the same for everyone, every time.
* **Optimized for Speed**: Uses a curated, lightweight TeX Live installation instead of `texlive-full`, resulting in much faster build times and a smaller footprint.
* **Tailored for Academia**: Includes essential packages for mathematics (`amsmath`, etc.), modern bibliography (`biblatex`), and presentations (`beamer`) right out of the box.
* **Clean Project Directory**: All compiled files (PDFs, logs, etc.) are automatically placed in an `output/` folder, which is ignored by Git.
* **Seamless VS Code Integration**: Pre-configured with the excellent [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) extension for live preview, IntelliSense, and build commands.
* **Collaboration-Friendly**: Personal editor preferences (like Vim keybindings) are optional and are not forced on collaborators.

## 🚀 Using as a Template

To start a new project based on this setup, you don't need to fork it.

1.  Click the green **"Use this template"** button at the top of the repository page on GitHub.
2.  Choose **"Create a new repository"**.
3.  Give your new repository a name and description. A fresh copy of this template will be created in your account with a clean git history.

Once your new repository is created, follow the steps below.

### Quick Start

#### Prerequisites

Before you begin, make sure you have the following installed on your system:

1.  [Docker Desktop](https://www.docker.com/products/docker-desktop/)
2.  [Visual Studio Code](https://code.visualstudio.com/)
3.  The [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension for VS Code.

#### Usage

1.  **Clone your new repository:**
    ```bash
    git clone <your-new-repository-url>
    cd <repository-folder>
    ```

2.  **Open in VS Code:**
    ```bash
    code .
    ```

3.  **Reopen in Container:**
    A notification will appear in the bottom-right corner prompting you to "Reopen in Container". Click it.

That's it! The Dev Container will build, and VS Code will reload, placing you inside your ready-to-use LaTeX environment.

## 🔧 Customization

### Adding More LaTeX Packages

This setup is intentionally minimal. If you need a specific LaTeX package that isn't included, you will get an error like `File 'somepackage.sty' not found.`.

To add a missing package:

1.  **Find the Debian package name** for it (e.g., search online for "debian package for `somepackage.sty`"). Let's say you need a package found in `texlive-science`.

2.  **Edit the `Dockerfile`:**
    Open `.devcontainer/Dockerfile` and add the package name to the `apt-get install` list.

    ```dockerfile
    # Add your needed package, e.g., texlive-science
    RUN apt-get update && \
        apt-get install -y --no-install-recommends \
        # ... other packages ...
        texlive-latex-extra \
        texlive-science \
        # ... other packages ...
    ```

3.  **Rebuild the Container:**
    Open the Command Palette (`Cmd+Shift+P` or `Ctrl+Shift+P`) and run **`Dev Containers: Rebuild Container`**. The new package will be installed and available for you to use.

### Personalizing Your Editor (Vim Example)

This project is configured to respect individual editor preferences.

* The **VSCodeVim** extension is listed in `.vscode/extensions.json`, which means VS Code will *recommend* it to users who don't have it, but it will **not** force the installation.
* **To add your personal Vim settings, do NOT add them to this project's configuration files.** This would force your settings on everyone.

The correct way is to use VS Code's **Settings Sync**:

1.  Open your **local** VS Code (not in the container).
2.  Open your personal user settings file (`Preferences: Open User Settings (JSON)` from the Command Palette).
3.  Place all your Vim settings (keybindings, leader keys, etc.) in this file.
4.  Ensure Settings Sync is enabled.

When you start this Dev Container, Settings Sync will automatically apply your personal settings for you, while your collaborators will get their own personal settings.

## 📁 Project Structure

```
.
├── .devcontainer/
│   ├── devcontainer.json # Configures VS Code (settings, extensions) inside the container
│   └── Dockerfile        # Defines the container environment (OS, TeX Live packages)
├── .vscode/
│   └── extensions.json   # Recommends optional extensions like Vim
├── output/               # All compiled files go here (ignored by git)
├── .gitignore            # Ignores the output/ folder
├── README.md             # This file
└── sample.tex            # An example LaTeX file to get you started
```

Happy TeXing!k