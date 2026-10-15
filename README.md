# WritersAdda

A MkDocs Material website for a founder-led technical documentation studio, with services, process information, and clearly labeled portfolio samples.

## Preview locally

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m mkdocs serve
```

Open http://127.0.0.1:8000/ in your browser. Stop the local server with Ctrl+C.

## Before publishing

1. Replace the email, LinkedIn, and GitHub placeholders in `docs/contact.md` with working business contact details.
2. Confirm the GitHub repository and site URL in `mkdocs.yml` if the repository name or Pages URL changes.
3. Add verified biography details and any additional experience claims you want to publish.
4. Replace illustrative behavior with verified product evidence before describing any example as production-tested. Keep client work anonymized or get permission before publishing it.

The current portfolio pages are finished writing demonstrations, not client case studies. The API contract is fictional, and all examples state their validation limits.

## Build the site

```powershell
.\.venv\Scripts\python.exe -m mkdocs build --strict
```

The generated site is written to `site/`.
