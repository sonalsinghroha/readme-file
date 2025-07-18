# Requirements.txt Management – Standard Operating Procedure (SOP)

| Author      | Created on  | Version    | Last updated by | Last edited on |
|-------------|-------------|------------|-----------------|----------------|
| Sonal       | 18-07-2025  | version 1  | Sonal           | 18-07-2025     |

## Table of Contents
- [Introduction](#introduction)
- [Installing from requirements.txt](#installing-from-requirementstxt)
- [Creating requirements.txt](#creating-requirementstxt)
- [Freezing Installed Packages](#freezing-installed-packages)
- [Best Practices](#best-practices)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
- [Contact Information](#contact-information)
- [References](#references)
- [Contributor](#contributor)

---

## Introduction

This SOP covers the usage of `requirements.txt` files in Python for dependency management. The file lists all Python packages required for a project, ensuring consistent environments across machines.

---

## Installing from requirements.txt

Install all listed packages in one command:

```bash
pip install -r requirements.txt
```

This ensures all required dependencies are installed at the specified versions.

---

## Creating requirements.txt

Manually or automatically create the file:

### Method 1: Freeze current environment
```bash
pip freeze > requirements.txt
```

### Method 2: Selectively write dependencies
```text
flask==2.3.3
pandas>=1.3.0
requests
```

---

## Freezing Installed Packages

Use `pip freeze` to list all installed packages with version numbers:

```bash
pip freeze
```

Redirect output to `requirements.txt` to capture the environment:

```bash
pip freeze > requirements.txt
```

This is useful for sharing or recreating the environment.

---

## Best Practices

1. Always use a virtual environment before generating requirements  
2. Keep versions pinned for stability  
3. Regularly update and test `requirements.txt`  
4. Use `pip-tools` for more advanced dependency management  
5. Avoid including unnecessary packages  
6. Consider separating dev and prod requirements (e.g., `dev-requirements.txt`)

---

## Troubleshooting Common Issues

| **Issue**                                  | **Solution**                                                                 |
|--------------------------------------------|------------------------------------------------------------------------------|
| Incompatible versions                      | Review version numbers and use compatible ones                              |
| Package not found                          | Check spelling and availability on [PyPI](https://pypi.org)                 |
| OS-specific build errors                   | Use pre-built wheels or install required system libraries                   |
| Conflicts in dependencies                  | Use `pipdeptree` or `pip check` to resolve conflicts                        |
| Permissions error                          | Try `--user` flag or use virtual environments                               |

---

## Contact Information

| **Name**     | **Email address**                |
|--------------|----------------------------------|
| Sonal        | [sonal@example.com](mailto:sonal@example.com) |

---

## 📚 References

| **Link**                                                              | **Description**                     |
|-----------------------------------------------------------------------|-------------------------------------|
| [Pip Documentation](https://pip.pypa.io/en/stable/)                   | Official pip usage docs             |
| [Requirements File Format](https://pip.pypa.io/en/stable/cli/pip_install/#requirements-file-format) | Format and options                  |

---

## 👥 Contributor

- [Sonal](#)
