# VCS Policies - Documetation

## Author Information

| Created by | Created on | Version | Last Updated On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------- | ---------- | ------- | --------------- | ------------ | ----------- | ----------- | ----------- |
| Sonal      | 28-07-2025 | V 1.0   | 28-07-2025      | Prashant     |             |             |             |

---

## Table of Contents

* [Introduction](#introduction)
* [What are Branch Access Policies?](#what-are-branch-access-policies)
* [Why Branch Access Policies are Important](#why-branch-access-policies-are-important)
* [Prerequisites](#prerequisites)
* [Types of Access Policies](#types-of-access-policies)
* [Branch Protection Rules](#branch-protection-rules)
* [Access Control by Platform](#access-control-by-platform)
* [How to Implement Branch Access Policies](#how-to-implement-branch-access-policies)
* [Best Practices](#best-practices)
* [Common Mistakes](#common-mistakes)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

## Introduction


This document is part of the **VCS Policies** initiative, specifically focused on defining and documenting **Branch Access Policies**. These policies are essential for managing secure and collaborative workflows in modern version control systems (VCS) such as GitHub, GitLab, Bitbucket, and Azure DevOps.

The goal of branch access policies is to control who can push, merge, or delete branches, and under what conditions. This includes implementing **Branch Protection Rules**-a critical feature used to prevent unauthorized changes, enforce peer review, and maintain code quality before merging changes into protected branches like `main`, `develop`, or `release`.


---

## What are Branch Access Policies?

Branch access policies are configurations set on repositories that control actions like pushing, merging, or deleting branches. These ensure that:

* Only authorized users can make changes
* Pull Requests (PRs) are reviewed and approved
* Code meets CI/CD requirements
* Accidental or malicious changes are avoided

They form a subset of the broader VCS security and compliance strategies.

---

## Why Branch Access Policies are Important

| Reason                        | Explanation                                                              |
| ----------------------------- | ------------------------------------------------------------------------ |
| Maintain Code Integrity       | Avoids accidental changes to production or critical code                 |
| Enforce Review Process        | Ensures peer review, reducing bugs and improving collaboration           |
| Enable CI/CD Quality Gates    | Prevents broken or untested code from being merged                       |
| Limit Access to Trusted Users | Only authorized developers can modify protected branches                 |
| Support Regulatory Compliance | Ensures auditable and secure change management in regulated environments |

---

## Prerequisites

* A version control platform (e.g., GitHub, GitLab, Bitbucket, Azure DevOps)
* Defined branching model (e.g., Git Flow, trunk-based)
* Project roles and team structure (Admin, Developer, Reviewer, etc.)
* CI/CD pipeline integration (optional but recommended)
* Admin access to configure policies

---

## Types of Access Policies

| Policy Type             | Description                                                                 |
| ----------------------- | --------------------------------------------------------------------------- |
| Role-Based Access       | Assigns users roles like Read, Write, Admin based on their responsibilities |
| Branch-Level Controls   | Restrict pushing/merging/deleting to specific branches                      |
| Review & Approval Rules | Require reviews before merging, often from specific CODEOWNERS              |
| Commit Signing          | Require GPG-signed commits for verification                                 |
| CI/CD Status Checks     | Require builds, tests, and other checks to pass before merging              |
| Force Push Prevention   | Disallows rewriting history of important branches                           |
| Conditional Access      | Enforces access based on IP, device, SSO, or time                           |

---

## Branch Protection Rules

Branch Protection Rules ek tarah ka **security mechanism** hai jo Git-based version control systems mein use hota hai. Ye rules ensure karte hain ki sensitive ya critical branches jaise `main`, `release`, ya `production` par sirf authorized users hi changes kar sakein, woh bhi specific conditions ko fulfill karne ke baad.

### What are Branch Protection Rules?

Branch protection rules ek set of conditions hote hain jo kisi particular branch (ya branch pattern) par apply kiye jaate hain. Inka goal hota hai unauthorized access, accidental deletion, aur faulty code ke merge ko rokna.

### Why Use Branch Protection Rules?

| Reason                          | Explanation                                                        |
| ------------------------------- | ------------------------------------------------------------------ |
| Code ka integrity banaye rakhna | Prevents accidental ya malicious changes                           |
| Quality assurance               | Ensures ki code review aur testing ho pehle                        |
| Secure deployment               | Only approved changes hi production mein jaayein                   |
| Accountability                  | Sabhi changes trackable aur auditable hote hain                    |
| Automation integration          | CI/CD tools ke sath integrate karke workflows ko enforce karta hai |

### Common Protection Rules

| Rule                       | Description                                                      |
| -------------------------- | ---------------------------------------------------------------- |
| **Require Pull Requests**  | Direct push disallow karta hai; PR ke through hi changes aayengi |
| **Require Approvals**      | Minimum 1 ya zyada reviewers se approval lena zaroori hota hai   |
| **Required Status Checks** | CI tests, linting, ya builds pass hone chahiye merge se pehle    |
| **Require Signed Commits** | Har commit GPG sign hona chahiye (verification ke liye)          |
| **Prevent Force Push**     | History rewrite se rokta hai, jo data loss ka risk hota hai      |
| **Prevent Deletion**       | Branch accidentally delete na ho iske liye safeguard             |
| **Include Administrators** | Admins bhi rules bypass nahi kar sakte agar ye enabled ho        |

---

## Access Control by Platform

| Platform         | Method                            | Key Features                                                     |
| ---------------- | --------------------------------- | ---------------------------------------------------------------- |
| **GitHub**       | Branch protection rules, rulesets | CODEOWNERS, reviews, status checks, signed commits, admins rules |
| **GitLab**       | Protected branches, merge rules   | Role-based access, approval rules, push/merge/delete permissions |
| **Bitbucket**    | Branch permissions                | Restrict actions per user/group; use Pipelines for checks        |

---

## How to Implement Branch Access Policies

1. **Identify Critical Branches**: e.g., `main`, `release/*`, `hotfix/*`
2. **Define Roles & Responsibilities**: Determine who can write, review, and approve
3. **Enable Branch Protection**:

   * In GitHub: Settings > Branches > Add Rule
   * In GitLab: Repository > Branches > Protect
4. **Set Review Requirements**: Enforce PR approvals and CODEOWNERS
5. **Add CI/CD Checks**: Integrate tests, linting, and deployments as blockers
6. **Restrict Actions**: Disable force pushes and deletions
7. **Enforce for Admins**: Apply rules to everyone, including admins

---

## Best Practices

* Use wildcard patterns to apply consistent rules across many branches
* Automate rule enforcement using repository templates or API scripts
* Include a `CODEOWNERS` file to specify required reviewers
* Lock down release and production branches tightly
* Require up-to-date branches before allowing merges
* Document branch policies in your team or project wiki

---

## Common Mistakes

| Mistake                    | Problem Caused                                  |
| -------------------------- | ----------------------------------------------- |
| No Review Enforcement      | Allows risky or unapproved changes to be merged |
| Ignoring Status Checks     | May introduce broken or insecure code           |
| Using force push on `main` | Can rewrite history and lose critical data      |
| Incomplete branch patterns | Policy may not cover all relevant branches      |
| Skipping admin enforcement | Allows policy bypass by privileged users        |

---

## Conclusion

Branch access policies are a vital subset of Project VCS Policies. They improve code quality, reduce risk, and promote collaboration by enforcing strict controls on how branches can be modified, reviewed, and merged. Combined with branch protection rules and role-based access, they form the foundation of secure and scalable development workflows.

---

## Contact Information

| Name  | Email                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Sonal | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## References

| Link                                                                                                                            | Description                    |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| [GitHub Docs](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-branch-rules) | GitHub Branch Protection Rules |
| [GitLab Docs](https://docs.gitlab.com/ee/user/project/repository/branches/protected_branches.html)                              | GitLab Protected Branches      |
| [Bitbucket Docs](https://support.atlassian.com/bitbucket-cloud/docs/enforce-branch-permissions/)                                | Bitbucket Branch Permissions   |
