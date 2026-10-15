# Run the WritersAdda site locally

**Sample type:** Self-directed portfolio demonstration · **Validation:** The strict MkDocs build command was run in the current project environment on Windows PowerShell. Fresh-install steps are documented but not separately tested on each platform.

This guide shows how to install the documentation site's dependencies, preview changes, and build a production-ready static site. It is written for contributors editing the WritersAdda MkDocs project.

## Prerequisites

- Python 3.10 or newer
- Git, if you are cloning the repository
- PowerShell on Windows, or a terminal on macOS/Linux

Check the installed Python version:

```powershell
py --version
```

On macOS/Linux, use `python3 --version`.

## Get the project

Clone the repository and move into its directory:

```bash
git clone https://github.com/writersadda24/writersadda.git
cd writersadda
```

If you already have the project, skip this step and open a terminal in its root directory (the directory containing `mkdocs.yml`).

## Create an isolated environment

On Windows PowerShell:

```powershell
py -m venv .venv
```

On macOS/Linux:

```bash
python3 -m venv .venv
```

You do not need to activate the environment if you invoke its Python executable directly.

## Install dependencies

Windows PowerShell:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

macOS/Linux:

```bash
./.venv/bin/python -m pip install -r requirements.txt
```

## Preview the documentation

Windows PowerShell:

```powershell
.\.venv\Scripts\python.exe -m mkdocs serve
```

macOS/Linux:

```bash
./.venv/bin/python -m mkdocs serve
```

Open `http://127.0.0.1:8000/`. The preview server rebuilds the site when source files change. Stop it with `Ctrl+C`.

## Build the site

Run a strict build before committing:

```powershell
.\.venv\Scripts\python.exe -m mkdocs build --strict
```

The generated static site is written to `site/`. A successful strict build means MkDocs found no warnings; it does not verify that illustrative sample API behavior exists in a real service.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| `py` is not recognized | Install Python and enable the Python launcher, or use `python` if it is on `PATH`. |
| `No module named mkdocs` | Install the dependencies using the `.venv` Python command above. |
| Port 8000 is already in use | Start the preview on another port: `python -m mkdocs serve --dev-addr 127.0.0.1:8001`. |
| A page does not appear in navigation | Add its Markdown path to the `nav` section in `mkdocs.yml`. |
| Strict build reports a warning | Fix the warning in the source before publishing. |

## Publish changes

Push changes to the `main` branch. The repository's GitHub Actions workflow builds the site and deploys it to GitHub Pages. Check the workflow run in the repository's **Actions** tab before sharing the updated site.

[View services](../services.md) · [Contact WritersAdda](../contact.md)
