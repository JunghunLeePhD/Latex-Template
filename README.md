# LaTeX Dev Container Template for VS Code

This repository is a GitHub template for creating a complete, lightweight, and reproducible development environment for LaTeX. It is specifically optimized for academic work, with a curated set of packages perfect for mathematical papers and Beamer presentations.

The entire environment is containerized using Docker, which solves the "it works on my machine" problem. This template provides a standard, non-opinionated base, allowing you and your collaborators to use your own preferred editor settings via VS Code's Settings Sync.

## ✨ Features

* **Collaboration-Friendly**: Provides a standard base environment without forcing personal editor settings on team members.

* **Reproducible Environment**: Powered by Docker, it works exactly the same for everyone, every time.

* **Optimized for Speed**: Uses a curated, lightweight TeX Live installation, resulting in much faster build times.

* **Tailored for Academia**: Includes essential packages for mathematics (`amsmath`), modern bibliography (`biblatex`), and presentations (`beamer`).

* **Clean Project Directory**: All compiled files (PDFs, logs, etc.) are automatically placed in a top-level `output/` folder.

* **Seamless VS Code Integration**: Pre-configured with the excellent [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) extension.

## 🚀 Using as a Template

To start a new project based on this setup, you don't need to fork it.

1. Click the green **"Use this template"** button at the top of the repository page on GitHub.

2. Choose **"Create a new repository"**.

3. Give your new repository a name and description. A fresh copy of this template will be created in your account with a clean git history.

Once your new repository is created, follow the steps below.

### Quick Start

#### Prerequisites

Before you begin, make sure you have the following installed on your system:

1. [Docker Desktop](https://www.docker.com/products/docker-desktop/)

2. [Visual Studio Code](https://code.visualstudio.com/)

3. The [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension for VS Code.

4. Git setting in you local machine

  ```bash
  git config --global user.email YOUR_EMAIL
  git config --global user.name YOUR_NAME
  ```

#### Usage

1. **Clone your new repository** and open it in VS Code.

2. A notification will appear prompting you to **"Reopen in Container"**. Click it.

3. VS Code will now build the container. This may take a few minutes the first time.

That's it! You can now edit any `.tex` file in the `src/` folder and see the PDF in the `output/` folder update in real-time.

## 🔧 Customization

### Personalizing Your Editor with Settings Sync (Vim Example)

This template intentionally does **not** include personal editor settings like Vim keybindings in its configuration. This ensures that no one on your team has their preferred setup overridden.

The correct way to use your personal settings is with **VS Code Settings Sync**.

1. **Configure Your Local VS Code**: On your main computer (not in the container), open your global `settings.json` (`Preferences: Open User Settings (JSON)` from the Command Palette). Add all your preferred settings here (e.g., your Vim configuration).

2. **Turn On Settings Sync**: Make sure you are logged into your GitHub or Microsoft account in VS Code and that Settings Sync is enabled.

3. **Launch the Container**: When you open this project in the Dev Container, Settings Sync will automatically apply your personal settings and install your preferred extensions (like `VSCodeVim`) for you and only you.

This is the perfect way to have a consistent project environment while giving every collaborator their own personalized editing experience.

### Adding More LaTeX Packages

If you need a specific LaTeX package that isn't included, you will get an error like `File 'somepackage.sty' not found.`.

1. **Find the Debian package name** for it (e.g., search online for "debian package for `somepackage.sty`").

2. **Edit the `Dockerfile`:** Open `.devcontainer/Dockerfile` and add the package name to the `apt-get install` list.

3. **Rebuild the Container:** Run `Dev Containers: Rebuild Container` from the Command Palette.


## 📁 Project Structure
```
.
├── .devcontainer/
│   ├── Dockerfile        # Shared base for both configs (OS, TeX packages)
│   └── devcontainer.json
├── src/
│   └── sample.tex        # Your LaTeX source files go here
├── output/               # All compiled files go here (ignored by git)
├── .gitignore
└── README.md
```
