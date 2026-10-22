# Contributing to LAN Paste

Thank you for your interest in contributing to LAN Paste! This guide covers setting up your local environment, making changes, running tests, and opening pull requests.

---

## Project Overview & Stack

LAN Paste is a lightweight self-hosted paste service intended for trusted local-area networks and Tailscale meshes.

- **Backend:** Python (Flask, Gunicorn)
- **Database:** SQLite (persisted locally or in a Docker volume)
- **Frontend:** HTML templates with vanilla CSS and JavaScript (theme toggle)
- **Containers:** Docker and Docker Compose

---

## Prerequisites

- **Python:** 3.12 or 3.13
- **Git**
- **Docker & Docker Compose** (optional for local code changes, required for container builds)

---

## Local Development Setup

1. **Fork and clone the repository:**
   ```bash
   git clone https://github.com/<your-username>/lan-paste.git
   cd lan-paste
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python -m venv .venv

   # On Linux / macOS:
   source .venv/bin/activate

   # On Windows (PowerShell):
   .venv\Scripts\Activate.ps1
   ```

3. **Install development dependencies:**
   ```bash
   pip install -r requirements-dev.txt
   ```

4. **Configure environment variables:**
   ```bash
   cp .env.example .env
   ```
   Set `PASTE_ADMIN_TOKEN` to a secret value in `.env`.
   > **Note:** `.env` is ignored by Git. Never commit `.env` or include real passwords or tokens in code or test fixtures.

5. **Start the local application:**
   ```bash
   python app.py
   ```
   Open `http://localhost:8000` in your browser.

---

## Running Tests

All pull requests run automated checks in GitHub Actions. You can run the exact same checks locally:

```bash
# Verify Python syntax:
python -m compileall -q app.py tests

# Run the test suite:
python -m pytest -q
```

---

## Running with Docker Compose

To test the containerized service locally:

```bash
# Build and run containers in background:
docker compose up -d --build

# View container logs:
docker compose logs -f

# Shut down containers:
docker compose down
```

---

## Pull Request Guidelines

- **Branching:** Create a dedicated branch from `main`:
  ```bash
  git checkout -b fix/issue-description
  ```
- **Scope:** Keep pull requests focused on a single bug or feature.
- **Testing:** Include regression or unit tests in `tests/test_app.py` for new behavior.
- **Clean Diff:** Run `git diff --check` and verify no unnecessary files or secrets are staged.

---

## Reporting Issues

If you find a bug or have a suggestion, open an issue on GitHub with:
- A clear description of the problem or feature.
- Steps to reproduce (if reporting a bug).
- Relevant environment details (OS, browser, Python/Docker version).
