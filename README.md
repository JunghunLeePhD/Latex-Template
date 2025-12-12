# Collaborative LaTeX Template

A robust, pre-configured environment for writing mathematical papers using **LaTeX**, **VS Code**, and **DevContainers**. This template is designed to solve the "it works on my machine" problem by providing a consistent TeX Live environment for everyone.

## ✨ Features

* **Zero-Setup LaTeX:** The entire TeX Live distribution (approx 4GB) is pre-installed in the Docker container. No local installation required.
* **Auto-Compilation (CI/CD):** Every time you push code to GitHub, a **GitHub Action** automatically builds the PDF to ensure it compiles correctly.
* **Built-in Tools:**
    * **LaTeX Workshop:** The gold-standard VS Code extension for IntelliSense and viewing.
    * **LTeX:** Advanced grammar and spell checking for academic English.
    * **Latexmk:** Automated build tool configured to keep your directory clean.
    * **GitGraph:** Visual interface for Git history.

---

## 📋 Prerequisites

Before you begin, install these three tools. You do **not** need to install LaTeX or TeX Live manually.

1.  [**Docker Desktop**](https://www.docker.com/products/docker-desktop/) (Running in the background)
2.  [**Visual Studio Code**](https://code.visualstudio.com/)
3.  **Dev Containers Extension** for VS Code (Search `ms-vscode-remote.remote-containers` in the extension store)

---

## 🚀 Getting Started

1.  **Get the Code:**
    * Open VS Code.
    * Press `F1` and select **Git: Clone**.
    * Paste the repository URL.

2.  **Enter the Environment:**
    * Once the folder opens, you will see a popup: *"Folder contains a Dev Container configuration..."*
    * Click **Reopen in Container**.
    * *Note:* The first time you do this, it will take ~5-15 minutes to download the full TeX Live distribution.

3.  **Build the PDF:**
    * Open `main.tex`.
    * Save the file (`Ctrl+S`).
    * The PDF will automatically compile to the `build/` folder.

---

## 🤖 Automation (GitHub Actions)

This repository includes a workflow (`.github/workflows/compile_latex.yml`) that acts as a safety net.

* **When it runs:** Automatically on every `push` to the `main` branch or any Pull Request.
* **What it does:** It spins up a server, installs LaTeX, and compiles your document from scratch.
* **Why it matters:** It guarantees that your code works for everyone, not just on your local machine.
* **Download the PDF:** Go to the **Actions** tab on GitHub, click the latest run, and download the `compiled-pdf` artifact at the bottom.

---


## **📂 Project Structure**

To keep the collaboration clean, please adhere to this file structure:

- `main.tex`: The skeleton file. Loads packages and imports sections. **Do not write content here.**


- `sections/`: Write your chapters here (e.g., `01-intro.tex`, `02-proofs.tex`).


- `macros.sty`: Define all custom math commands here (e.g., `\newcommand{\R}{\mathbb{R}}`).


- `references.bib`: Your BibTeX database.


- `figures/`: Place all images and plots here.

---
## **🤝 Collaboration Workflows**

Choose the guide that matches your experience level.

### **🐣 Workflow A: For Mathematicians (The "Easy" Way)**

*Use this if you want to focus on Math and avoid Git commands.*

**Step 1: Your Personal Workspace**

1. Ask the **Repository Manager** to create a personal branch for you (e.g., `alice-draft`).


2. In VS Code, look at the bottom-left corner (it usually says `main`).


3. Click it and select your personal branch (`alice-draft`) from the list.


4. **Stop.** You stay here forever. Do not switch back to main.



**Step 2: Saving Your Work** When you finish a section or theorem:

1. Click the **Source Control** icon (Graph with nodes) on the left sidebar.


2. Type a short message (e.g., "Finished Lemma 3").


3. Click **Commit**.


4. Click **Sync Changes** (This sends your work to the cloud and downloads updates).



**Step 3: Rules**

- **Never** try to fix "Merge Conflicts" yourself. If you see an error, contact the Manager.


- **Never** rename files without asking.



### **🛠️ Workflow B: For Developers (The "Pro" Way)**

*Use this if you are comfortable with CLI, Branching, and CI/CD.*

**Branching Strategy**

- **Protection:** `main` is protected. Direct pushes are blocked.


- **Feature Branches:** Create a new branch for every task (`feature/fix-typos`, `feature/add-appendix`).


- **Merging:** Use Pull Requests (PR).



**Rebase Policy**

- **Private Branches:** You may `rebase` your local feature branches before pushing to clean up history.


- **Shared Branches:** Do **NOT** rebase any branch a mathematician is working on (e.g., `alice-draft`). It will break their local sync. Use `git merge` instead.



**Labels** This repo uses a specific taxonomy for PRs. Please tag your PRs accordingly:

- `Content: Proof` / `Content: New Section`


- `Math: Needs Check` / `Math: Verified`

---
## **🛡️ For the Repository Manager**

**How to Sync Mathematicians:** Since they stay on their personal branches, you must manually update them with the latest changes from `main`.

Run this routine periodically:

```bash
# 1. Update Main
git checkout main
git pull origin main

# 2. Update the Mathematician (e.g., Alice)
git checkout alice-draft
git pull origin alice-draft  # Get her latest work
git merge main               # Merge main INTO her branch (Do not rebase!)
git push origin alice-draft  # Push the update to her

# 3. Return to work
git checkout main
```

**Tagging Versions:** When submitting to ArXiv or a Journal, create a tag:

```bash
git tag v1.0-arxiv
git push origin v1.0-arxiv
```

---

## ⚙️ For Developers: Customizing the Environment

If you want to add a new tool or VS Code extension for **the whole team**, do not just install it locally. You must add it to the configuration file so everyone gets it.

### Adding VS Code Extensions

1.  Open `.devcontainer/devcontainer.json`.
2.  Find the `customizations.vscode.extensions` array.
3.  Add the "Extension ID" to the list.
    * *Tip:* Right-click an extension in VS Code sidebar -> **Copy Extension ID**.

```json
"extensions": [
    "james-yu.latex-workshop",
    "streetsidesoftware.code-spell-checker",
    "your-new-extension-id-here" // <--- Add it here
]
```

4. **Rebuild:** Press `F1` -> **Dev Containers: Rebuild Container** to apply changes.



### **Adding Linux Packages**

If you need a new system tool (e.g., `pandoc`, `python3`), add it to `.devcontainer/Dockerfile`:

```Dockerfile
RUN apt-get update && apt-get -y install --no-install-recommends \
    pandoc \
    python3 \
    ...
```
