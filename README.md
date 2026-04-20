# Agentic Self-Healing UI Framework

An agentic test automation framework that automatically recovers from broken UI selectors using AI-driven self-healing strategies — with Allure reporting and a live CI dashboard.

[![CI Self-Healing Test Suite](https://github.com/gautamakky10/agentic-self-healing-framework-gv/actions/workflows/allure-report.yml/badge.svg)](https://github.com/gautamakky10/agentic-self-healing-framework-gv/actions/workflows/allure-report.yml)

---

## How It Works

When a Selenium selector fails, the `SelectorRecoveryAgent` attempts multiple fallback strategies (ID, name, XPath, CSS, link text) to locate the element and heal the test in real time. Each heal is logged and surfaced in the Allure report.

## Stack

| Layer | Technology |
|---|---|
| Language | Java 21 |
| Test Runner | JUnit 5 |
| Browser Automation | Selenium 4 + WebDriverManager |
| Reporting | Allure 2 |
| CI | GitHub Actions |
| Report Hosting | GitHub Pages (`gh-pages` branch) |
| Dashboard Data | `dashboard-data` branch (`history.json`, `latest.json`) |

## CI Pipeline (4 Stages)

```
install → lint → retail-role-flows → healing-report-summary
```

| Stage | What it does |
|---|---|
| `install` | Resolves Maven deps, caches `.m2` |
| `lint` | Validates POM, compiles sources |
| `retail-role-flows` | Runs `RetailWebsiteTest`, generates & deploys Allure report |
| `healing-report-summary` | Parses results, builds `run.json`, pushes to `dashboard-data` |

## Allure Report

Deployed to GitHub Pages after every run on `main`:

```
https://gautamakky10.github.io/agentic-self-healing-framework-gv/
```

## Run Locally

**Prerequisites:** Java 21, Maven 3.x, Google Chrome

```bash
# Run all tests
mvn clean test -Dtest=RetailWebsiteTest

# Generate Allure report (requires allure CLI)
allure serve target/allure-results
```

## Project Structure

```
src/test/java/com/selfhealing/
├── RetailWebsiteTest.java       # Main test suite
├── SelectorRecoveryAgent.java   # Self-healing selector logic
├── TestOrchestrator.java        # Test lifecycle management
├── HealingReportWriter.java     # Writes heal events to Allure
├── RecoveryResult.java          # Heal outcome model
├── DomSnapshotTool.java         # DOM capture utility
└── DashboardTest.java           # Dashboard smoke tests

.github/workflows/
└── allure-report.yml            # 4-stage CI pipeline
```
