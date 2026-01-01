# Home Assistant Blueprints

A collection of useful Home Assistant blueprints to automate and enhance your smart home experience. These blueprints provide ready-to-use automation templates that can be easily imported and customized in your Home Assistant installation.

## Available Blueprints

| Blueprint | Description | Install |
|-----------|-------------|---------|
| [RGB Color Cycling](rgb-color-cycling-blueprint.yaml) | Smooth RGB color cycling script that transitions through the color spectrum. Creates beautiful smooth color transitions through Cyan→Blue→Magenta→Red→Yellow→Green→Cyan cycle. | [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fbthos%2Fhome-assistant-blueprints%2Frefs%2Fheads%2Fmain%2Frgb-color-cycling-blueprint.yaml) |
| [Dishwasher PVPC Smart Scheduling](dishwasher-pvpc-smart-scheduling-blueprint.yaml) | Smart dishwasher scheduling based on PVPC electricity pricing. Automatically checks PVPC prices when dishwasher is turned on and reschedules to cheaper hours if current price is too high. Supports Home Connect for native delayed start. | [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fbthos%2Fhome-assistant-blueprints%2Frefs%2Fheads%2Fmain%2Fdishwasher-pvpc-smart-scheduling-blueprint.yaml) |
| [Occupancy Multi-Condition Light Control](occupancy-multi-condition-light-control-blueprint.yaml) | Generalized occupancy-based lighting with multiple sensors, time restrictions, and additional conditions. Supports AND/OR logic, illuminance thresholds, day/night restrictions, and automatic turn-off delays. | [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fbthos%2Fhome-assistant-blueprints%2Frefs%2Fheads%2Fmain%2Foccupancy-multi-condition-light-control-blueprint.yaml) |
| [State Machine Light Control](state-machine-light-control-blueprint.yaml) | Advanced lighting control using state machine with multiple device groups. Supports immediate and delayed behaviors, state persistence, and debouncing to prevent rapid cycling. | [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fbthos%2Fhome-assistant-blueprints%2Frefs%2Fheads%2Fmain%2Fstate-machine-light-control-blueprint.yaml) |

## Usage Instructions

### Installing Blueprints

1. **Using the Install Button**: Click the "Open your Home Assistant instance..." button in the table above for any blueprint you want to install. This will open your Home Assistant instance and pre-fill the blueprint import dialog.

2. **Manual Installation**: 
   - Copy the raw URL of the blueprint file (e.g., `https://raw.githubusercontent.com/bthos/home-assistant-blueprints/refs/heads/main/rgb-color-cycling-blueprint.yaml`)
   - In Home Assistant, go to **Settings** → **Automations & Scenes** → **Blueprints**
   - Click **Import Blueprint** and paste the URL

### Using Blueprints

1. After importing a blueprint, go to **Settings** → **Automations & Scenes** → **Automations**
2. Click **Create Automation** → **Use Blueprint**
3. Select the imported blueprint and configure the required parameters
4. Save your automation with a descriptive name

### Blueprint-Specific Requirements

#### Dishwasher PVPC Smart Scheduling Blueprint

Before using this blueprint, you need:

**PVPC Hourly Pricing Integration:**
- Install the PVPC integration from Home Assistant integrations
- Ensure you have a `sensor.pvpc` entity providing electricity prices

**Dishwasher Device:**
- A controllable dishwasher device (switch, smart plug, or Home Connect appliance)

**Optional Home Connect Setup:**
- Home Connect integration configured for native delayed start functionality
- Dishwasher program name (e.g., 'Dishcare.Dishwasher.Program.Auto2')

**Usage Tips:**
- Set your maximum acceptable electricity price threshold
- The blueprint will automatically find the cheapest hour within your specified time window
- With Home Connect, it uses native delayed start; without it, turns device off/on at scheduled time
- Notifications help track scheduling decisions and price information

#### RGB Color Cycling Blueprint

Before using the RGB Color Cycling blueprint, you need to create the following input number helpers in Home Assistant:

**Go to Settings → Devices & Services → Helpers → Create Helper → Number:**

- `input_number.color_r` (min: 0, max: 255, step: 1)
- `input_number.color_g` (min: 0, max: 255, step: 1) 
- `input_number.color_b` (min: 0, max: 255, step: 1)
- `input_number.color_phase` (min: 1, max: 6, step: 1)
- `input_number.color_step` (min: 1, max: 50, step: 1)

**Usage Tips:**
- The blueprint works with any RGB-capable lights
- Adjust the step size to control transition speed (lower = smoother, higher = faster)
- Only lights that are currently "on" will have their colors changed
- The color cycle will smoothly transition through the full spectrum

#### Occupancy Multi-Condition Light Control Blueprint

Generalized occupancy-based lighting control converted from Node-RED workflows.

**Required:**
- One or more occupancy sensors (binary_sensor entities)
- Target light or switch entities to control

**Optional:**
- Illuminance sensor for ambient light checking
- Time restrictions (day only, night only, custom windows)
- Adaptive brightness settings

**Usage Tips:**
- Perfect for hallways with multiple occupancy sensors (use AND logic)
- Living rooms requiring both occupancy and low illuminance
- Rooms that should only activate during specific times (night only, day only)
- Supports multiple target devices with transition time control
- Automatic turn-off delay prevents lights from flickering
- Use AND logic when all sensors must detect occupancy
- Use OR logic when any sensor detecting occupancy should trigger

**Adaptive Brightness Feature:**
- Protects eyes from bright light at night (occasional activations)
- Uses dimmed brightness during nighttime (default 30%)
- Uses full brightness during daytime (default 100%)
- Night period detection: sun-based (automatic) or custom time window
- Enable with `Adaptive Brightness` toggle

**Common Configurations:**
- **Hallway (2 sensors)**: Use AND logic, night_only restriction, 0 minute turn-off delay
- **Living Room**: Use single sensor, add illuminance sensor (< 500 lux), 15 minute turn-off delay
- **Dressing Room**: Use single sensor, night_only restriction, 0 minute turn-off delay
- **Night-friendly**: Enable adaptive brightness, 30% night brightness, sunset-based detection

#### State Machine Light Control Blueprint

Advanced lighting control with state machine logic converted from Node-RED workflows.

**Required:**
- Occupancy sensor (binary_sensor)
- At least one device group configured

**Optional:**
- Input text helper for state persistence (recommended for reliability)
- Second device group for complex scenarios

**Usage Tips:**
- Perfect for bathrooms with mirror and main lights (different behaviors)
- Mirror light: Use immediate behavior for instant response
- Main light: Use delayed behavior (30 seconds) to prevent rapid cycling
- State machine handles transitions: OFF → OFF_TO_ON → ON → ON_TO_OFF → OFF
- State persistence via helper entity ensures state survives restarts
- Delayed devices automatically reset if occupancy detected during delay
- Minimum state duration prevents rapid cycling (debouncing)

**Common Configurations:**
- **Bathroom**: 
  - Group 1 (Mirror): Immediate behavior
  - Group 2 (Main): Delayed behavior, 30 second delay
  - Use state helper for persistence

## Contributing

We welcome contributions of new blueprints! Here's how you can contribute:

### Blueprint Standards

1. **File Naming**: Use descriptive, lowercase names with hyphens (e.g., `rgb-color-cycling-blueprint.yaml`)

2. **Required Metadata**: Every blueprint must include:
   ```yaml
   blueprint:
     name: "Descriptive Blueprint Name"
     description: >
       Clear description of what the blueprint does.
       Include any special requirements or setup instructions.
     domain: script  # or automation
     author: your-github-username
   ```

3. **Documentation**: Include clear descriptions for all input parameters

4. **Testing**: Test your blueprint thoroughly before submitting

### Submission Process

1. **Fork** this repository
2. **Create** your blueprint file following the naming convention
3. **Test** the blueprint in your Home Assistant instance
4. **Update** the README.md table with your new blueprint
5. **Submit** a pull request with:
   - Blueprint file
   - Updated README.md
   - Description of what the blueprint does
   - Any special requirements or setup instructions

### Blueprint Categories

We organize blueprints into the following categories:
- **Lighting**: Light control, color cycling, mood lighting
- **Security**: Motion detection, alerts, surveillance
- **Climate**: HVAC control, temperature management
- **Entertainment**: Media control, party modes
- **Utilities**: General home automation, scheduling

## License

This project is open source. Individual blueprints may have their own licensing terms as specified by their authors.

## Support

If you encounter issues with any blueprint:
1. Check the blueprint's specific requirements and setup instructions
2. Verify that all required helper entities are created correctly
3. Review the Home Assistant logs for any error messages
4. Open an issue in this repository with detailed information about the problem

---

*Made with ❤️ for the Home Assistant community*