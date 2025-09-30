# Setup: Save Draft to Repository Feature

This feature allows users to submit their event data back to the repository as timestamped drafts with password protection.

## 🔒 Security Model

- **GitHub Token**: User-configurable, stored in browser localStorage only
- **Draft Password**: Validated by GitHub Actions workflow server-side
- **No secrets in code**: Everything stored securely

## Setup Steps (Administrator)

### 1. Create GitHub Secret for Draft Password

1. Go to: **https://github.com/nathanproton/vdem-training/settings/secrets/actions**
2. Click **"New repository secret"**
3. Name: `DRAFT_PASSWORD`
4. Value: Choose a secure password (you'll share this with authorized users)
5. Click **"Add secret"**

### 2. Create a GitHub Personal Access Token (to share with users)

**Option A: Single Shared Token (Easier)**
1. Go to: **https://github.com/settings/tokens**
2. Click **"Generate new token (classic)"**
3. Name: `vdem-training-shared`
4. Expiration: Set as needed
5. Scope: Check **ONLY** `public_repo` (minimal permissions)
6. Click **"Generate token"**
7. **Copy and securely share this token** with authorized users

**Option B: Individual User Tokens (More Secure)**
- Each user creates their own token
- Better audit trail
- Users follow same steps above

### 3. Share Credentials with Users

Send to authorized users:
- **GitHub Token**: `ghp_xxxxxxxxxxxxxxxxxxxx`
- **Draft Password**: `YourSecurePassword123`
- **Instructions**: See "For End Users" section below

## For End Users

### First-Time Setup

1. Visit: **https://nathanproton.github.io/vdem-training/**
2. Click **"Settings"** to expand
3. Paste your **GitHub token** in the field
4. Click **"Save Token"**
5. Done! You're ready to submit drafts

### Submitting a Draft

1. Add or edit your events
2. Click **"Save Draft to Repository"**
3. Enter the **draft password** (provided by administrator)
4. Enter your name (optional)
5. Wait for confirmation message
6. Check the **Actions** tab to see the workflow run!

### Your draft will be saved to:
`drafts/events-YYYY-MM-DD_HH-MM-SS.json`

View all drafts: **https://github.com/nathanproton/vdem-training/tree/main/drafts**

## How It Works

```
┌─────────────────────┐
│  User configures    │
│  token in Settings  │
│  (stored in browser)│
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  User clicks        │
│  "Save Draft"       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Enter password     │
│  Enter name         │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Browser sends to   │
│  GitHub API         │
│  (using user token) │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Workflow triggered │
│  Validates password │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Saves JSON draft   │
│  Commits to repo    │
└─────────────────────┘
```

## Security Features

✅ **Token in browser only** - Never in HTML source  
✅ **Password validated server-side** - Can't be bypassed  
✅ **HTTPS encryption** - Secure transmission  
✅ **Limited token scope** - Only triggers workflows  
✅ **Audit trail** - Who submitted what and when  
✅ **Timestamped** - No overwrites, full history  

## Troubleshooting

### "Please configure your GitHub token first"
- Go to Settings
- Paste your token
- Click Save Token

### "Invalid GitHub token"
- Token may be expired or revoked
- Check token scope includes `public_repo`
- Create a new token

### "Failed to save draft"
- Check your internet connection
- Verify repository is accessible
- Check Actions tab for workflow errors

### Workflow doesn't run
- Verify `DRAFT_PASSWORD` secret is set in repository
- Check token has correct permissions
- View workflow logs in Actions tab

## Token Permissions

The GitHub token needs **minimal permissions**:
- For **public repositories**: `public_repo` scope only
- For **private repositories**: `repo` scope (full control)

The token can **ONLY**:
- Trigger the `save-draft` workflow
- Cannot push code directly
- Cannot modify repository settings
- Cannot access other repositories

## Data Privacy

- **GitHub Token**: Stored in user's browser localStorage only
- **Events Data**: Sent directly to GitHub API over HTTPS
- **No third-party services**: Direct browser → GitHub communication
- **No tracking**: No analytics or data collection

## Revoking Access

**To revoke a user's access:**
1. Change the `DRAFT_PASSWORD` secret
2. Or revoke their GitHub token at: https://github.com/settings/tokens

**User can clear their own token:**
- Settings → "Clear Token" button

## Cost

- **GitHub Pages**: FREE
- **GitHub Actions**: FREE (2000 minutes/month)
- **No serverless costs**: Works entirely on GitHub infrastructure
- **Total**: $0/month ✨