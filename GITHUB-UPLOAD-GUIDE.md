# 🚀 HOW TO UPLOAD THIS TO GITHUB (5 Minutes!)

Follow these simple steps to create your GitHub repository and add it to HACS.

## 📋 What You'll Need

- A GitHub account (free - sign up at github.com)
- The files I've prepared (they're in the github-repo folder)

---

## 🔷 STEP 1: Create GitHub Repository (2 minutes)

### 1.1 Go to GitHub
- Visit https://github.com
- Sign in (or create account if needed)

### 1.2 Create New Repository
1. Click the **"+"** button in top right
2. Click **"New repository"**
3. Fill in:
   - **Repository name:** `rinnai-dashboard` (or any name you like)
   - **Description:** "Custom animated dashboard for Rinnai RU199iN water heater"
   - **Public** (must be public for HACS)
   - ✅ Check "Add a README file"
   - **License:** MIT License
4. Click **"Create repository"**

---

## 🔷 STEP 2: Upload Files (2 minutes)

### Method A: Web Upload (Easiest)

1. In your new repository, click **"Add file"** → **"Upload files"**

2. **Download these files** from what I created:
   - `rinnai-dashboard.html`
   - `hacs.json`
   - `README.md`
   - `info.md`
   - `LICENSE`
   - `.gitignore`
   - `example-configuration.yaml`

3. **Drag and drop** all files into the upload area

4. **Commit message:** "Initial commit - Rinnai Dashboard v1.0.0"

5. Click **"Commit changes"**

### Method B: Git Command Line (Advanced)

```bash
# Download all files to a folder on your computer first, then:

cd /path/to/your/folder
git init
git add .
git commit -m "Initial commit - Rinnai Dashboard v1.0.0"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/rinnai-dashboard.git
git push -u origin main
```

---

## 🔷 STEP 3: Create a Release (1 minute)

This is required for HACS to work!

1. In your repository, click **"Releases"** (right sidebar)
2. Click **"Create a new release"**
3. Fill in:
   - **Tag:** `v1.0.0`
   - **Release title:** `v1.0.0 - Initial Release`
   - **Description:**
     ```
     Initial release of Rinnai RU199iN Custom Dashboard
     
     Features:
     - Animated dashboard with cyberpunk design
     - Real-time temperature monitoring
     - Pump and heating status
     - Performance metrics
     - Fully responsive
     ```
4. Click **"Publish release"**

---

## 🔷 STEP 4: Add to HACS (1 minute)

### 4.1 Add Custom Repository

1. Open **Home Assistant**
2. Go to **HACS** (in sidebar)
3. Click the **three dots** (⋯) in top right
4. Select **"Custom repositories"**
5. Add:
   - **Repository:** `https://github.com/YOUR_USERNAME/rinnai-dashboard`
   - **Category:** Lovelace
6. Click **"Add"**

### 4.2 Install the Dashboard

1. In HACS, search for "Rinnai"
2. Click on **"Rinnai RU199iN Custom Dashboard"**
3. Click **"Download"**
4. **Restart Home Assistant**

### 4.3 Add to Dashboard

1. Go to your dashboard
2. Click **three dots** → **Edit Dashboard**
3. Click **"+ Add Card"**
4. Add this:
   ```yaml
   type: iframe
   url: /local/rinnai-dashboard.html
   aspect_ratio: 60%
   ```
5. Click **Save**

---

## ✅ VERIFICATION

Your repository should look like this:

```
rinnai-dashboard/
├── .gitignore
├── LICENSE
├── README.md
├── hacs.json
├── info.md
├── rinnai-dashboard.html
└── example-configuration.yaml
```

---

## 🎯 ALTERNATIVE: Quick Upload via GitHub Desktop

If you prefer a GUI:

1. Download **GitHub Desktop** (desktop.github.com)
2. Click **"Add"** → **"Create New Repository"**
3. Name it `rinnai-dashboard`
4. Copy all files into the repository folder
5. Click **"Commit to main"**
6. Click **"Publish repository"**
7. Make sure **"Keep this code public"** is checked
8. Click **"Publish Repository"**

Then follow Step 3 (Create Release) and Step 4 (Add to HACS).

---

## 💡 TIPS

- **Repository must be PUBLIC** for HACS to work
- **Always create a release** with a version tag (v1.0.0)
- Use **semantic versioning** for future updates (v1.0.1, v1.1.0, etc.)
- Add screenshots to your README later to make it look professional

---

## 🐛 TROUBLESHOOTING

### "Repository not found" in HACS
- Make sure repository is **public**
- Check URL is exactly: `https://github.com/YOUR_USERNAME/rinnai-dashboard`
- Wait a few minutes for GitHub to index it

### "No releases found"
- Create a release with version tag (v1.0.0)
- Make sure tag starts with "v"

### Dashboard not downloading in HACS
- Verify `hacs.json` file is present
- Check category is set to "Lovelace"
- Restart Home Assistant

---

## 🎉 YOU'RE DONE!

Once uploaded, you can:
- ✅ Install via HACS on any Home Assistant instance
- ✅ Share the repository with others
- ✅ Update easily by creating new releases
- ✅ Accept contributions from the community

Your repository URL will be:
**`https://github.com/YOUR_USERNAME/rinnai-dashboard`**

---

## 📱 BONUS: Share Your Work

Consider:
- Post on Home Assistant Community forums
- Share on Reddit r/homeassistant
- Add screenshots to your README
- Star the rinnaicontrolr-ha integration repository

Enjoy your new dashboard! 🔥💧
