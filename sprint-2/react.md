

# React CI Checks – Dependency Scanning

<img width="302" height="167" alt="image" src="https://github.com/user-attachments/assets/6879c31b-a933-4d55-bf44-a4bf1a5dc000" />

## Author Information

| Created by | Created on | Version | Last Updated On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------- | ---------- | ------- | --------------- | ------------ | ----------- | ----------- | ----------- |
| Sonal      | 11-08-2025 | V 1.0   | 11-08-2025      | Anjali       |             |             |             |

---

## Table of Contents

* [Introduction](#introduction)
* [What is Dependency Scanning in CI?](#what-is-dependency-scanning-in-ci)
* [Why is Dependency Scanning Important?](#why-is-dependency-scanning-important)
* [Workflow of CI Dependency Scanning](#workflow-of-ci-dependency-scanning)
* [Different Tools for React Dependency Scanning](#different-tools-for-react-dependency-scanning)
* [Comparison of Popular Tools](#comparison-of-popular-tools)
* [Advantages of Dependency Scanning in React CI](#advantages-of-dependency-scanning-in-react-ci)
* [Proof of Concept (POC)](#proof-of-concept-poc)
* [Best Practices](#best-practices)
* [Recommendations & Conclusion](#recommendations--conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

## Introduction

This document explains **React CI Checks for Dependency Scanning**, outlining the process, importance, tools, and best practices for identifying vulnerable, outdated, or risky dependencies in React applications.
It also includes tool comparisons, a workflow diagram, and a POC for implementation in CI pipelines.

---

## What is Dependency Scanning in CI?

**Dependency scanning** in CI/CD is an automated process that analyzes the libraries, frameworks, and packages your React application depends on, checking them for known vulnerabilities, license issues, or outdated versions.
For React, this typically involves **npm**, **yarn**, or **pnpm** dependency audits integrated into CI pipelines.

---

## Why is Dependency Scanning Important?

| Reason                    | Description                                             |
| ------------------------- | ------------------------------------------------------- |
| **Security**              | Detects vulnerable dependencies that can be exploited.  |
| **Compliance**            | Ensures licensing requirements are met.                 |
| **Stability**             | Avoids using outdated or unmaintained packages.         |
| **Performance**           | Identifies heavy or unnecessary dependencies.           |
| **Continuous Monitoring** | Automatically scans dependencies on every commit or PR. |

---

## Workflow of CI Dependency Scanning

| Step | Action                                                               |
| ---- | -------------------------------------------------------------------- |
| 1    | Developer commits or updates code in the repository.                 |
| 2    | CI pipeline triggers and installs dependencies.                      |
| 3    | Dependency scanning tool runs (npm audit, Snyk, Dependabot, etc.).   |
| 4    | Tool compares dependencies with vulnerability databases (e.g., NVD). |
| 5    | Report is generated in CI logs or sent to dashboards.                |
| 6    | Developer reviews vulnerabilities and applies fixes/upgrades.        |
| 7    | Code is merged after resolving critical vulnerabilities.             |

---

**Workflow Diagram:**

```
[Commit/Pull Request]  
     ↓  
[CI Pipeline Trigger]  
     ↓  
[Dependency Installation]  
     ↓  
[Dependency Scanning Tool Execution]  
     ↓  
[Generate Vulnerability Report]  
     ↓  
[Fix Vulnerabilities]  
     ↓  
[Merge Code]
```

---

## Different Tools for React Dependency Scanning

| Tool Name                  | Purpose                                              | Highlights                                   |
| -------------------------- | ---------------------------------------------------- | -------------------------------------------- |
| **npm audit**              | Built-in npm vulnerability scanner                   | Quick, integrated into npm CLI               |
| **yarn audit**             | Yarn package vulnerability scanning                  | Similar to npm audit for Yarn users          |
| **Snyk**                   | Security scanning & remediation suggestions          | Cloud dashboard, PR integration              |
| **Dependabot**             | Automated dependency update PRs                      | Native to GitHub, auto-fixes vulnerabilities |
| **OWASP Dependency-Check** | Checks dependencies against CVE databases            | Open-source, broad ecosystem support         |
| **Retire.js**              | Scans JavaScript libraries for known vulnerabilities | Focused on JS vulnerabilities                |

---

## Comparison of Popular Tools

| Feature/Tool      | npm audit | yarn audit | Snyk        | Dependabot    | OWASP DC    |
| ----------------- | --------- | ---------- | ----------- | ------------- | ----------- |
| **Speed**         | Fast      | Fast       | Medium      | Medium        | Medium      |
| **Remediation**   | Partial   | Partial    | Full        | Full          | Partial     |
| **Automation**    | Yes       | Yes        | Yes         | Yes           | Partial     |
| **License Check** | No        | No         | Yes         | Yes           | Yes         |
| **Cost**          | Free      | Free       | Paid & Free | Free          | Free        |
| **Integration**   | Easy      | Easy       | CI/CD Ready | GitHub Native | CI/CD Ready |

---

## Advantages of Dependency Scanning in React CI

| Advantage                 | Benefit                                       |
| ------------------------- | --------------------------------------------- |
| **Security Assurance**    | Blocks vulnerable packages before production. |
| **Faster Fixes**          | Suggests and automates version upgrades.      |
| **Compliance Safety**     | Avoids license-related legal risks.           |
| **Operational Stability** | Reduces dependency-related outages.           |
| **Continuous Protection** | Protects codebase on every PR or commit.      |

---

## Proof of Concept (POC)

Example: **GitHub Actions with npm audit + Snyk**

**.github/workflows/dependency-scan.yml**

```yaml
name: React Dependency Scanning

on: [push, pull_request]

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - name: Install dependencies
        run: npm ci
      - name: Run npm audit
        run: npm audit --audit-level=high
      - name: Snyk Scan
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

This setup runs both npm audit and Snyk scans on every commit or PR.

---

## Best Practices

* Run **dependency scanning** on every PR before merge.
* Set **audit levels** (e.g., high or critical) to block merges on severe vulnerabilities.
* Use **Dependabot** for automatic updates.
* Regularly review and remove unused dependencies.
* Maintain a **lock file** (`package-lock.json` / `yarn.lock`) to avoid version drift.
* Periodically upgrade Node.js and package manager versions.

---

## Recommendations & Conclusion

For most React projects:

* Use **npm audit** or **yarn audit** for quick scanning.
* Add **Snyk** for deeper vulnerability insights and remediation.
* Enable **Dependabot** for automated PR updates.
* Integrate scans into CI to **block merges** with critical vulnerabilities.

Dependency scanning is **not optional** — it’s essential for securing your React applications and keeping them stable in production.

---

## Contact Information

| Name  | Email                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Sonal | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## References

| Link                                                                      | Description                                     |
| ------------------------------------------------------------------------- | ----------------------------------------------- |
| [npm audit Docs](https://docs.npmjs.com/cli/v9/commands/npm-audit)        | npm built-in security scanner                   |
| [yarn audit Docs](https://classic.yarnpkg.com/en/docs/cli/audit/)         | Yarn package vulnerability check                |
| [Snyk Docs](https://docs.snyk.io/)                                        | Dependency vulnerability scanning & remediation |
| [Dependabot Docs](https://docs.github.com/en/code-security/dependabot)    | Automated dependency updates                    |
| [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/) | Open-source CVE-based dependency scanner        |



Do you want me to create that diagram?
