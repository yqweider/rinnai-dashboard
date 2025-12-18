# 🔄 HOW TO UPDATE YOUR GITHUB REPOSITORY

## 📋 Quick Overview

You're updating from **v1.0.0** (monitoring only) to **v1.1.0** (with interactive controls).

---

## 🚀 METHOD 1: Web Upload (Easiest - 3 Minutes)

### Step 1: Download the Updated File
1. Download the new **`rinnai-dashboard.html`** file (the one with interactive controls)
2. Save it to your computer

### Step 2: Go to Your Repository
1. Open your browser
2. Go to: `https://github.com/YOUR_USERNAME/rinnai-dashboard`
3. Sign in if needed

### Step 3: Replace the File
1. Click on **`rinnai-dashboard.html`** in the file list
2. Click the **pencil icon** (✏️) to edit
3. Click **"Delete this file"** (trash icon)
4. Confirm deletion
5. Go back to main repository page
6. Click **"Add file"** → **"Upload files"**
7. Drag the new `rinnai-dashboard.html` file
8. **Commit message:** "Update to v1.1.0 - Add interactive controls"
9. Click **"Commit changes"**

### Step 4: Update README (Optional but Recommended)
1. Click on **`README.md`**
2. Click the **pencil icon** to edit
3. Find the **Features** section and add:
   ```markdown
   - 🎮 **Interactive Controls** - Set temperature and control recirculation
   ```
4. Update version badge if you have one
5. Commit changes

### Step 5: Create New Release
1. Click **"Releases"** (right sidebar)
2. Click **"Draft a new release"**
3. Fill in:
   - **Tag:** `v1.1.0`
   - **Release title:** `v1.1.0 - Interactive Controls`
   - **Description:**
     ```
     ## New Features
     - 🎮 Interactive temperature control (100-140°F)
     - 💧 Start/Stop recirculation with custom duration
     - ✅ Real-time status feedback
     - 🎨 Enhanced UI with control buttons
     
     ## Changes
     - Added temperature adjustment controls
     - Added recirculation duration control
     - Added service call integration
     - Added status message system
     
     ## Compatibility
     - Fully backward compatible with v1.0.0
     - Requires Home Assistant 2024.1.0+
     - Requires rinnaicontrolr-ha v2.2.0+
     ```
4. Click **"Publish release"**

### Step 6: Users Update via HACS
Once published, users can:
1. Go to HACS in Home Assistant
2. Find "Rinnai Dashboard"
3. Click **"Update"**
4. Restart Home Assistant
5. Hard refresh browser (Ctrl+Shift+R)

---

## 🚀 METHOD 2: Git Command Line (Advanced - 2 Minutes)

### If You Have Git Installed:

```bash
# Navigate to your local repository
cd /path/to/rinnai-dashboard

# Make sure you're on main branch
git checkout main

# Pull latest (just in case)
git pull origin main

# Copy the new dashboard file
cp /path/to/new/rinnai-dashboard.html ./

# Stage the changes
git add rinnai-dashboard.html

# Commit with message
git commit -m "Update to v1.1.0 - Add interactive controls

- Add temperature control (+/- buttons)
- Add recirculation start/stop with duration
- Add status message system
- Enhance UI with control section"

# Push to GitHub
git push origin main

# Create and push tag
git tag -a v1.1.0 -m "v1.1.0 - Interactive Controls"
git push origin v1.1.0
```

### Then Create Release on GitHub:
1. Go to repository on GitHub
2. Click "Releases" → "Draft a new release"
3. Select tag `v1.1.0`
4. Add release notes (see Method 1, Step 5)
5. Publish

---

## 🚀 METHOD 3: GitHub Desktop (Easy with GUI)

### If You Use GitHub Desktop:

1. Open **GitHub Desktop**
2. Select your `rinnai-dashboard` repository
3. **Replace** the `rinnai-dashboard.html` file in the folder
4. GitHub Desktop shows the changes
5. Add commit message: "Update to v1.1.0 - Add interactive controls"
6. Click **"Commit to main"**
7. Click **"Push origin"**
8. Go to GitHub.com to create the release (see Method 1, Step 5)

---

## ✅ VERIFICATION CHECKLIST

After updating, verify:

- [ ] New file uploaded successfully
- [ ] Commit message is clear
- [ ] Release v1.1.0 is published with tag
- [ ] Release notes explain new features
- [ ] README updated (optional)
- [ ] Can see update in HACS

---

## 📱 HOW USERS WILL UPDATE

### Via HACS:
1. HACS → Frontend
2. Find "Rinnai Dashboard"
3. Click **"Update"** (if available)
4. Restart Home Assistant
5. Hard refresh browser

### Manual Users:
1. Download new file from your repo
2. Replace in `/config/www/`
3. Hard refresh browser

---

## 🎯 VERSION NUMBERING

For future updates:

- **v1.1.0** → **v1.1.1** (Bug fixes, small changes)
- **v1.1.0** → **v1.2.0** (New features, enhancements)
- **v1.1.0** → **v2.0.0** (Major changes, breaking changes)

---

## 💡 PRO TIPS

### Best Practices:
1. **Always create a release** - HACS requires tags
2. **Write clear release notes** - Users want to know what changed
3. **Use semantic versioning** - Makes tracking easier
4. **Test locally first** - Make sure it works before pushing

### What to Include in Release Notes:
- ✅ **New Features** - What's new
- ✅ **Changes** - What's different
- ✅ **Bug Fixes** - What's fixed
- ✅ **Breaking Changes** - What might break (if any)
- ✅ **Requirements** - Minimum versions

### Optional Extras:
- Add screenshots showing new controls
- Create a CHANGELOG.md file
- Add version badge to README
- Tag issues/PRs in release notes

---

## 🐛 TROUBLESHOOTING

### "Nothing changed" after update:
- Hard refresh browser (Ctrl+Shift+R)
- Clear browser cache
- Restart Home Assistant
- Check file actually updated in repo

### HACS not showing update:
- Wait a few minutes (GitHub/HACS sync delay)
- Verify release tag starts with 'v'
- Check release is published (not draft)
- Manually refresh HACS

### Users can't see new features:
- Tell them to hard refresh (Ctrl+Shift+R)
- File might be cached
- May need to clear HA frontend cache

---

## 📝 EXAMPLE COMMIT MESSAGES

**Good:**
```
Update to v1.1.0 - Add interactive controls

- Add temperature adjustment (+/- buttons)
- Add recirculation control with duration
- Add status feedback system
- Improve UI with new controls section
```

**Bad:**
```
update file
```

---

## 🎉 YOU'RE DONE!

After updating:
1. ✅ New version on GitHub
2. ✅ Release published
3. ✅ Users can update via HACS
4. ✅ Everyone gets interactive controls!

**Remember:** Every time you update, create a new release with a new version tag!

---

## 📚 ADDITIONAL RESOURCES

- [GitHub Releases Guide](https://docs.github.com/en/repositories/releasing-projects-on-github)
- [Semantic Versioning](https://semver.org/)
- [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
- [HACS Documentation](https://hacs.xyz/)

Happy updating! 🚀
