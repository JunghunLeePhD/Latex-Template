# LaTeX Dev Container Template for VS Code

This repository is a GitHub template for creating a complete, lightweight, and reproducible development environment for LaTeX. It is specifically optimized for academic work, with a curated set of packages perfect for mathematical papers and Beamer presentations.

The entire environment is containerized using Docker, which solves the "it works on my machine" problem. This template offers two distinct configurations to suit your preferred editing style.

## ✨ Features

* **Choice of Environment**: Select between a standard VS Code setup or a pre-configured Vim environment.
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

#### Usage

1. **Clone your new repository** and open it in VS Code.
2. A notification will appear: **"Folder contains multiple Dev Container configuration files. Select a configuration."**
3. **Choose your preferred environment**:
   * `LaTeX (Standard)`: For a default VS Code experience.
   * `LaTeX (Vim)`: For an experience with Vim keybindings pre-installed and configured.
4. VS Code will now build the container. This may take a few minutes the first time.

That's it! You can now edit any `.tex` file in the `src/` folder and see the PDF in the `output/` folder update in real-time.

## 🔧 Configurations Explained

This template uses a shared `Dockerfile` for the base LaTeX installation, but provides two different configurations for the editor.

### 1. LaTeX (Standard)

* **Location**: `.devcontainer/base/devcontainer.json`
* **Description**: This is the default, clean experience. It only installs the essential `LaTeX Workshop` extension. It's perfect for users who want a standard editor or who manage their own editor preferences with Settings Sync.

### 2. LaTeX (Vim)

* **Location**: `.devcontainer/vim/devcontainer.json`
* **Description**: This is an "opinionated" setup that comes with the `VSCodeVim` extension pre-installed and configured with a set of efficient keybindings (e.g., `jk` for escape). This is ideal for Vim users who want to get started immediately.

## ⚠️ Troubleshooting

### Problem: Old settings seem to be stuck (e.g., files in the wrong output folder).

Sometimes, VS Code and Docker can be aggressive with caching. If you make a change to a `devcontainer.json` file and it doesn't seem to apply even after a regular rebuild, you may need to force a full, clean rebuild.

**Solution 1: Rebuild without Cache (Easier)**

1. Open the Command Palette (`Cmd+Shift+P` or `Ctrl+Shift+P`).
2. Run the command **`Dev Containers: Rebuild without Cache`**. This is slower than a normal rebuild but will solve most caching issues.

**Solution 2: Full Manual Cleanup (More Forceful)**

If the problem persists, you can manually delete the old container and image.

1. Close VS Code.
2. Open your Terminal (not in VS Code).
3. Find and remove the old container:
   ```bash
   # Find the container ID
   docker ps -a
   # Stop and remove it
   docker stop <container_id>
   docker rm <container_id>
    ```

4. Find and remove the old image:

```Bash
# Find the image ID (usually starts with vsc-)
docker images
# Remove it
docker rmi <image_id>
```

5. Re-open your project in VS Code. It will now perform a completely fresh build.

## 📁 Project Structure
```
.
├── .devcontainer/
│   ├── Dockerfile        # Shared base for both configs (OS, TeX packages)
│   ├── base/
│   │   └── devcontainer.json # "Standard" configuration
│   └── vim/
│       └── devcontainer.json # "Vim" configuration
├── src/
│   └── sample.tex        # Your LaTeX source files go here
├── output/               # All compiled files go here (ignored by git)
├── .gitignore
└── README.md
```