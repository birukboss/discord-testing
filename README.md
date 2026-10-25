# discord-testing

Use a webhook-based **Discord message** action (such as `appleboy/discord-action`). It is the standard choice for CI/CD notifications because it requires zero bot code or OAuth permissions—just a simple webhook URL.

### Setup Guide

1. **Create a Discord Webhook:**
* Go to your Discord server channel settings ➔ **Integrations** ➔ **Webhooks** ➔ **New Webhook**.
* Copy the generated **Webhook URL**.


2. **Add to GitHub Secrets:**
* In your GitHub repository, go to **Settings** ➔ **Secrets and variables** ➔ **Actions**.
* Create a new repository secret named `DISCORD_WEBHOOK` and paste your webhook URL.


3. **Add the Workflow Step:**
Add the following step to your workflow file (e.g., `.github/workflows/deploy.yml`):

```yaml
name: CI/CD Pipeline

on: [push]

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Send Discord Notification
        uses: appleboy/discord-action@v1.2.0
        with:
          webhook_url: ${{ secrets.DISCORD_WEBHOOK }}
          message: "Workflow finished successfully for commit: ${{ github.sha }}"

```
