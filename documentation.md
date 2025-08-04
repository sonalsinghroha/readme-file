

# VCS Authn & Authz Strategy – Notification Documentation

<img width="704" height="512" alt="image" src="https://github.com/user-attachments/assets/9dbeda3b-e6a1-42c0-8c0e-890241abd4cc" />


---

## Author Information

| **Created by** | **Created on** | **Version** | **Last Updated On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| -------------- | -------------- | ----------- | ------------------- | ---------------- | --------------- | --------------- | --------------- |
| Sonal          | 01-08-2025     | V 1.0       | 01-08-2025          | Anjali           |                 |                 |                 |

---

## Table of Contents

* [Introduction](#introduction)
* [Pre-requisites](#pre-requisites)
* [Step-by-Step Setup Guide *(Performed on GitHub)*](#step-by-step-setup-guide-performed-on-github)
* [Best Practices](#best-practices)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

## Introduction

This document is part of the **VCS Authn & Authz Strategy** and focuses on setting up notification systems in Version Control Systems like GitHub, GitLab, Bitbucket, and Azure DevOps. It includes the required pre-requisites, step-by-step configuration guides for **Email** and **Slack**, and best practices to ensure secure and effective alerting. These notifications help teams stay aware of key repository activities such as code changes, access events, and CI/CD pipeline status.

For a detailed overview of notification concepts and background, refer to the introduction guide [here](https://github.com/Snaatak-Cloudops-Crew/documentation/tree/SCRUM-99-Sonal/VCS/Notification-System/Introduction).

---

## Pre-requisites

| **Requirement**               | **Description**                                               |
| ----------------------------- | ------------------------------------------------------------- |
| **VCS Platform**              | GitHub, GitLab, Bitbucket, or Azure DevOps configured         |
| **Admin Access**              | Required to create webhooks or configure notification rules   |
| **Email Server or Chat Tool** | Configured for sending messages (e.g., SMTP, Slack, MS Teams) |
| **API/Webhook Token**         | For external integrations (if required)                       |
| **CI/CD System (Optional)**   | To link with deployment alerts                                |

---

## Step-by-Step Setup Guide *(Performed on GitHub)*

This section explains how to configure **Email** and **Slack** notifications within **GitHub**. Other platforms follow similar flows, but all steps and screenshot placements below are GitHub-specific.

---

### Email Notification Setup

**Step 1:** Navigate to your repository or project settings
Go to the main settings area of your GitHub repository.

> *Insert screenshot of GitHub repository settings*

**Step 2:** Find the “Notifications” or “Email Alerts” section
Locate the menu option related to notifications or integrations.

> *Insert screenshot of notification settings menu*

**Step 3:** Configure your SMTP server (if using GitHub Enterprise Server)
Make sure GitHub can send outbound email through an SMTP server.

> *Insert screenshot of SMTP config (Enterprise only)*

**Step 4:** Create a new email alert rule
Click on an option like “New Email Notification” or set rules via organization-level settings.

> *Insert screenshot of rule creation*

**Step 5:** Select trigger events
Choose events like:

* Push
* Pull/Merge requests
* Role/Permission changes
* Workflow or pipeline failures

> *Insert screenshot showing event checkboxes*

**Step 6:** Enter recipient email addresses
Add recipients manually or use a distribution list.

> *Insert screenshot showing recipient input*

**Step 7:** Customize subject/message (if supported)
Use tokens or templates for better formatting (optional).

> *Insert screenshot of customization field*

**Step 8:** Save and enable the rule
Click **Save**, **Enable**, or equivalent to activate it.

> *Insert screenshot of final save*

**Step 9:** Trigger a test event
Perform a test push or merge to verify email notification.

> *Insert screenshot of action*

**Step 10:** Check your inbox
Validate delivery, format, and correctness of content.

> *Insert screenshot of test email received*

---

### Slack Notification Setup

**Step 1:** Visit [Slack API Apps](https://api.slack.com/apps) and create a new app
Click **Create New App → From Scratch**, then name the app and select your workspace.

> *Insert screenshot of Slack app creation*

**Step 2:** Enable **Incoming Webhooks**
In the app features menu, toggle **Incoming Webhooks** ON.

> *Insert screenshot of enabling webhooks*

**Step 3:** Add a new webhook to your workspace
Click **Add New Webhook**, then select a channel to post messages to.

> *Insert screenshot of channel selection*

**Step 4:** Copy the generated webhook URL
You'll use this URL in GitHub to send messages.

> *Insert screenshot of webhook URL*

**Step 5:** Open your GitHub repository settings
Go to **Settings → Webhooks** in your repository.

> *Insert screenshot of GitHub webhook section*

**Step 6:** Add a new webhook
Paste the Slack webhook URL in the Payload URL field.

> *Insert screenshot of webhook creation in GitHub*

**Step 7:** Choose which events to trigger Slack messages
Examples include:

* Pushes
* Pull Requests
* Team or role changes
* CI/CD workflow events

> *Insert screenshot showing event selection*

**Step 8:** (Optional) Customize message formatting
If available, use Slack message blocks or raw JSON payloads.

> *Insert screenshot of advanced config (optional)*

**Step 9:** Save and activate the webhook
Click **Add Webhook** to complete the setup.

> *Insert screenshot of save action*

**Step 10:** Trigger a test event
Push code or open a pull request to trigger the notification.

> *Insert screenshot of test activity*

**Step 11:** Verify message in Slack
Check the selected Slack channel to confirm receipt.

> *Insert screenshot of Slack message received*

---

## Best Practices

| **Best Practice**                   | **Why It Matters**                                           |
| ----------------------------------- | ------------------------------------------------------------ |
| **Enable Only Relevant Events**     | Avoids noise and improves focus                              |
| **Use Secure Channels**             | Prevents leakage of sensitive data                           |
| **Define Notification Ownership**   | Ensures accountability for responding to alerts              |
| **Test Regularly**                  | Validates working setup and message formatting               |
| **Integrate with Monitoring Tools** | Allows central visibility with tools like Datadog or Grafana |
| **Log All Notifications**           | Useful for audits and incident investigations                |

---

## Conclusion

A well-configured notification system strengthens your VCS security posture by providing real-time alerts for critical events. Whether using **Email** or **Slack**, timely notifications help teams respond faster and maintain transparency over repository activity.

---

## Contact Information

| **Name** | **Email**                                                                     |
| -------- | ----------------------------------------------------------------------------- |
| Sonal    | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## References

| **Link**                                                                                                                                                                            | **Description**                    |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| [GitHub Notifications](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-email-preferences/setting-your-notification-preferences) | GitHub Notification Settings       |
| [GitLab Notifications](https://docs.gitlab.com/ee/user/profile/notifications.html)                                                                                                  | GitLab Notification Overview       |
| [Bitbucket Webhooks](https://support.atlassian.com/bitbucket-cloud/docs/manage-webhooks/)                                                                                           | Bitbucket Webhook Configuration    |
| [Azure DevOps Notifications](https://learn.microsoft.com/en-us/azure/devops/notifications/about-notifications)                                                                      | Azure DevOps Notification Settings |

---

