# Introduction to Make – Documentation

| Author      | Created on  | Version    | Last updated by | Last edited on |
|-------------|-------------|------------|-----------------|----------------|
| Sonal       | 18-07-2025  | version 1  | Sonal           | 17-07-2025     |

## Table of Contents
- [Introduction](#introduction)
- [What is Make?](#what-is-make)
- [Key Features](#key-features)
- [Why Use Make?](#why-use-make)
- [Basic Makefile Example](#basic-makefile-example)
- [Best Use Cases](#best-use-cases)
- [Contact Information](#contact-information)
- [References](#references)
- [Contributor](#contributor)

---

## Introduction

This document provides an overview of **`make`**, a powerful build automation tool commonly used in software development to compile and manage projects efficiently. Originally created for C/C++ programs, `make` is now used for a wide range of automation tasks.

---

## What is Make?

`make` is a command-line utility that reads instructions from a **Makefile**, which defines:
- **Targets** (files to generate)
- **Dependencies** (files the targets depend on)
- **Commands** (how to build/update them)

This allows developers to automate compilation, testing, installation, and more, by simply running:

```bash
make
```

---

## Key Features

| **Feature**              | **Description**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| **Declarative Rules**    | Define how to build targets from dependencies                                   |
| **Automatic Dependency Tracking** | Rebuilds only what's changed, improving efficiency                      |
| **Variables and Macros** | Use variables to simplify and modularize your Makefile                         |
| **Pattern Rules**        | Write generalized build rules for multiple files                               |
| **Portability**          | Works on most UNIX-based systems and also on Windows (via tools like MinGW)    |
| **Shell Integration**    | Executes shell commands directly within Makefiles                              |

---
## Why Use Make?

- Automates complex build processes  
- Saves time by only rebuilding what has changed  
- Reduces human error and improves reliability  
- Improves maintainability of large codebases  
- Works cross-platform (Unix/Linux/macOS; available for Windows)  
- Easily integrates into CI/CD pipelines

---
## Basic Makefile Example

```make
all: app

app: main.o utils.o
\tgcc -o app main.o utils.o

main.o: main.c
\tgcc -c main.c

utils.o: utils.c
\tgcc -c utils.c

clean:
\trm -f *.o app
```

To build:
```bash
make
```

To clean:
```bash
make clean
```

---

## Best Use Cases

- Compiling source code (especially C/C++/Fortran)  
- Automating testing or deployment tasks  
- Building static websites  
- Running Docker or Kubernetes commands in sequence  
- Managing scripts and CLI tools in data science or DevOps  

---

## Contact Information

| **Name**     | **Email address**                |
|--------------|----------------------------------|
| Sonal        | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## References

| **Link**                                               | **Description**                       |
|--------------------------------------------------------|---------------------------------------|
| [GNU Make Manual](https://www.gnu.org/software/make/manual/make.html) | Official documentation               |
| [Makefile Tutorial](https://makefiletutorial.com/)     | Beginner-friendly tutorial            |

---

## Contributor

 Sonal
