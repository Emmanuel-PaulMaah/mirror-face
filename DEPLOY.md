# 🚀 Deploy to GitHub Pages - Step-by-Step Guide

This guide will teach you how to deploy your Face Tracking Mirror app to GitHub Pages so anyone can access it online!

## Prerequisites
- A GitHub account (free at [github.com](https://github.com))
- Git installed on your computer (check by running `git --version` in terminal)

---

## Step 1: Download Your Project Files

First, download these files from Replit to your computer:

1. Click the **three dots menu** (⋮) in Replit's file explorer
2. Select **"Download as zip"**
3. Extract the zip file to a folder on your computer

**Important files to keep:**
- `index.html` - Your main app
- `demo-avatar.glb` - Demo 3D model
- `.gitignore` - Tells git which files to ignore

**Optional files:**
- `server.py` - Only for local testing (GitHub Pages doesn't need this)
- `replit.md` - Project documentation (helpful for reference)
- `DEPLOY.md` - This deployment guide

> **Note:** GitHub Pages automatically serves `index.html` - you don't need `server.py` for deployment!

---

## Step 2: Create a GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **"+"** icon in the top-right corner
3. Select **"New repository"**
4. Fill in the details:
   - **Repository name:** `face-tracking-mirror` (or any name you like)
   - **Description:** "Real-time face tracking with 3D models using MediaPipe"
   - **Visibility:** Public (required for free GitHub Pages)
   - ✅ Check **"Add a README file"**
5. Click **"Create repository"**

---

## Step 3: Push Your Files to GitHub

### Option A: Using GitHub Desktop (Easiest)

1. Download [GitHub Desktop](https://desktop.github.com/)
2. Sign in with your GitHub account
3. Click **"Clone a repository"** → Select your new repo
4. Choose where to save it on your computer
5. Copy all your project files into this folder
6. GitHub Desktop will show your changes
7. Write a commit message: "Initial commit - face tracking app"
8. Click **"Commit to main"**
9. Click **"Push origin"**

### Option B: Using Command Line (Terminal)

Open your terminal in the project folder and run:

```bash
# Initialize git repository
git init

# Add all files to git
git add .

# Commit your files
git commit -m "Initial commit - face tracking app"

# Connect to your GitHub repository (replace USERNAME and REPO-NAME)
git remote add origin https://github.com/USERNAME/REPO-NAME.git

# Push to GitHub
git branch -M main
git push -u origin main
```

**Replace:**
- `USERNAME` with your GitHub username
- `REPO-NAME` with your repository name

---

## Step 4: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **"Settings"** (top navigation)
3. Click **"Pages"** in the left sidebar
4. Under **"Source"**, select:
   - **Branch:** `main`
   - **Folder:** `/ (root)`
5. Click **"Save"**

GitHub will show a message: *"Your site is ready to be published at https://USERNAME.github.io/REPO-NAME/"*

---

## Step 5: Wait and Test

1. Wait **1-2 minutes** for GitHub to build your site
2. Refresh the Settings → Pages page
3. You should see: *"Your site is live at https://USERNAME.github.io/REPO-NAME/"*
4. Click the link to open your app!

---

## 🎉 Your App is Live!

Your face tracking mirror is now publicly accessible! Share the link with anyone.

**Example URL:**
```
https://yourusername.github.io/face-tracking-mirror/
```

---

## Making Updates

Whenever you make changes to your app:

### Using GitHub Desktop:
1. Make your changes in the local folder
2. Open GitHub Desktop
3. Write a commit message describing your changes
4. Click **"Commit to main"**
5. Click **"Push origin"**
6. Wait 1-2 minutes for GitHub Pages to update

### Using Command Line:
```bash
# Add your changes
git add .

# Commit with a message
git commit -m "Updated tracking smoothness"

# Push to GitHub
git push
```

---

## Troubleshooting

### ❌ Camera doesn't work
- **HTTPS required:** GitHub Pages automatically serves over HTTPS ✅
- Clear your browser cache and try again
- Check browser permissions for camera access

### ❌ 404 Error / Page not found
- Wait 2-3 minutes after enabling Pages
- Make sure `index.html` is in the root folder (not in a subfolder)
- Check that the repository is **Public**

### ❌ 3D model doesn't load
- Make sure `demo-avatar.glb` is in the same folder as `index.html`
- Check the browser console (F12) for errors
- Verify the file was uploaded to GitHub

### ❌ Blank page
- Open browser console (F12) and check for errors
- Make sure all files were pushed to GitHub
- Try hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

---

## Advanced: Custom Domain

Want to use your own domain like `myapp.com`?

1. Buy a domain from [Namecheap](https://namecheap.com) or [Google Domains](https://domains.google)
2. In your GitHub repository settings → Pages:
   - Enter your custom domain
   - Click **"Save"**
3. In your domain registrar's DNS settings, add:
   - **Type:** CNAME
   - **Name:** www
   - **Value:** `yourusername.github.io`
4. Wait 24-48 hours for DNS to propagate

---

## Tips for Success

✅ **Always test locally first** using `python server.py` on port 5000
✅ **Use meaningful commit messages** to track your changes
✅ **Test on mobile** by visiting the URL on your phone
✅ **Share your project** - add the live link to your repository README

---

## Need Help?

- **GitHub Pages Docs:** https://docs.github.com/pages
- **Git Guide:** https://guides.github.com/introduction/git-handbook/
- **MediaPipe Docs:** https://developers.google.com/mediapipe

Happy deploying! 🎭✨
