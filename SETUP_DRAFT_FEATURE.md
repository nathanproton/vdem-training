# Setup: Save Draft to Repository Feature

This feature allows users to submit their event data back to the repository as timestamped drafts with password protection.

## Setup Steps

### 1. Create GitHub Secret for Password

1. Go to your repository: **https://github.com/nathanproton/vdem-training**
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **"New repository secret"**
4. Name: `DRAFT_PASSWORD`
5. Value: Choose a secure password (share this with authorized users)
6. Click **"Add secret"**

### 2. Create GitHub Personal Access Token

1. Go to: **https://github.com/settings/tokens**
2. Click **"Generate new token"** → **"Generate new token (classic)"**
3. Give it a name: `vdem-training-dispatch`
4. Set expiration: **No expiration** (or your preference)
5. Select scope: **ONLY** check `repo` → `public_repo` (if public repo)
   - OR check `repo` (full control) if private
6. Click **"Generate token"**
7. **COPY THE TOKEN** (you won't see it again!)

### 3. Update index.html with Token

1. Open `index.html`
2. Find line ~888:
   ```javascript
   'Authorization': 'Bearer YOUR_GITHUB_TOKEN_HERE',
   ```
3. Replace `YOUR_GITHUB_TOKEN_HERE` with your actual token:
   ```javascript
   'Authorization': 'Bearer ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxx',
   ```
4. Commit and push the change

### 4. Test the Feature

1. Visit: **https://nathanproton.github.io/vdem-training/**
2. Add or edit some events
3. Click **"Save Draft to Repository"**
4. Enter the password you set in step 1
5. Enter your name (optional)
6. Check the **Actions** tab for the workflow run
7. If successful, find your draft in the `drafts/` folder!

## How It Works

```
User clicks button
     ↓
Enters password
     ↓
Frontend sends to GitHub API
     ↓
Triggers repository_dispatch event
     ↓
Workflow validates password
     ↓
Saves JSON as drafts/events-YYYY-MM-DD_HH-MM-SS.json
     ↓
Commits to repository
```

## Security Notes

⚠️ **Important:**
- The GitHub token is **embedded in the HTML** (publicly visible)
- Token scope is **limited to triggering workflows only**
- **Actual security** comes from the password validation in the workflow
- Password is sent to GitHub (over HTTPS) and validated server-side
- Password is **never exposed** in the public HTML

## File Locations

- **Drafts saved to:** `drafts/events-YYYY-MM-DD_HH-MM-SS.json`
- **Workflow:** `.github/workflows/save-draft.yml`
- **Frontend code:** `index.html` (line ~862)

## Troubleshooting

**"Authentication failed"**
- Check that your GitHub token is valid
- Verify token has `public_repo` or `repo` scope

**Workflow doesn't run**
- Check the Actions tab for errors
- Verify `DRAFT_PASSWORD` secret is set correctly

**"Invalid password"**
- User entered wrong password
- Check workflow run logs in Actions tab

## Usage for End Users

1. Click **"Save Draft to Repository"**
2. Enter the password (get from admin)
3. Enter your name (optional)
4. Wait for confirmation message
5. Draft is saved with timestamp!

Your draft will be available at:
`https://github.com/nathanproton/vdem-training/tree/main/drafts`
