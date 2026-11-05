# 🎯 LOOM Dashboard - Installation & Usage Guide

## Overview

The **LOOM Dashboard** is a self-contained, browser-based front-end for managing LOOM (Agent Operating System). It requires no backend server, no installation, and no build steps—just open the HTML file in your browser.

**Key Features:**
- ✅ Submit Intent Cards directly from the UI
- ✅ Approve/reject decisions with one click
- ✅ View Monday briefing with pending items
- ✅ Track project status and strategy
- ✅ Secure GitHub token storage (localStorage only)
- ✅ Responsive design (desktop, tablet, mobile)
- ✅ Dark mode support
- ✅ Real-time sync with GitHub repo

---

## Quick Start

### 1. **Download & Open**

The dashboard is a single HTML file: `loom-dashboard.html`

**To open it:**
- Save the file to your computer
- Double-click it to open in your default browser, OR
- Right-click → "Open with" → Choose your browser

**That's it.** No installation needed.

---

### 2. **Configure GitHub Token**

The dashboard needs access to your LOOM repository via GitHub API.

**Step 1: Create a Personal Access Token**
1. Go to [GitHub Settings → Tokens](https://github.com/settings/tokens)
2. Click **"Generate new token (classic)"**
3. Give it a name like `LOOM Dashboard`
4. Select these scopes:
   - ✅ `repo` (full control of private repositories)
   - ✅ `workflow` (update GitHub Action workflows)
5. Click **"Generate token"**
6. **Copy the token immediately** (you won't see it again)

**Step 2: Store Token in Dashboard**
1. Click **⚙️ Settings** button in the top right
2. Paste your GitHub token in the **"GitHub Personal Access Token"** field
3. Verify the **Repository URL** is correct (default: `WalkerJustin/loom`)
4. Click **"Save Settings"**

✅ Your token is now stored **locally in your browser only**. It is never sent anywhere else.

---

### 3. **Configure Settings** (Optional)

In the Settings modal:

| Setting | Description |
|---------|------------|
| **GitHub Repository URL** | Your LOOM repo (e.g., `WalkerJustin/loom`) |
| **GitHub Token** | Your personal access token from above |
| **Enable Notifications** | Show alerts for new decisions |
| **Auto-Refresh** | Automatically sync with GitHub every 5 minutes |

---

## Features & How to Use

### 📊 **Dashboard Tab**
Your overview of all LOOM activity.

- **Pending (DECIDE)** – Items requiring your approval decision
- **Pending (REVIEW)** – Information-sharing items you should be aware of
- **Pending (LOG)** – Items being recorded for history
- **Recent Activity** – Last 5 submissions

**Action:** Click refresh button (🔄 Sync) to manually update.

---

### ✍️ **Submit Intent Tab**
Create new Intent Cards without editing the GitHub repo.

**Required fields:**
- **Title** – Short name for this intent
- **Description** – What this is about
- **Room** – SPIN, PATTERN, WARP, WEAVE, or HARVEST
- **Tier** – DECIDE (needs approval), REVIEW (info share), or LOG (record)
- **Purpose** – Why are we doing this?
- **End State** – What does success look like?
- **Constraints** – Any limitations? (optional)

**Action:** Fill out the form and click **"Submit Intent Card"**
- This creates a GitHub issue automatically
- The issue is labeled with the tier and room
- It appears in the dashboard immediately

---

### ✅ **Approvals Tab**
Manage decisions that need your approval.

Shows all **DECIDE-tier** items waiting for action.

**For each item, you can:**
- **✓ Approve** – Accept the decision, close the issue
- **↩ Request Changes** – Ask for more work before approving
- **✗ Reject** – Decline the decision, close the issue

**Workflow:**
1. View the Intent Card details
2. Select approve/reject/request changes
3. Add optional reasoning in the prompt
4. Click the button
5. The issue is updated on GitHub automatically

---

### 📅 **Monday Brief Tab**
Your weekly priority summary.

Shows:
- **⚡ Decisions Required** – All DECIDE-tier items you need to approve
- **📌 Reviews** – Key REVIEW-tier items this week
- Clickable links to each issue for details

**Use this on Monday to:**
- See what decisions are waiting for you
- Prioritize your week
- Know what information you need to review

---

### 🚀 **Projects Tab**
Browse active projects and strategy.

Shows issues tagged with `project:` label, including:
- Project name and number
- Current status
- Links to full details

**To add projects to this view:**
- Create GitHub issues with the `project:` label
- They'll automatically appear in the dashboard

---

## Security & Privacy

### ✅ **What's Secure:**
- **GitHub token is stored locally only** – In your browser's localStorage
- **No backend server** – Everything runs in your browser
- **No data collection** – Nothing is sent anywhere except GitHub API calls
- **HTTPS only** – All GitHub API calls are encrypted

### ⚠️ **Things to Know:**
- If you clear your browser's cache/cookies, your token will be deleted
- Token is readable by JavaScript code on this page (standard browser limitation)
- **Do NOT share your browser session** with others; they could access your token
- If you suspect your token is compromised, regenerate it on GitHub immediately

### 🔐 **Best Practices:**
1. Use a **token with limited scope** (only `repo` and `workflow`)
2. **Regenerate tokens periodically** (e.g., every 90 days)
3. Use this dashboard on **trusted devices only**
4. Don't leave the browser open if you step away

---

## Troubleshooting

### ❌ "GitHub API error: 401"
- Token is expired or invalid
- Go to Settings, re-enter your token
- Verify token has not been revoked on GitHub

### ❌ "Cannot read property of undefined"
- Repository URL is incorrect
- Go to Settings, check the format: `owner/repo`
- Example: `WalkerJustin/loom`

### ❌ No issues appear in Dashboard
- Verify your token has `repo` scope
- Verify you're pointing to the correct repository
- Click 🔄 Sync to manually refresh
- Check GitHub to ensure issues exist

### ❌ Submissions fail silently
- Verify GitHub token in Settings
- Check browser console (F12) for error messages
- Ensure repository URL is correct

### 🔧 How to Debug
1. Open **Browser Developer Tools** (F12)
2. Go to **Console** tab
3. Check for red error messages
4. Copy errors and troubleshoot

---

## Tips & Tricks

### 💡 **Tip 1: Use Browser Bookmarks**
- Bookmark the dashboard for quick access
- Or create a desktop shortcut to the HTML file

### 💡 **Tip 2: Dark Mode**
- Click 🌙 Dark button in top right
- Preference is saved automatically

### 💡 **Tip 3: Mobile Usage**
- Dashboard is fully responsive
- Works great on tablets and phones
- Save as bookmark on phone home screen

### 💡 **Tip 4: Auto-Refresh**
- Enable "Auto-refresh" in Settings
- Dashboard syncs with GitHub every 5 minutes
- Great for background monitoring

### 💡 **Tip 5: Share with Team**
- This dashboard is for ONE user per browser
- Each team member should use their own GitHub token
- Or set up on a shared device with a shared token account

---

## File Structure

```
loom-dashboard.html       (Single self-contained file)
└─ Embedded CSS          (All styling)
└─ Embedded JavaScript   (All functionality)
└─ No external files needed
```

That's it. One file. Open it. Use it.

---

## Advanced: Deploying as a Web App

### Option 1: Personal Server
If you want to host it online:

1. Upload `loom-dashboard.html` to any web server
2. Access via: `https://yourserver.com/loom-dashboard.html`
3. Token is still stored locally (not affected)

### Option 2: GitHub Pages
1. Push `loom-dashboard.html` to a GitHub repo
2. Enable Pages in repo settings
3. Access via: `https://yourusername.github.io/repo/loom-dashboard.html`

### Option 3: AWS S3 + CloudFront
1. Upload to S3
2. Serve via CloudFront for caching
3. Use HTTPS only

**Note:** No matter where you host it, your token remains in your browser—never sent to the server.

---

## What's NOT Supported (Yet)

- ❌ Real-time notifications (check dashboard manually)
- ❌ Editing existing Intent Cards (create new ones)
- ❌ Complex filtering/search (basic view only)
- ❌ Integration with other tools (GitHub only)

These can be added if needed!

---

## Future Enhancements

Possible additions:
- 🔔 Real-time notifications via webhooks
- 📊 Analytics and metrics dashboards
- 🔍 Advanced search and filtering
- 📱 Native mobile app
- 🤖 AI-powered suggestions
- ↔️ Integration with Slack, Discord
- 🗂️ Custom workflows and automation

---

## Support & Feedback

**Found a bug?** Check the browser console (F12) for errors.

**Have a suggestion?** You can:
1. Edit the HTML yourself (it's just code)
2. Create an issue in your LOOM repo
3. Contact Justin or open a discussion

---

## License & Attribution

This dashboard is designed for the LOOM Agent Operating System.
- Created for: Justin Walker
- Purpose: Streamline LOOM interactions
- No external dependencies required

Happy decision-making! 🚀

---

**Last Updated:** November 2024
**Version:** 1.0
