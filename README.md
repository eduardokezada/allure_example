# SDET Automation Examples (Python)
![Tests](https://github.com/eduardokezada/sdet-automation-examples/actions/workflows/tests.yml/badge.svg)
End-to-end **UI** tests with Selenium and **API** tests with Pytest + Requests. CI via GitHub Actions, HTML report as artifact.

## Targets
- **UI:** https://www.saucedemo.com (public QA demo site)
- **API:** https://dummyjson.com (public fake API)

## Tech
- Python 3.11+
- pytest, requests
- selenium + webdriver-manager (Chrome, headless)
- pytest-html (report uploaded in CI)

## Quick start (local)
```bash
python -m venv .venv && . .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# Run API tests
pytest -q api_tests

# Run UI tests (headless by default)
pytest -q ui_tests

# Generate combined HTML report
pytest --html=report.html --self-contained-html
```

## Config
- Env vars:
  - `API_BASE` (default: https://dummyjson.com)
  - `HEADLESS` (default: 1)
- Centralized in `utils/config.py`

## CI
GitHub Actions workflow in `.github/workflows/tests.yml`:
- Installs deps
- Runs API + UI test suites
- Uploads `report.html` as artifact

## Structure
```
sdet-automation-examples/
├── api_tests/
├── ui_tests/
├── utils/
├── .github/workflows/tests.yml
├── pytest.ini
└── requirements.txt
```

## Reports
- HTML report (`report.html`) uploaded in CI artifacts.
- Allure report generated and uploaded in CI artifacts (`allure-report`).


## Allure report
Generate an interactive Allure report (requires Java 11+ locally):
```bash
# run tests and collect allure results
pytest --alluredir=allure-results
# generate html
allure generate allure-results -o allure-report --clean
# open locally
allure open allure-report
```
In CI, the workflow generates and uploads the **allure-report** folder as an artifact.


## GitHub Pages (Allure) 🎉
This workflow publishes the Allure report to **GitHub Pages** on every push.
After the first successful run, your report will be available at:
```
https://eduardokezada.github.io/sdet-automation-examples/allure/index.html
```
If Pages is disabled, enable **Settings → Pages → Build and deployment → Source: GitHub Actions**.
