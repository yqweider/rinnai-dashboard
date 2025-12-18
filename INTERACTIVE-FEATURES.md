# 🎮 INTERACTIVE DASHBOARD FEATURES

## ✨ New in v1.1.0: Full Control Integration!

The dashboard now includes **interactive controls** to manage your Rinnai water heater directly!

---

## 🎯 What You Can Control

### 1. 🌡️ **Temperature Control**
- **Adjust target temperature** from 100°F to 140°F
- Use **+/- buttons** to increment by 1°F
- Click **"Apply Temperature"** to send to water heater
- See confirmation message when set

**How it works:**
- Calls `water_heater.set_temperature` service
- Updates your `water_heater.rinnai_water_heater` entity
- Real-time feedback in dashboard

### 2. 💧 **Recirculation Control**
- **Start/Stop hot water circulation** on demand
- Set **custom duration** (5-60 minutes)
- One-click control with status feedback
- Button changes based on current state

**How it works:**
- **Start:** Calls `rinnai.start_recirculation` service with duration
- **Stop:** Calls `switch.turn_off` on recirculation switch
- Monitors pump status for feedback

---

## 🚀 Using the Controls

### Temperature Adjustment:
1. Click **minus (-)** to decrease or **plus (+)** to increase
2. Watch the target temperature update
3. Click **"Apply Temperature"** button
4. See success message confirming change

### Recirculation:
1. Enter desired **duration** (default 15 minutes)
2. Click **"Start Recirculation"** button
3. Button changes to **"Stop Recirculation"** when running
4. Click again to stop early if needed

---

## 🔧 Technical Details

### Services Called:

#### Set Temperature:
```yaml
service: water_heater.set_temperature
target:
  entity_id: water_heater.rinnai_water_heater
data:
  temperature: 125  # Your selected temp
```

#### Start Recirculation:
```yaml
service: rinnai.start_recirculation
target:
  entity_id: water_heater.rinnai_water_heater
data:
  recirculation_minutes: 15  # Your selected duration
```

#### Stop Recirculation:
```yaml
service: switch.turn_off
target:
  entity_id: switch.rinnai_recirculation
```

---

## 🎨 UI Features

### Status Messages:
- ✅ **Green** - Success (action completed)
- 🔴 **Red** - Error (something went wrong)
- ℹ️ **Blue** - Info (demo mode or notification)

### Button States:
- **Enabled** - Ready to use
- **Disabled** - Action in progress
- **Color change** - Active/inactive state

### Visual Feedback:
- Buttons scale on hover
- Success/error messages appear for 5 seconds
- Instant UI updates reflect changes

---

## 🛡️ Safety Features

### Temperature Limits:
- **Minimum:** 100°F (prevents too cold)
- **Maximum:** 140°F (prevents scalding)
- **Step:** 1°F increments

### Recirculation Limits:
- **Minimum:** 5 minutes
- **Maximum:** 60 minutes
- Prevents accidental very long runs

### Error Handling:
- Catches and displays service call errors
- Buttons re-enable after errors
- Clear error messages for troubleshooting

---

## 📱 Demo Mode

When not connected to Home Assistant (testing locally):
- **Temperature control** - Shows what would be set
- **Recirculation** - Simulates pump turning on/off
- **Visual updates** - See animations in action
- **No actual changes** - Safe to test

---

## ⚙️ Configuration

### Default Values:
```javascript
// In the dashboard HTML:
currentTargetTemp = 120;  // Default starting temp
recircDuration = 15;      // Default circulation time
```

### Customization:
Edit the HTML to change:
- Default temperature (line ~360)
- Default duration (line ~395)
- Min/max limits (adjust temperature function)
- Button colors (CSS styles)

---

## 🔍 Troubleshooting

### Controls don't work:
- ✅ Verify you're accessing via Home Assistant (not direct file)
- ✅ Check browser console (F12) for errors
- ✅ Ensure entities exist and are available
- ✅ Verify services are available in Developer Tools

### Temperature not changing:
- Check water heater entity is correct
- Verify `water_heater.set_temperature` service exists
- Check Home Assistant logs for errors
- Ensure water heater is online

### Recirculation not starting:
- Verify `rinnai.start_recirculation` service exists
- Check integration is v2.2.0+
- Ensure `switch.rinnai_recirculation` exists
- Try calling service manually in Developer Tools

### Status messages not showing:
- Check JavaScript console for errors
- Verify statusMessage div exists in HTML
- Ensure showStatus function is defined

---

## 💡 Pro Tips

### Quick Access:
1. Set common temperature as default
2. Use duration presets for routine tasks
3. Add to home screen on mobile for instant access

### Automation Integration:
Controls work alongside your automations:
- Manual override doesn't break automations
- Automations can still trigger circulation
- Both can coexist peacefully

### Best Practices:
- **Morning routine:** Start 15-min circulation before shower
- **Quick use:** Use 5-10 min for hand washing
- **Extended use:** Set 30+ min for multiple showers
- **Emergency stop:** Click stop button if needed

---

## 🎯 Future Enhancements (Ideas)

Potential additions:
- [ ] Schedule presets (morning, evening, etc.)
- [ ] One-touch temperature favorites (comfortable, hot, max)
- [ ] Circulation timer countdown
- [ ] Energy usage estimation
- [ ] Historical usage charts
- [ ] Voice control integration

---

## 📚 Related Documentation

- [Home Assistant Water Heater Integration](https://www.home-assistant.io/integrations/water_heater/)
- [Rinnai Services Documentation](https://github.com/explosivo22/rinnaicontrolr-ha)
- [Home Assistant Service Calls](https://www.home-assistant.io/docs/scripts/service-calls/)

---

**Enjoy full control of your Rinnai water heater!** 🔥💧
