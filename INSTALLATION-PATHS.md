# 📍 INSTALLATION PATH QUICK REFERENCE

## 🎯 Where Files Go (Automatically)

### HACS Installation (Recommended)
When users install via HACS, files automatically go to:

```
/config/www/community/rinnai-dashboard/rinnai-dashboard.html
```

**Dashboard card configuration:**
```yaml
type: iframe
url: /local/community/rinnai-dashboard/rinnai-dashboard.html
aspect_ratio: 60%
```

---

### Manual Installation (Alternative)
If users manually copy files, they go to:

```
/config/www/rinnai-dashboard.html
```

**Dashboard card configuration:**
```yaml
type: iframe
url: /local/rinnai-dashboard.html
aspect_ratio: 60%
```

---

## 🔍 How to Verify Installation

### Check if HACS installed correctly:
```bash
ls -la /config/www/community/rinnai-dashboard/
# Should show: rinnai-dashboard.html
```

### Check if manual install worked:
```bash
ls -la /config/www/
# Should show: rinnai-dashboard.html
```

### Test in browser:
**HACS:** `http://YOUR_HA_IP:8123/local/community/rinnai-dashboard/rinnai-dashboard.html`  
**Manual:** `http://YOUR_HA_IP:8123/local/rinnai-dashboard.html`

---

## 💡 Pro Tip

After installing via HACS, Home Assistant automatically:
- ✅ Downloads the file
- ✅ Places it in the correct directory
- ✅ Makes it accessible at `/local/community/...`
- ✅ Updates it when you release new versions

Users don't need to manually copy anything! That's the power of HACS! 🚀
