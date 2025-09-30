# GitHub Actions Workflows

## Fetch VDEM Training Data

This workflow automatically fetches training event data from the VDEM website and updates `import-data.json`.

### How It Works

1. **Fetches** the VDEM training schedule page
2. **Parses** the `<meta name="type">` tag
3. **Decodes** HTML entities (`&#x22;` → `"`)
4. **Fixes** malformed JSON (removes extra commas)
5. **Updates** `import-data.json` in the repository
6. **Commits** changes automatically

### Schedule

- Runs **daily at 6 AM UTC** (1 AM EST / 2 AM EDT)
- Can also be **manually triggered** from the Actions tab

### Manual Trigger

1. Go to **Actions** tab in GitHub
2. Select **"Fetch VDEM Training Data"**
3. Click **"Run workflow"**
4. Select branch `main`
5. Click **"Run workflow"** button

### Benefits

✅ **No CORS issues** - Runs server-side
✅ **Automatic updates** - Keeps data fresh
✅ **Version controlled** - All changes tracked in Git
✅ **Manual override** - Trigger anytime you need

### Monitoring

Check the workflow runs in the **Actions** tab to see:
- When it last ran
- If it succeeded or failed
- What changes were made
