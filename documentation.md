

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

###  Email Notification Setup

---

###  **Account Level Notification Setup**



**Step 1:** Go to your GitHub account settings
Click your **profile icon → Settings** from the top-right corner of GitHub.

> <img width="364" height="434" alt="Screenshot 2025-08-04 170448" src="https://github.com/user-attachments/assets/6ab70718-6ece-42d6-93f1-2bd8f704f3fc" />



**Step 2:** Open the Notifications tab
In the left sidebar, click **Notifications** to access email settings.

> <img width="883" height="427" alt="Screenshot 2025-08-04 170629" src="https://github.com/user-attachments/assets/780a3873-5c18-4699-800b-f8607e57b3f5" />



**Step 3:** Set your default email address
Under **Default notifications email**, add or verify your preferred email address.

> <img width="891" height="211" alt="Screenshot 2025-08-04 170725" src="https://github.com/user-attachments/assets/db07f96f-ba29-4a2e-918a-9193585598d1" />




**Step 4:** Enable notifications for watched repositories
Under **Watching**, click **“Notify me: Email”** to receive emails about repositories you watch.

> <img width="767" height="279" alt="Screenshot 2025-08-04 170829" src="https://github.com/user-attachments/assets/8b2a869a-881f-44d2-b98f-c27404502f77" />




**Step 5:** Enable participation and mention alerts
Under **Participating, @mentions**, click **“Notify me: Email”** to get emails when you're tagged or involved in threads.

> <img width="736" height="260" alt="Screenshot 2025-08-04 170844" src="https://github.com/user-attachments/assets/f8d9ae02-6eea-4547-8420-604f13131380" />




**Step 6:** Customize which events trigger emails
Click **Customize email updates**, then select the events you want:

* Pull Request reviews
* Pull Request pushes
* Comments on issues and PRs
* (Optional) Include your own updates

Click **Save** after selecting.

> <img width="775" height="308" alt="Screenshot 2025-08-04 170946" src="https://github.com/user-attachments/assets/9650a996-cfb1-4ad6-9830-9e0c16d1095c" />





###  **Repository Level Notification Setup**

---

**Step 1:** Open the repository where you want push notifications
Go to the specific repository you want notifications from.



**Step 2:** Go to repository settings
Click the **Settings** tab in the repository navigation menu.

> <img width="1017" height="319" alt="Screenshot 2025-08-04 165351" src="https://github.com/user-attachments/assets/b04d111d-f70e-4fa1-b7a7-da3fbd95a575" />




**Step 3:** Navigate to Email notifications
In the left menu under **Integrations**, click **Actions → Email notifications**.

> ![1stgfd](https://github.com/user-attachments/assets/a0ccba37-03ab-489f-8898-9fe72caf6d34)




**Step 4:** Configure the notification fields

* **Address**: Enter one or two space-separated email addresses
* **Approved header**: Leave blank unless using a mailing list
* **Active**: Check this box to enable notifications

> <img width="944" height="414" alt="Screenshot 2025-08-04 165615" src="https://github.com/user-attachments/assets/81647f8e-b9a3-4469-9ed2-8f3d611d7b03" />




**Step 5:** Save the configuration
Click **Setup notifications** to apply your changes.

> <img width="1147" height="348" alt="Screenshot 2025-08-04 162104" src="https://github.com/user-attachments/assets/8bc9a08f-5309-4239-be19-81d0a6ded091" />




###  Summary

| Scope                | Purpose                                                                        |
| -------------------- | ------------------------------------------------------------------------------ |
| **Account Level**    | Get notified about PRs, issues, comments, and mentions across all repositories |
| **Repository Level** | Get notified when someone pushes to a specific repository                      |


---

### Slack Notification Setup

**Step 1:** Visit [Slack API Apps](https://api.slack.com/apps) and create a new app
Click **Create New App → From Scratch**, then name the app and select your workspace.

> Insert screenshot of Slack app creation

---

**Step 2:** Enable Incoming Webhooks
In the app features menu, toggle **Incoming Webhooks** ON.

> Insert screenshot of enabling webhooks

---

**Step 3:** Add a new webhook to your workspace
Click **Add New Webhook**, then select a channel to post messages to.

> Insert screenshot of channel selection

---

**Step 4:** Copy the generated webhook URL
You'll use this URL in GitHub to send messages.

> Insert screenshot of webhook URL

---

**Step 5:** Open your GitHub repository settings
Go to **Settings → Webhooks** in your repository.

> Insert screenshot of GitHub webhook section

---

**Step 6:** Add a new webhook
Paste the Slack webhook URL in the **Payload URL** field.
Set **Content type** to `application/json`.
(Optional) Set a secret for added security.

> Insert screenshot of webhook creation in GitHub

---

**Step 7:** Choose which events to trigger Slack messages
Examples include:

* Pushes
* Pull Requests
* Issues
* Workflow runs (CI/CD)
* Deployments

> Insert screenshot showing event selection

---

**Step 8:** (Optional) Customize message formatting
By default, GitHub sends full JSON payloads.
To format messages or filter events, use a middleware like Zapier, n8n, or a custom function.

> Insert screenshot of advanced config (optional)

---

**Step 9:** Save and activate the webhook
Click **Add Webhook** to complete the setup.
GitHub will send a ping to verify.

> Insert screenshot of save action

---

**Step 10:** Trigger a test event
Push code or open a pull request to trigger the notification.

> Insert screenshot of test activity

---

**Step 11:** Verify message in Slack
Check the selected Slack channel to confirm the notification appears.

> Insert screenshot of Slack message received



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

