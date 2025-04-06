# 🧠 GithubDailyPush - n8n Workflow for Daily Workflow Backup

This n8n workflow automates daily backups of all your n8n workflows by pushing them to a specified GitHub repository and notifying you via email upon success or failure.

## 📌 Features

- 🔁 **Daily Scheduling** — Automatically runs every day at 4 AM UTC.
- 📤 **Push to GitHub** — Backs up each workflow as a JSON file to a GitHub repo.
- 🔂 **Loop through workflows** — Iterates through all workflows stored in your n8n instance.
- ✅ **Email Notification** — Sends a success message when complete.
- ❌ **Failure Notification** — Sends an error email if the GitHub push fails.

---

## 📦 Requirements

Before using this workflow, make sure you have:

- A running [n8n instance](https://docs.n8n.io).
- OAuth2 credentials configured for:
  - **GitHub**
  - **Gmail**
- A GitHub repository created to store workflow backups.
- Your email address added to the `SuccessMail` and `FailMail` nodes.

---

## ⚙️ Setup Instructions

### 1. 🔐 Connect Credentials

- **GitHub OAuth2**: Create a GitHub OAuth app and connect it to n8n under credentials.
- **Gmail OAuth2**: Set up Gmail OAuth2 credentials in n8n for sending emails.

### 2. 📝 Configure Email Address

Update the following nodes with your email:

- `SuccessMail` → `sendTo`
- `FailMail` → `sendTo`

### 3. 📂 GitHub Repository Setup

Make sure your GitHub repository exists. In this workflow, it's set to:

```plaintext
https://github.com/neverbend007/n8nWorkflowsBackup
```

Each backed-up file will be stored under:
```
docs/YYYY-MM-DD/<workflow-name>.json
```

With the commit message as the date:
```
YYYY-MM-DD
```

### 4. 🕓 Scheduled Execution

The workflow is triggered daily at **4 AM UTC** via the `Schedule Trigger` node. You can also run it manually using the `Manual Trigger`.

---

## 🧭 Workflow Flow

```
Schedule Trigger (4AM)
      ↓
  Fetch All Workflows (n8n API)
      ↓
  Loop Over Each Workflow
      ↓
  ┌────→ Push to GitHub
  │       ↓
  │   On Success → Loop Ends
  │
  └────→ On Failure → Send FailMail
      ↓
All Pushed? → Send SuccessMail
```

---

## 📧 Email Messages

### ✅ On Success:
Subject: `n8n Workflows Backed Up Successfully`  
Body: `Breathe easy! :)`

### ❌ On Failure:
Subject: `n8n Workflow - Github save failed`  
Body:
```
Look at your workflow here: https://neverbend007.app.n8n.cloud/workflow/iKRlNEduQ9GTy5XV
```

---

## 🛠 Customization

- **Change the backup folder**: Modify `filePath` in the GitHub node.
- **Customize messages**: Edit `subject` and `message` in the Gmail nodes.
- **Adjust schedule**: Modify the `Schedule Trigger` to run at your desired time.

---

## 🧪 Testing

To test manually:

1. Open the workflow in n8n.
2. Click `Execute Workflow`.
3. Check your GitHub repo and email for confirmation.

---

## 🧠 Tips

- Set up retry logic in GitHub node for more resilience.
- You can use tags or filters in the `n8n` node to back up only specific workflows.
- Use a `.gitignore` in the GitHub repo to exclude anything you don’t want tracked.

---

## 📞 Support

If you run into issues, check:

- n8n logs and error messages.
- OAuth2 credentials.
- GitHub token scopes (must allow repo access).
- Gmail settings (check spam folder or email limits).

---

Enjoy the peace of mind with automatic backups! 💾🔒

---
