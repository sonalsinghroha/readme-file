# Golang Installation Guide – Standard Operating Procedure (SOP)

| Author      | Created on  | Version    | Last updated by | Last edited on |
|-------------|-------------|------------|-----------------|----------------|
| Sonal       | 18-07-2025  | version 1  | Sonal           | 18-07-2025     |

## Table of Contents
- [Introduction](#introduction)
- [System Requirements](#system-requirements)
- [Installing Go on Windows](#installing-go-on-windows)
- [Installing Go on macOS](#installing-go-on-macos)
- [Installing Go on Linux](#installing-go-on-linux)
- [Verifying Installation](#verifying-installation)
- [Setting GOPATH and Environment Variables](#setting-gopath-and-environment-variables)
- [Uninstalling Go](#uninstalling-go)
- [Best Practices](#best-practices)
- [Contact Information](#contact-information)
- [References](#references)
- [Contributor](#contributor)

---

## Introduction

This SOP outlines the process of installing the Go programming language (Golang) on Windows, macOS, and Linux systems. Go is known for its simplicity, concurrency support, and performance.

---

## System Requirements

- OS: Windows 10/11, macOS, or Linux
- 200MB of disk space
- Internet connection
- Admin/root privileges

---

## Installing Go on Windows

1. Visit [https://go.dev/dl](https://go.dev/dl)
2. Download the Windows `.msi` installer.
3. Run the installer and follow prompts.
4. Confirm installation directory and proceed.

---

## Installing Go on macOS

### Method 1: Using Homebrew
```bash
brew install go
```

### Method 2: Manual Installation
1. Download the `.pkg` file from [https://go.dev/dl](https://go.dev/dl)
2. Open the file and follow the installation steps.

---

## Installing Go on Linux

### Debian/Ubuntu:
```bash
sudo apt update
sudo apt install golang-go
```

### Manual Installation (latest version):
```bash
wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
```

Add Go to PATH:
```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.profile
source ~/.profile
```

---

## Verifying Installation

Check version:
```bash
go version
```

Check environment:
```bash
go env
```

---

## Setting GOPATH and Environment Variables

Set up Go workspace:
```bash
mkdir -p ~/go/{bin,src,pkg}
```

Add to shell profile (`~/.bashrc`, `~/.zshrc`, or `~/.profile`):
```bash
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

Apply changes:
```bash
source ~/.bashrc  # or source ~/.zshrc
```

---

## Uninstalling Go

### Windows:
- Use "Add or Remove Programs" and uninstall Go

### macOS/Linux:
```bash
sudo rm -rf /usr/local/go
```

Remove PATH references from profile files.

---

## Best Practices

1. Always install latest stable version from official site  
2. Use Go modules (`go mod init`) instead of GOPATH for dependency management  
3. Keep `$GOPATH` clean and organized  
4. Avoid modifying system Go installation  
5. Regularly update Go for security patches  

---

## Contact Information

| **Name**     | **Email address**                |
|--------------|----------------------------------|
| Sonal        | [sonal@example.com](mailto:sonal@example.com) |

---

## 📚 References

| **Link**                                             | **Description**                |
|------------------------------------------------------|--------------------------------|
| [Go Downloads](https://go.dev/dl)                    | Official download page         |
| [Installing Go](https://go.dev/doc/install)          | Official installation guide    |
| [Go Environment Variables](https://golang.org/doc/gopath_code.html) | Guide to GOPATH and environment |

---

## 👥 Contributor

- [Sonal](#)
