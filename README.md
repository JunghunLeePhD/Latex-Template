# Collaborative LaTeX Template

A robust, pre-configured environment for writing mathematical papers using **LaTeX**, **VS Code**, and **DevContainers**. This template is designed to ensure a consistent TeX Live environment and seamless CI/CD integration.

## ✨ Features

* **Zero-Setup LaTeX:** The entire TeX Live distribution is pre-installed in the Docker container. No local installation required.
* **Auto-Compilation (CI/CD):** Every time you push code to GitHub, a **GitHub Action** automatically builds the PDF to ensure it compiles correctly.
* **Built-in Tools:**
    * **LaTeX Workshop:** The gold-standard VS Code extension for IntelliSense and viewing.
    * **LTeX:** Advanced grammar and spell checking for academic English.
    * **Latexmk:** Automated build tool configured to keep your directory clean.
    * **GitGraph:** Visual interface for Git history.


## 📋 Prerequisites

Before you begin, install these three tools. You do **not** need to install LaTeX or TeX Live manually.

1.  [**Docker Desktop**](https://www.docker.com/products/docker-desktop/) (Running in the background)
2.  [**Visual Studio Code**](https://code.visualstudio.com/)
3.  **Dev Containers Extension** for VS Code (Search `ms-vscode-remote.remote-containers` in the extension store)


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


## 🤖 Automation (GitHub Actions)

This repository includes a workflow (`.github/workflows/compile_latex.yml`) that acts as a safety net.

* **When it runs:** Automatically on every `push` to the `main` branch or any Pull Request.
* **What it does:** It spins up a server, installs LaTeX, and compiles your document from scratch.
* **Why it matters:** It guarantees that your code works for everyone, not just on your local machine.
* **Download the PDF:** Go to the **Actions** tab on GitHub, click the latest run, and download the `compiled-pdf` artifact at the bottom.


## ⚙️ Customizing the Environment

If you want to add a new tool or VS Code extension for **the whole team**, do not just install it locally. You must add it to the configuration file.

### Adding VS Code Extensions
1.  Open `.devcontainer/devcontainer.json`.
2.  Find the `customizations.vscode.extensions` array.
3.  Add the "Extension ID" to the list (Right-click extension in sidebar -> Copy Extension ID).

```json
"extensions": [
    "james-yu.latex-workshop",
    "streetsidesoftware.code-spell-checker",
    "your-new-extension-id-here"
]
```

4. **Rebuild:** Press `F1` -> **Dev Containers: Rebuild Container** to apply changes.



### **Adding Linux Packages**

If you need a new system tool (e.g., `pandoc`, `python3`), add it to `.devcontainer/Dockerfile`.

## **📂 Project Structure**

Please adhere to this file structure to keep the repository clean:

- `main.tex`: The skeleton file. Loads packages and imports sections. **Do not write content here.**


- `sections/`: Write your chapters here (e.g., `01-intro.tex`, `02-proofs.tex`).


- `macros.sty`: Define all custom math commands here (e.g., `\newcommand{\R}{\mathbb{R}}`).


- `references.bib`: Your BibTeX database.


- `figures/`: Place all images and plots here.

## 🤝 Collaboration Workflow

We use a **Main-Production** strategy.
* **`main`**: The active working branch. All new features land here first.
* **`production`**: The "Gold Master". Only contains versions submitted to ArXiv/Journals.

### 1. Daily Routine (For Developers/Collaborators)

**Step 1: Start a Task**
Always branch from `main`.

```bash
git checkout main
git pull origin main
git checkout -b feature/lemma-proof
```



**Step 2: Work & Commit** Write your LaTeX. Commit often.


```bash
git add .
git commit -m "Drafting Lemma 3"
```


**Step 3: Submit for Review** Push your branch and open a Pull Request (PR) targeting **`**main**`**.


```bash
git push origin feature/lemma-proof
```




- **GitHub Action** will automatically compile your PDF to check for errors.


- Assign **Labels** (e.g., `Content: Proof`, `Math: Needs Check`).


- Request a **Review** from a colleague.



**Step 4: Merge** Once approved and the build passes, merge the PR into `main`.

### **2. Releasing a Version (Manager Only)**

When the paper is ready for submission (e.g., ArXiv or a Journal):

1. **Merge to Production:** Create a Pull Request from `main` into `production`.


2. **Tag it:** After merging, switch to production and tag the specific commit.


```bash
git checkout production
git pull origin production
git tag v1.0-arxiv
git push origin v1.0-arxiv
```

## 📋 How to Use GitHub Projects (Task Management)

We use **GitHub Projects** to track the progress of our paper. Think of it as our virtual whiteboard.

### 1. The Board Columns
* **Todo:** Sections, proofs, or ideas that we need to write but haven't started yet.
* **In Progress:** Branches currently being worked on (e.g., "Alice is writing the Introduction").
* **Review:** Pull Requests that are finished and waiting for someone to read/check.
* **Done:** Merged into `main`.

### 2. Creating a Task (Issue)
If you notice a gap in the logic or need a new section:
1.  Go to the **Issues** tab.
2.  Click **New Issue**.
3.  Give it a clear title (e.g., *"Write proof for Theorem 2"* or *"Fix citation format"*).
4.  (Optional) Assign it to yourself if you plan to do it immediately.

### 3. Linking Work to Tasks
When you create a Pull Request, link it to the Issue so the board updates automatically.
* In your Pull Request description, type: `Closes #12` (where #12 is the issue number).
* GitHub will automatically move the card to **Done** when your code is merged.

### **Setup Tip (For You, The Manager)**

Since you are setting this up for the first time:

1. Go to the **Projects** tab in your repository.


2. Click **Link a project** (or Create new).


3. Choose the **"Board"** template.


4. In the Project settings, ensure you turn on **"Workflows"** so that items move automatically (e.g., when a PR is opened, move item to "In Progress").