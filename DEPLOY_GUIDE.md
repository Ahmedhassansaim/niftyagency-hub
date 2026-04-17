# NiftyCode Agency Hub — Complete Deployment Guide

---

## Architecture Overview

```
┌──────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   GitHub     │────▸│  GitHub Pages    │◂────│  Your Domain    │
│  (code repo) │     │  (free hosting)  │     │  ops.nifty.com  │
└──────────────┘     └──────────────────┘     └─────────────────┘
```

Your single `index.html` file lives on GitHub, is hosted free via GitHub Pages, and you can connect any custom domain to it.

---

## PART 1 — Store on GitHub

### Step 1: Create a GitHub Account (skip if you have one)

1. Go to **github.com** → click **Sign up**
2. Follow the prompts (email, password, username)
3. Verify your email

### Step 2: Create a Repository

1. Click the **+** icon (top-right) → **New repository**
2. Fill in:
   - **Repository name:** `agency-hub` (or whatever you prefer)
   - **Description:** `NiftyCode Agency Operations Hub`
   - **Visibility:** **Public** (required for free GitHub Pages)
   - ✅ Check **"Add a README file"**
3. Click **Create repository**

### Step 3: Upload Your File

1. In your new repo, click **Add file** → **Upload files**
2. Drag and drop the `index.html` file from your computer
3. In the commit message box, type: `Initial upload`
4. Click **Commit changes**

✅ Your code is now stored on GitHub!

---

## PART 2 — Host on GitHub Pages (Free)

### Step 4: Enable GitHub Pages

1. In your repo, click **Settings** (gear icon in the top bar)
2. In the left sidebar, scroll down and click **Pages**
3. Under **"Build and deployment"**:
   - **Source:** select **Deploy from a branch**
   - **Branch:** select **main**
   - **Folder:** select **/ (root)**
4. Click **Save**

### Step 5: Wait for Deployment

1. Wait 1–2 minutes
2. Go back to **Settings → Pages**
3. You'll see a green banner:
   **"Your site is live at https://YOUR-USERNAME.github.io/agency-hub/"**
4. Click the link — your app is live!

### Your Default URL

```
https://YOUR-USERNAME.github.io/agency-hub/
```

You can bookmark this and use it immediately. But if you want a custom domain, continue below.

---

## PART 3 — Connect a Custom Domain (Optional)

You can use any domain you own (e.g., `ops.niftycode.com` or `hub.youragency.com`).

### Option A: Subdomain (Recommended — e.g., ops.niftycode.com)

#### Step 6A: Add CNAME Record at Your Domain Registrar

1. Log in to your domain registrar (Namecheap, GoDaddy, Cloudflare, etc.)
2. Go to **DNS Settings** for your domain
3. Add a new record:

   | Type    | Host/Name | Value                            | TTL  |
   |---------|-----------|----------------------------------|------|
   | CNAME   | ops       | YOUR-USERNAME.github.io          | Auto |

   - Replace `ops` with whatever subdomain you want
   - Replace `YOUR-USERNAME` with your actual GitHub username

4. Save the record

#### Step 7A: Tell GitHub About Your Domain

1. Go to your repo → **Settings** → **Pages**
2. Under **"Custom domain"**, type your full subdomain:
   ```
   ops.niftycode.com
   ```
3. Click **Save**
4. ✅ Check **"Enforce HTTPS"** (may take a few minutes to appear)

#### Step 8A: Create CNAME File

1. In your repo, click **Add file** → **Create new file**
2. Name it: `CNAME` (all caps, no extension)
3. Content — just your domain on one line:
   ```
   ops.niftycode.com
   ```
4. Commit the file

### Option B: Root Domain (e.g., niftycode.com)

#### Step 6B: Add A Records at Your Registrar

Add these **4 A records** pointing to GitHub's servers:

| Type | Host/Name | Value             |
|------|-----------|-------------------|
| A    | @         | 185.199.108.153   |
| A    | @         | 185.199.109.153   |
| A    | @         | 185.199.110.153   |
| A    | @         | 185.199.111.153   |

Then follow Steps 7A and 8A above but with your root domain.

### DNS Propagation

After setting DNS records, wait **10 minutes to 48 hours** for propagation. Usually it's under 30 minutes.

To check if it's working:
```
https://ops.niftycode.com
```

---

## PART 4 — Future Updates

### How to Update Your App

Whenever you get an updated `index.html`:

1. Go to your GitHub repo
2. Click on `index.html`
3. Click the **pencil icon** (Edit this file) or **"..."** → **Delete** then re-upload
4. For easiest re-upload: **Add file** → **Upload files** → drag the new `index.html` → check **"Commit directly to main"** → Commit

GitHub Pages will auto-redeploy in ~1 minute.

---

## PART 5 — Data Management

### How Data Works

| Feature | How It Works |
|---------|-------------|
| **Storage** | Browser localStorage (saved on your device) |
| **Persistence** | Data stays even after closing browser |
| **Multi-device** | Use Export/Import to move data between devices |
| **Backup** | Click **↓ Export** in the app header → saves a `.json` file |
| **Restore** | Click **↑ Import** → select your `.json` backup |

### Backup Recommendations

- Export a backup **at least weekly**
- Export before clearing browser data
- Keep backups in Google Drive or Dropbox

### What Clears localStorage

- Manually clearing browser data/cache
- Using incognito/private mode (data won't persist)
- Switching browsers or devices

---

## Quick Reference Card

| Task | Where | What to Do |
|------|-------|------------|
| **View your app** | Browser | Go to your GitHub Pages URL or custom domain |
| **Update the app** | GitHub | Upload new `index.html`, auto-deploys in ~1 min |
| **Backup data** | App header | Click ↓ Export |
| **Restore data** | App header | Click ↑ Import → select JSON file |
| **Change domain** | GitHub Settings → Pages | Update custom domain field |
| **Check deploy status** | GitHub repo → Actions tab | Green ✓ = deployed |

---

## Troubleshooting

**"404 - Page not found"**
→ Make sure the file is named exactly `index.html` (lowercase) and is in the root of the repo, not inside a folder.

**Custom domain not working**
→ DNS can take up to 48 hours. Check that your CNAME file exists in the repo and matches exactly what you entered in Settings → Pages.

**"HTTPS not available"**
→ Wait 15-30 minutes after setting up the custom domain. GitHub needs time to issue the SSL certificate.

**Data disappeared**
→ You may have cleared browser data. Use ↑ Import with your most recent backup JSON file.
