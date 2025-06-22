# Home Assistant Blueprints

A collection of useful Home Assistant blueprints to automate and enhance your smart home experience. These blueprints provide ready-to-use automation templates that can be easily imported and customized in your Home Assistant installation.

## Available Blueprints

| Blueprint | Description | Install |
|-----------|-------------|---------|
| [RGB Color Cycling](rgb-color-cycling-blueprint.yaml) | Smooth RGB color cycling script that transitions through the color spectrum. Creates beautiful smooth color transitions through Cyan→Blue→Magenta→Red→Yellow→Green→Cyan cycle. | [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fbthos%2Fhome-assistant-blueprints%2Frefs%2Fheads%2Fmain%2Frgb-color-cycling-blueprint.yaml) |

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