# 🔥 Rinnai RU199iN Custom Dashboard for Home Assistant

A beautiful, animated dashboard for monitoring and controlling your Rinnai RU199iN tankless water heater through Home Assistant.

![Dashboard Preview](https://img.shields.io/badge/Home%20Assistant-Compatible-41BDF5?logo=homeassistant&logoColor=white)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## ✨ Features

- 🎨 **Beautiful Cyberpunk Design** - Dark gradient background with neon teal & orange accents
- 🌡️ **Real-time Temperature Monitoring** - Color-coded outlet/inlet temperatures
- 💧 **Animated Water Tank Visualization** - Shows water level and heating status
- 🔄 **Circulation Status** - Live pump and recirculation monitoring
- 🔥 **Heating Indicators** - Glowing animations when burner is active
- 📊 **Performance Metrics** - Pump cycles, hours, combustion data, fan diagnostics
- 🎮 **Interactive Controls** - Set temperature and control recirculation directly from dashboard
- 📱 **Fully Responsive** - Works perfectly on desktop, tablet, and mobile
- ⚡ **Zero Dependencies** - Pure HTML/CSS/JS, no external libraries required

## 📸 Screenshots

### Desktop View
The dashboard shows real-time water heater status with animated visualizations:
- Large temperature display with color-coded indicators
- Animated water tank with heating element
- Flow rate meter with progress bar
- Pump and heating status cards
- Fan diagnostics

### Mobile View
Fully responsive single-column layout optimized for phones and tablets.

## 🎯 Requirements

- **Home Assistant** 2024.1.0 or newer
- **Rinnai Control-R Integration** ([rinnaicontrolr-ha](https://github.com/explosivo22/rinnaicontrolr-ha)) version 2.2.0+
- Rinnai RU199iN (or compatible model) with Control-R 2.0 module

## 🚀 Installation

### Method 1: HACS (Recommended)

1. Open **HACS** in Home Assistant
2. Click the **three dots** in the top right
3. Select **Custom repositories**
4. Add this repository URL: `https://github.com/YOUR_USERNAME/rinnai-dashboard`
5. Category: **Lovelace**
6. Click **Add**
7. Click **Download** on the Rinnai Dashboard card
8. Restart Home Assistant

### Method 2: Manual Installation

1. Download `rinnai-dashboard.html` from this repository
2. Copy it to `/config/www/` in your Home Assistant installation
3. If the `www` folder doesn't exist, create it

## 📝 Configuration

### Step 1: Verify Entity Names

The dashboard is pre-configured with standard entity names. Verify yours match:

1. Go to **Developer Tools → States** in Home Assistant
2. Filter by "rinnai"
3. Compare with the entity names in the dashboard

Your entities should be:
```
water_heater.rinnai_water_heater
binary_sensor.rinnai_recirculation
binary_sensor.rinnai_heating
sensor.rinnai_outlet_temperature
sensor.rinnai_inlet_temperature
sensor.rinnai_water_flow_rate
sensor.rinnai_pump_cycles
sensor.rinnai_pump_hours
sensor.rinnai_combustion_cycles
sensor.rinnai_operation_hours
sensor.rinnai_fan_current
sensor.rinnai_fan_frequency
```

If your entity names differ, edit `rinnai-dashboard.html` around line 310 to update the `ENTITY_MAP`.

### Step 2: Add to Dashboard

**If installed via HACS:**
```yaml
type: iframe
url: /local/community/rinnai-dashboard/rinnai-dashboard.html
aspect_ratio: 60%
```

**If installed manually:**
```yaml
type: iframe
url: /local/rinnai-dashboard.html
aspect_ratio: 60%
```

Or for a full-screen panel view:
1. Create a new dashboard view
2. Enable "Panel Mode"
3. Add the iframe card

### Step 3: Optional - Add Template Sensors

For enhanced pump verification, add this to `configuration.yaml`:

```yaml
template:
  - binary_sensor:
      - name: "Rinnai Pump Actually Running"
        unique_id: rinnai_pump_actually_running
        state: >
          {{ states('binary_sensor.rinnai_recirculation') == 'on' 
             and states('sensor.rinnai_water_flow_rate')|float(0) > 0.1 }}
        device_class: running
        icon: mdi:pump
```

Then restart Home Assistant.

## 🎨 Customization

### Change Aspect Ratio

```yaml
aspect_ratio: 50%  # Taller display
aspect_ratio: 70%  # Shorter display
aspect_ratio: 100% # Square (good for mobile)
```

### Modify Colors

Edit the CSS gradients in `rinnai-dashboard.html`:

```css
background: linear-gradient(135deg, #YOUR_COLOR1 0%, #YOUR_COLOR2 50%, #YOUR_COLOR3 100%);
```

### Update Entity Names

If your entity names differ, update the `ENTITY_MAP` around line 310:

```javascript
const ENTITY_MAP = {
  targetTemp: 'your_water_heater_entity_here',
  outletTemp: 'your_outlet_temp_sensor_here',
  // ... etc
};
```

## 🔧 Troubleshooting

### Dashboard shows "Unknown" or demo data
- Verify entity names match your system
- Check that sensors have data in Developer Tools → States
- Enable "Maintenance Data" in Rinnai integration settings
- Wait 30 seconds for initial data load

### Dashboard not loading
- **HACS install:** Verify file is at `/config/www/community/rinnai-dashboard/rinnai-dashboard.html`
- **Manual install:** Verify file is at `/config/www/rinnai-dashboard.html`
- Clear browser cache (Ctrl+Shift+R)
- Try accessing directly: 
  - HACS: `http://YOUR_HA_IP:8123/local/community/rinnai-dashboard/rinnai-dashboard.html`
  - Manual: `http://YOUR_HA_IP:8123/local/rinnai-dashboard.html`

### Sensors not updating
- Enable "Maintenance Data" in Rinnai integration configuration
- Restart Home Assistant
- Check integration logs for errors

### Mobile display issues
- Use a modern browser (Chrome, Safari, Firefox)
- Try full-screen mode
- Adjust aspect ratio in card configuration

## 📱 Mobile Optimization

### Add to Home Screen

**iPhone:**
1. Open in Safari
2. Tap Share → Add to Home Screen

**Android:**
1. Open in Chrome
2. Menu → Add to Home Screen

Now access like a native app!

## 📚 Additional Resources

- [Rinnai Integration Documentation](https://github.com/explosivo22/rinnaicontrolr-ha)
- [Home Assistant Dashboard Documentation](https://www.home-assistant.io/dashboards/)
- [Template Sensor Documentation](https://www.home-assistant.io/integrations/template/)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

MIT License - feel free to use and modify!

## 💡 Tips

- Works great as a dedicated dashboard tab
- Consider adding automations based on dashboard data
- Enable maintenance mode for detailed sensor updates
- Compatible with Home Assistant Companion app

## 🆘 Support

If you encounter issues:
1. Check entity names match your system
2. Verify Rinnai integration is v2.2.0+
3. Check browser console (F12) for errors
4. Open an issue with error details

## ⭐ Acknowledgments

Built for the Home Assistant community. Special thanks to:
- [explosivo22](https://github.com/explosivo22) for the rinnaicontrolr-ha integration
- Home Assistant community for inspiration and support

---

**Enjoy your new Rinnai dashboard!** 🔥💧
