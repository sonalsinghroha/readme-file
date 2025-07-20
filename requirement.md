# Requirements.txt – SOP

| Author      | Created on  | Version    | Last updated by | Last edited on |
|-------------|-------------|------------|------------------|----------------|
| Sonal       | 18-07-2025  | version 1  | Sonal            | 18-07-2025     |

---

## Table of Contents
- [Introduction](#introduction)
- [Installing from requirements.txt](#installing-from-requirementstxt)
- [Generating requirements.txt (Freezing Dependencies)](#generating-requirementstxt-freezing-dependencies)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
- [Best Practices](#best-practices)
- [Contact Information](#contact-information)
- [References](#references)
- [Contributor](#contributor)

---

## Introduction

This SOP explains how to use the `requirements.txt` file in Python projects for managing package dependencies. It enables **consistent environments** across local machines, CI/CD pipelines, and production systems.

---

## Installing from requirements.txt

Install all required Python packages in one step using:

```bash
pip install -r requirements.txt
```

> Make sure to activate your virtual environment (if any) **before** running this command.

This reads the file line by line and installs the exact versions specified.

---

## Generating requirements.txt (Freezing Dependencies)

You can generate the `requirements.txt` file in two ways:

### Method 1: Auto-generate from current environment

```bash
pip freeze > requirements.txt
```

This captures the **entire environment**, including version-locked packages, and is perfect for deployment.

### Method 2: Manually specify only key dependencies

Example content of a custom file:

```text
flask==2.3.3
pandas>=1.3.0
requests
```

This method helps you avoid cluttering the file with unnecessary packages.

---

## Troubleshooting Common Issues

| **Issue**                                  | **Root Cause**                             | **Solution**                                                                  |
|--------------------------------------------|--------------------------------------------|-------------------------------------------------------------------------------|
| `ERROR: Could not find a version`          | Incompatible or non-existing version       | Check version on [PyPI](https://pypi.org) and update in the file              |
| `ModuleNotFoundError` after install        | Package name typo or missing dependency    | Double-check the name and format                                              |
| `Permission denied`                        | User-level install blocked                 | Use `--user` or activate virtual environment                                  |
| OS-specific errors (like gcc, ssl)         | Missing system libraries                   | Install system dependencies using apt/yum (e.g. `build-essential`, `libssl`)  |
| Dependency version conflicts               | Incompatible versions between libraries    | Use `pipdeptree`, `pip check`, or `pip install --upgrade --force-reinstall`  |

---

## Best Practices

1. Always activate a **virtual environment** before generating or installing
2. Use **exact versions** to avoid future breakage (`==`, not `>=`)
3. Periodically clean and review the file to avoid unused packages
4. Test your `requirements.txt` on a clean machine before production
5. Use tools like `pip-tools` (`pip-compile`, `pip-sync`) for advanced management
6. Consider using multiple files:
   - `requirements.txt` → for production
   - `dev-requirements.txt` → for development/test dependencies

---

## Contact Information

| **Name**     | **Email address**                |
|--------------|----------------------------------|
| Sonal        | [sonal.roha.snaatak@mygurukulam.co](sonal.roha.snaatak@mygurukulam.co) |

---

## References

| **Link**                                                              | **Description**                     |
|-----------------------------------------------------------------------|-------------------------------------|
| [Pip Documentation](https://pip.pypa.io/en/stable/)                   | Official pip usage docs             |
| [Requirements File Format](https://pip.pypa.io/en/stable/cli/pip_install/#requirements-file-format) | Format and options                  |
| [PyPI](https://pypi.org)                                              | Python Package Index                 |

---

## Contributor

Sonal

