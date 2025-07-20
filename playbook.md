# Ansible Playbook - Documentation

| Author | Created on | Version | Last updated by | Last edited on |
|--------|------------|---------|------------------|----------------|
| Sonal  | 18-07-25   | version 1	  | Sonal            | 18-07-25       |

---

## Table of Contents
- [Introduction](#introduction)
- [Why Ansible Playbooks are Used](#why-ansible-playbooks-are-used)
- [What to Include in an Ansible Playbook](#what-to-include-in-an-ansible-playbook)
- [Key Features of Ansible Playbooks](#key-features-of-ansible-playbooks)
- [How to Write an Ansible Playbook](#how-to-write-an-ansible-playbook)
- [Sample Ansible Playbook](#sample-ansible-playbook)
- [Best Practices](#best-practices)
- [Common Mistakes](#common-mistakes)
- [Contact Information](#contact-information)
- [References](#references)
- [Contributors](#contributors)

---

## Introduction

An **Ansible Playbook** is a YAML-formatted file that defines a set of automation tasks used for configuration management, application deployment, and IT orchestration.

Playbooks describe **what** actions to perform and **in what order**, making them easy to read, share, and reuse across teams.

Ansible is **agentless**, which means it doesn’t require any software or agents to be installed on the target systems. All it needs is **SSH access** and Python installed on the managed nodes.


---

## Why Ansible Playbooks are Used

- **Automation of Manual Tasks** – No more typing the same commands on multiple servers.
- **Consistency** – All environments (dev/stage/prod) stay same.
- **Version Controlled** – Stored in Git for tracking changes.
- **Scalability** – Run tasks across 100s of servers easily.
- **Easy Rollbacks** – You can revert configs easily if you write reversible tasks.

---

## What to Include in an Ansible Playbook

- **Play Name** – Description of what the playbook does
- **Hosts** – Target systems (e.g., `webservers`, `all`, `localhost`)
- **Become** – If root privileges are required (become: yes)
- **Vars** – Variables for reuse
- **Tasks** – Step-by-step actions to execute
- **Handlers** – For service restart etc., triggered by tasks
- **Roles** – Reusable modules (optional but powerful)

---

## Key Features of Ansible Playbooks

- **YAML-based** – Simple, readable structure
- **Idempotent** – Running it multiple times won’t change the result
- **Modular** – Use roles, variables, includes
- **Error Handling** – Use `ignore_errors`, `failed_when`, etc.
- **Notification** – Use `notify` to trigger `handlers` like service restart

---

## How to Write an Ansible Playbook

```bash
1. Create a file: playbook.yml
2. Define hosts and become (root) if needed
3. Write tasks in order
4. Use modules like `apt`, `service`, `copy`, `template`, etc.
5. Run using: ansible-playbook playbook.yml -i inventory
```

---

## Sample Ansible Playbook

```yaml
---
- name: Install and Start NGINX
  hosts: webservers
  become: yes

  tasks:
    - name: Install NGINX
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Start NGINX
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Copy index.html
      copy:
        src: files/index.html
        dest: /var/www/html/index.html
```

---

## Best Practices

- Use **meaningful play and task names**
- Keep playbooks **modular** using **roles**
- Always **test** on non-prod environments
- Use **variables and templates** to avoid duplication
- Store playbooks in **Git repo** with proper versioning
- Use **handlers** for service restarts instead of repeating code
- Add **comments** for clarity

---

## Common Mistakes

| Mistake                     | Problem Caused                            |
|-----------------------------|--------------------------------------------|
| Hardcoding values           | Makes playbook non-reusable                |
| Not using handlers          | Services may restart unnecessarily         |
| No error handling           | Playbook stops on minor issues             |
| Skipping `become: yes`      | Commands may fail if root access is needed |
| Poor indentation in YAML    | Causes parsing errors                      |

---

## Contact Information

| Name   | Email                      |
|--------|----------------------------|
| Sonal  | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## References

| Link | Description |
|------|-------------|
| [Ansible Docs](https://docs.ansible.com/) | Official documentation |
| [YAML Basics](https://yaml.org/start.html) | Learn YAML syntax |
| [Ansible Galaxy](https://galaxy.ansible.com/) | Community roles for reuse |

---

## Contributors

- Sonal
