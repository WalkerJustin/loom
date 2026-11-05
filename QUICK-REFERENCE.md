# 🎯 LOOM Dashboard - Quick Reference Card

## 🚀 Get Started in 3 Steps

### Step 1️⃣ Open
- Double-click `loom-dashboard.html`
- Appears in your browser instantly

### Step 2️⃣ Configure Token
1. Click **⚙️ Settings** (top right)
2. Go to https://github.com/settings/tokens
3. Create new token with `repo` + `workflow` scopes
4. Paste token in Settings → Save

### Step 3️⃣ Start Using
- Submit Intent Cards via "Submit Intent" tab
- Approve decisions via "Approvals" tab
- View status in Dashboard
- Check Monday Brief for weekly summary

---

## 📋 Tabs Overview

| Tab | Purpose | Quick Action |
|-----|---------|--------------|
| **Dashboard** | See all pending items by tier | Click 🔄 to refresh |
| **Submit Intent** | Create new Intent Cards | Fill form → Submit |
| **Approvals** | Approve/reject DECIDE items | Click ✓/↩/✗ |
| **Monday Brief** | Weekly priority summary | Review pending decisions |
| **Projects** | Browse active projects | View project status |

---

## 🎯 Intent Card Template

When you submit, include:
```
Title:        "Update authentication flow"
Room:         PATTERN
Tier:         DECIDE (needs approval)
Purpose:      "Improve security and performance"
End State:    "OAuth 2.0 implemented, all tests pass"
Constraints:  "Must not break existing integrations"
```

---

## ✅ Decision Workflow

```
1. New Intent Card submitted (DECIDE tier)
   ↓
2. Appears in "Approvals" tab
   ↓
3. You review and choose:
   ✓ Approve → Issue closes
   ↩ Request Changes → Developer fixes
   ✗ Reject → Issue closes
   ↓
4. Decision is logged in GitHub
```

---

## 🔐 Security Checklist

- [ ] Token has limited scope (`repo` + `workflow` only)
- [ ] Token stored locally (not sent anywhere)
- [ ] Clear browser cache if leaving shared computer
- [ ] Regenerate token if compromised
- [ ] Use HTTPS if accessing remotely

---

## 🎨 Customization Tips

### Dark Mode
Click 🌙 Dark button → Preference saved

### Auto-Refresh
Settings → Enable "Auto-refresh" → Syncs every 5 min

### Repository URL
Settings → Change to any `owner/repo` format

---

## 🆘 Common Issues

| Issue | Solution |
|-------|----------|
| "GitHub API error: 401" | Token expired → regenerate on GitHub |
| No issues showing | Wrong repo URL → check Settings |
| Token lost after browser restart | Normal → re-enter in Settings |
| Slow to load | Check internet → Click 🔄 refresh |

---

## 📱 Browser Compatibility

✅ Works great in:
- Chrome/Edge (Recommended)
- Firefox
- Safari
- Mobile browsers (fully responsive)

---

## 💾 Data Storage

- **Stored Locally:** Token, repo URL, preferences
- **Stored on GitHub:** All Intent Cards, decisions, comments
- **Sent Nowhere Else:** Dashboard only talks to GitHub API

---

## 🔗 Useful Links

- Create GitHub Token: https://github.com/settings/tokens
- Your LOOM Repo: https://github.com/WalkerJustin/loom
- GitHub API Docs: https://docs.github.com/en/rest
- This Dashboard: Open `loom-dashboard.html`

---

## 🎯 Your Next Steps

1. ✅ Save `loom-dashboard.html` to your computer
2. ✅ Create GitHub personal access token
3. ✅ Open dashboard and configure token
4. ✅ Submit your first Intent Card
5. ✅ Test approval workflow
6. ✅ Bookmark for daily use

---

**Ready?** Open `loom-dashboard.html` now! 🚀

---

### Legend
- 📊 Dashboard = Status overview
- ✍️ Submit Intent = Create new cards
- ✅ Approvals = Decision management
- 📅 Monday Brief = Weekly summary
- 🚀 Projects = Active work tracking
- ⚙️ Settings = Configuration
- 🔄 Sync = Manual refresh
- 🌙 Dark = Theme toggle

---

**Questions?** Check LOOM-DASHBOARD-README.md for full documentation.
