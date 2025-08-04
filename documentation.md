

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


><img width="1063" height="403" alt="Screenshot 2025-08-04 173252" src="https://github.com/user-attachments/assets/458e6bd4-14ad-456c-b16a-88b237266509" />


###  Summary

| Scope                | Purpose                                                                        |
| -------------------- | ------------------------------------------------------------------------------ |
| **Account Level**    | Get notified about PRs, issues, comments, and mentions across all repositories |
| **Repository Level** | Get notified when someone pushes to a specific repository                      |


---

### Slack Notification Setup

**Step 1:** Visit [https://api.slack.com/apps](https://api.slack.com/apps) and create a new app for GitHub
Click **Create New App → From Scratch**, and select your Slack workspace.

> Create Slack App <img width="1201" height="283" alt="Screenshot 2025-08-04 173504" src="https://github.com/user-attachments/assets/be4df036-a373-4717-8811-ae9b1a54174b" />

---

**Step 2:** Integrate Slack with GitHub by authorizing access
Log in with your GitHub credentials, complete OTP verification, and authorize the Slack app.

 GitHub Login
> <img width="878" height="520" alt="Screenshot 2025-08-04 143220" src="https://github.com/user-attachments/assets/f51455a6-7eb7-444d-bcc2-507469c90090" />



 GitHub Two-Factor Authentication 
 ><img width="809" height="594" alt="Screenshot 2025-08-04 143233" src="https://github.com/user-attachments/assets/fe6d6543-c687-4e0a-a807-56ec396e269a" />

 Select GitHub Organization for Access
> <img width="781" height="598" alt="Screenshot 2025-08-04 143409" src="https://github.com/user-attachments/assets/fa06cf11-d640-44f7-8993-6086a991c30c" />

 Confirm GitHub App Authorization 
 ><img width="809" height="408" alt="Screenshot 2025-08-04 143437" src="https://github.com/user-attachments/assets/a59f1d99-79c6-4e76-9457-a863f1ad3063" />



---

**Step 3:** Subscribe your GitHub repository to a Slack channel
Go to the Slack channel and run the subscribe command:

```bash
/github subscribe owner/repo
```

Example:

```bash
/github subscribe sonalsinghroha/newone
```

 Type the subscription command
 ><img width="529" height="224" alt="Screenshot 2025-08-04 175046" src="https://github.com/user-attachments/assets/7ca84eb5-9703-4e84-9406-9af718da16d1" />

 Grant access permission to Slack app 
 ><img width="823" height="434" alt="Screenshot 2025-08-04 175555" src="https://github.com/user-attachments/assets/332519ac-2431-435d-b4ca-6faea6191fb5" />

 Confirmation of successful subscription and commit notification in Slack
 ><img width="741" height="290" alt="Screenshot 2025-08-04 175219" src="https://github.com/user-attachments/assets/46d7f0a5-7467-4ddc-a278-62a3a0add7b2" />


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

