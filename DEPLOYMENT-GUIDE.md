# 🚀 LOOM Dashboard - Deployment & Hosting Guide

## Overview

The LOOM Dashboard is a **single HTML file** that requires no backend, no build process, and no deployment complexity. You can:

1. **Open locally** – Double-click the file on your computer
2. **Share via file** – Email the HTML file to teammates
3. **Host online** – Put it on any web server
4. **GitHub Pages** – Deploy to GitHub for free
5. **Corporate intranet** – Host behind your firewall

---

## 📋 Deployment Checklist

- [ ] You have `loom-dashboard.html` file
- [ ] You have a GitHub personal access token
- [ ] You know your LOOM repo URL (e.g., `WalkerJustin/loom`)
- [ ] Choose deployment method below

---

## 🏠 Option 1: Local Deployment (Easiest)

**Best for:** Personal use, testing, no internet needed

### Steps:
1. Download `loom-dashboard.html`
2. Save to your computer (e.g., Desktop, Documents)
3. Double-click the file
4. Browser opens automatically
5. Configure GitHub token in Settings
6. Start using!

### Pros:
- ✅ No internet required
- ✅ Instant load time
- ✅ Most secure (token never leaves computer)
- ✅ Works offline (except GitHub syncing)

### Cons:
- ❌ Only works on your local computer
- ❌ Can't access from other devices

### Browser Bookmarks:
- Right-click file → "Create shortcut" (Windows)
- Drag to dock (Mac)
- Pin to home screen (Mobile)

---

## 🌐 Option 2: GitHub Pages (Free & Easy)

**Best for:** Team sharing, public access, free hosting

### Prerequisites:
- GitHub account
- A public repository (or private with Pages enabled)

### Steps:

#### Step 1: Upload to GitHub
```bash
# Option A: Via GitHub Web UI
1. Go to your repo: github.com/yourusername/yourrepo
2. Click "Add file" → "Upload files"
3. Drag `loom-dashboard.html` to upload
4. Commit with message "Add LOOM Dashboard"

# Option B: Via Git
git add loom-dashboard.html
git commit -m "Add LOOM Dashboard"
git push
```

#### Step 2: Enable GitHub Pages
1. Go to repo Settings → Pages
2. Source: Select branch (main/master)
3. Folder: / (root)
4. Save

#### Step 3: Access Your Dashboard
- URL: `https://yourusername.github.io/yourrepo/loom-dashboard.html`
- Example: `https://walkerjustin.github.io/loom/loom-dashboard.html`

### Pros:
- ✅ Free hosting
- ✅ Access from anywhere
- ✅ Easy to share with team
- ✅ Automatic updates (push code, changes live)
- ✅ HTTPS included

### Cons:
- ❌ Requires GitHub repo
- ❌ Public by default (can be private)
- ❌ Slight delay after pushing changes

### Example: LOOM Dashboard on Pages
```
Repository: WalkerJustin/loom
File: loom-dashboard.html
Public URL: https://walkerjustin.github.io/loom/loom-dashboard.html
```

---

## 🏢 Option 3: Corporate Web Server

**Best for:** Teams, enterprises, controlled access

### Prerequisites:
- Access to web server (Apache, Nginx, IIS)
- HTTPS/SSL certificate (recommended)
- Network access configured

### Steps:

#### For Apache/Nginx:
```bash
# Copy file to web directory
cp loom-dashboard.html /var/www/html/
# or
cp loom-dashboard.html /usr/share/nginx/html/

# Make readable by web server
chmod 644 /var/www/html/loom-dashboard.html
```

#### For IIS (Windows):
1. Open IIS Manager
2. Right-click Default Website → Add Application
3. Alias: `loom`
4. Physical path: `C:\inetpub\wwwroot\loom`
5. Copy `loom-dashboard.html` to that folder
6. Access at: `http://yourserver/loom/loom-dashboard.html`

#### For Node.js Simple Server:
```bash
npm install -g http-server
http-server .
# Access at: http://localhost:8080/loom-dashboard.html
```

#### For Python:
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Access at: http://localhost:8000/loom-dashboard.html
```

### Security Considerations:
1. ✅ Use HTTPS only
2. ✅ Add authentication (if needed)
3. ✅ Restrict IP ranges (firewall)
4. ✅ Use security headers
5. ✅ Regular backups

### Example Nginx Configuration:
```nginx
server {
    listen 443 ssl http2;
    server_name loom.yourcompany.com;
    
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    
    root /var/www/loom;
    
    location / {
        index loom-dashboard.html;
    }
}
```

---

## ☁️ Option 4: AWS S3 + CloudFront (Scalable)

**Best for:** High availability, global access, production

### Prerequisites:
- AWS account
- S3 bucket
- CloudFront distribution
- Route 53 domain (optional)

### Steps:

#### Step 1: Create S3 Bucket
```bash
aws s3 mb s3://loom-dashboard
```

#### Step 2: Upload File
```bash
aws s3 cp loom-dashboard.html s3://loom-dashboard/
aws s3 sync . s3://loom-dashboard/ --exclude "*" --include "*.html"
```

#### Step 3: Enable Public Access
```bash
# Allow GetObject
aws s3api put-bucket-policy --bucket loom-dashboard --policy '{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Principal": "*",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::loom-dashboard/*"
    }]
}'
```

#### Step 4: Create CloudFront Distribution
1. AWS Console → CloudFront
2. Create distribution
3. Origin: S3 bucket
4. Viewer protocol: HTTPS only
5. Deploy

#### Step 5: Access
- CloudFront URL: `https://d123456.cloudfront.net/loom-dashboard.html`
- Or use custom domain via Route 53

### Pros:
- ✅ Global CDN for fast loading
- ✅ Highly available
- ✅ Automatic scaling
- ✅ DDoS protection included

### Cons:
- ❌ AWS costs (~$1-5/month for low usage)
- ❌ More complex setup
- ❌ Requires AWS account

---

## 📱 Option 5: Vercel (Easiest for Developers)

**Best for:** Developers, fast deployment, free tier

### Steps:
1. Push code to GitHub
2. Go to vercel.com
3. Import repository
4. Deploy (automatic)
5. Access at: `your-project.vercel.app/loom-dashboard.html`

### Pros:
- ✅ Free tier available
- ✅ Automatic deployments
- ✅ Global CDN included
- ✅ Custom domain support

---

## 🔒 Security Best Practices (All Options)

### ✅ DO:
- Use HTTPS only (not HTTP)
- Store token in browser localStorage only
- Use minimal-scope GitHub tokens
- Regenerate tokens every 90 days
- Monitor token usage on GitHub
- Keep backups of configuration
- Use strong passwords for GitHub account

### ❌ DON'T:
- Expose your GitHub token in code
- Commit secrets to repositories
- Use admin-level tokens
- Share your browser session
- Leave dashboard open on shared computers
- Publish your dashboard on non-HTTPS servers
- Store token in config files

---

## 🚨 Token Security

### Creating Safe Tokens:

```
GitHub → Settings → Developer Settings → Personal Access Tokens

Name: LOOM Dashboard
Expiration: 90 days
Scopes: repo, workflow

DO NOT SELECT: admin, delete_repo, gpg_key
```

### Rotating Tokens:

**Every 90 days:**
1. Create new token on GitHub
2. Update dashboard Settings
3. Delete old token from GitHub
4. Monitor for any access issues

### If Compromised:

1. **Immediately revoke** the token on GitHub
2. **Delete** from browser localStorage:
   - DevTools → Application → LocalStorage
   - Delete `loomConfig` key
3. **Create new token** with fresh scopes
4. **Update dashboard** with new token

---

## 📊 Deployment Comparison

| Method | Cost | Setup | Access | Speed | Security |
|--------|------|-------|--------|-------|----------|
| Local | Free | 1 min | Local only | Instant | Excellent |
| GitHub Pages | Free | 5 min | Public/Private | Fast | Good |
| Web Server | Variable | 10-30 min | Controlled | Fast | Excellent |
| AWS S3 | $1-5/mo | 20 min | Global | Very Fast | Excellent |
| Vercel | Free | 3 min | Global | Very Fast | Good |

---

## 🧪 Testing Your Deployment

### After deploying, verify:

```javascript
// Open browser console (F12)

// Test 1: Can you see the dashboard?
console.log("Dashboard loaded:", document.title);
// Expected: "LOOM Dashboard"

// Test 2: Can you access settings?
console.log("LocalStorage:", localStorage.getItem('loomConfig'));

// Test 3: Can you make API calls?
// (Set token in Settings first, then test in console)
```

### Manual Verification:
1. Open dashboard URL
2. Configure GitHub token in Settings
3. Click 🔄 Sync
4. Verify dashboard loads data from GitHub
5. Try submitting an Intent Card
6. Check that issue appears on GitHub

---

## 🔧 Troubleshooting Deployment

### "File not found" error
- Check file path is correct
- Verify file extension is `.html`
- Check permissions (readable by web server)

### "Can't connect to GitHub"
- Verify token is correct
- Check GitHub API rate limits
- Verify internet connection
- Try from different network

### HTTPS certificate warnings
- Install valid SSL certificate
- Update server configuration
- Trust certificate in browser

### Token not persisting
- Check browser allows localStorage
- Verify cookies are not disabled
- Try incognito mode
- Check browser privacy settings

---

## 📞 Support

**Need help?**
1. Check LOOM-DASHBOARD-README.md for full docs
2. Check QUICK-REFERENCE.md for common tasks
3. Open browser DevTools (F12) for error messages
4. Test with curl/Postman if API is not working

---

## 🎉 Deployment Checklist

- [ ] Download `loom-dashboard.html`
- [ ] Choose deployment method
- [ ] Deploy to chosen platform
- [ ] Generate GitHub PAT token
- [ ] Test dashboard loads
- [ ] Configure token in Settings
- [ ] Test submission workflow
- [ ] Test approval workflow
- [ ] Share with team
- [ ] Set up bookmarks/shortcuts

---

**Ready to go live?** Choose your deployment method above and follow the steps!

---

**Last Updated:** November 2024
**Version:** 1.0
