# Python Installation Guide 

| Author      | Created on  | Version    | Last updated by | Last edited on |
|-------------|-------------|------------|-----------------|----------------|
| Sonal       | 18-07-2025  | version 1  | Sonal           | 18-07-2025     |

## Table of Contents
- [Introduction](#introduction)
- [System Requirements](#system-requirements)
- [Installing Python on Windows](#installing-python-on-windows)
- [Installing Python on macOS](#installing-python-on-macos)
- [Installing Python on Linux](#installing-python-on-linux)
- [Verifying Installation](#verifying-installation)
- [Setting Environment Variables](#setting-environment-variables)
- [Using Virtual Environments](#using-virtual-environments)
- [Upgrading Python](#upgrading-python)
- [Best Practices](#best-practices)
- [Contact Information](#contact-information)
- [References](#references)
- [Contributor](#contributor)

---

## Introduction

This SOP provides a detailed guide for installing Python on different operating systems. Python is an interpreted, high-level programming language widely used for web development, automation, data science, and more.

---

## System Requirements

- OS: Windows 10/11, macOS, Linux 
- Admin/root access
- Internet connection
- 200MB of disk space

---

## Installing Python on Windows

1. Visit [https://www.python.org/downloads](https://www.python.org/downloads)
2. Download the latest Windows installer.
3. Run the installer:
   - **Check** “Add Python to PATH”
   - Click “Install Now”
4. Wait for the installation to complete.

---

## Installing Python on macOS

```bash
# Using Homebrew
brew install python
```

Or:

1. Download macOS installer from [https://www.python.org/downloads/mac-osx/](https://www.python.org/downloads/mac-osx/)
2. Open the `.pkg` file and follow the installation steps.

---

## Installing Python on Linux

For Debian/Ubuntu:
```bash
sudo apt update
sudo apt install python3 python3-pip
```

For RHEL/CentOS:
```bash
sudo yum install python3
```

For Arch:
```bash
sudo pacman -S python
```

---

## Verifying Installation

Check Python and pip versions:

```bash
python3 --version
pip3 --version
```

---

## Setting Environment Variables

Only required in some cases:

1. On Windows:
   - Open Environment Variables → Edit `Path` → Add Python directory, e.g., `C:\Python311\`

2. On Linux/macOS:
   ```bash
   export PATH="/usr/local/bin/python3:$PATH"
   ```

---

## Using Virtual Environments

Virtual environments help isolate dependencies:

```bash
# Create venv
python3 -m venv myenv

# Activate on Windows
myenv\Scripts\activate

# Activate on macOS/Linux
source myenv/bin/activate
```

---

## Upgrading Python

**Windows/macOS:**  
Re-run installer from [python.org](https://www.python.org)

**Linux:**  
```bash
sudo apt update && sudo apt upgrade python3
```

---

## Best Practices

1. Use the latest stable version of Python  
2. Always use virtual environments for projects  
3. Avoid editing system Python  
4. Install packages using `pip`  
5. Use `requirements.txt` for dependencies  
6. Keep Python and pip up to date  

---

## Contact Information

| **Name**     | **Email address**                |
|--------------|----------------------------------|
| Sonal        | [sonal.roha.snaatak@mygurukulam.co](sonal.roha.snaatak@mygurukulam.co) |

---

## References

| **Link**                                               | **Description**                  |
|--------------------------------------------------------|----------------------------------|
| [Official Python Docs](https://docs.python.org/3/)     | Main Python documentation        |
| [Real Python Installation Guide](https://realpython.com/installing-python/) | Community tutorial |

---

## Contributor

Sonal
