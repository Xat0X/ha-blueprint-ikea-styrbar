# 🎛️ IKEA Styrbar Multi-Device Controller

> **The ultimate way to control multiple lights and switches with a single IKEA Styrbar remote in Home Assistant.**

Turn your IKEA Styrbar into a multi-zone controller. Instead of controlling just one light, seamlessly cycle through different devices in your room using the arrow buttons.

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Blueprint-blue)
![Devices](https://img.shields.io/badge/Devices-IKEA%20Styrbar%20(E2001%20%7C%20E2002%20%7C%20E2313)-green)
![Author](https://img.shields.io/badge/Author-Xat0X-orange)

## 🌟 Why this blueprint?

Most blueprints limit you to controlling one specific group of lights. If you want to control the living room ceiling light, but also want to dim the reading lamp with the exact same remote, you usually need a second remote. **This blueprint fixes that.**

### Key Features
*   📱 **Universal Compatibility**: Works flawlessly with all Styrbar models (`E2001`, `E2002`, and the new AAA-battery `E2313`).
*   🔄 **Multi-Device Control**: Use the **Left** and **Right** buttons to cycle through your selected lights or switches.
*   👁️ **Visual Feedback**: The selected light will briefly blink, so you always know exactly which device you are controlling before you change the brightness.
*   🌊 **Advanced Smooth Dimming**: Optional transition-based smooth dimming. Configure step size and transition time (up to 2 seconds) per entity.
*   🛡️ **Dimming Threshold**: Never accidentally turn your lights off when dimming down! Set a minimum brightness threshold (e.g., 1%).
*   ⚡ **Custom Long-Press Actions**: Fully customizable actions for holding or releasing the Left and Right arrow buttons.

---

## 📋 Requirements

1.  **Home Assistant** (2024.x or newer).
2.  **IKEA Styrbar Remote** connected via **Zigbee2MQTT**.
    *   Supported models: `E2001`, `E2002`, `E2313`.
3.  **Input Number Helper (CRITICAL):**
    *   You **MUST** create an `input_number` helper in Home Assistant (Settings -> Devices & Services -> Helpers).
    *   Set Minimum to `0`, Maximum to `10` (or higher, depending on how many lights you want to control), and Step size to `1`.
    *   This helper acts as the remote's "memory" to remember which light is currently selected.

---

## 🚀 Installation

### Option 1: Direct Import (Recommended)
1.  Click the badge below to import the blueprint directly into your Home Assistant instance.
    [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FXat0X%2Fha-blueprint-ikea-styrbar%2Fblob%2Fmain%2Fikea_styrbar_multiple_entities.yaml)
2.  Click **"Preview Blueprint"** and then **"Import Blueprint"**.

### Option 2: Manual Installation
1.  Copy the code from the `ikea_styrbar_multiple_entities.yaml` file.
2.  Go to your Home Assistant config folder: `/config/blueprints/automation/xat0x/`.
3.  Create a file named `ikea_styrbar_multiple_entities.yaml` and paste the code.
4.  Go to **Developer Tools** -> **YAML** -> **Reload Automations**.

---

## ⚙️ Configuration Guide

Create a new automation using this blueprint. The settings are organized intuitively:

### 1. 🎛️ Devices & Targets
*   **Styrbar switch remote**: Select your IKEA Styrbar remote.
*   **Light/Switch Targets**: Select ALL the individual lights and switches you want to control.
*   **Selected Light/Switch Helper**: Select the `input_number` helper you created in the requirements step.

### 2. 💡 Brightness & Dimming
*   **Force Brightness**: Always turn a light on at a specific brightness level.
*   **Smooth Dimming**: Enable transition-based dimming instead of instant step-jumps.
*   **Smooth Dimming Targets**: Apply smooth dimming to all lights, or only specific selected entities.
*   **Prevent turning off when dimming**: Stop the remote from turning a light off when holding the dim-down button.

### 3. ⚡ Custom Actions
*   **Arrow Left/Right Hold**: Define what happens when you long-press the arrow buttons (e.g., control media players or trigger a scene).
*   **Arrow Left/Right Release**: Define what happens when you release the long-press.

---

## 🛡️ How it works

### Scenario 1: Switching Lights
1.  You walk into the room and want to control the reading lamp instead of the ceiling light.
2.  You press the **Right Arrow** button on the Styrbar.
3.  The system increments the `input_number` helper.
4.  The reading lamp briefly turns off and on (blinks) to visually confirm it is now the active target.
5.  You press the **Top** button, and only the reading lamp turns on.

### Scenario 2: Dimming down safely
1.  You hold the **Bottom** button to dim the lights for a movie.
2.  The brightness smoothly transitions down.
3.  Because *Prevent turn off when dimming* is enabled, the brightness stops exactly at 1% and does not turn off completely, even if you keep holding the button.

---

## ❓ FAQ

**Q: My remote doesn't do anything when I press the arrow buttons!**
A: Check if you have created and assigned the `input_number` helper. Without this helper, the blueprint cannot remember which light to control.

**Q: Can I use this with ZHA instead of Zigbee2MQTT?**
A: This specific blueprint is highly optimized for the MQTT action payloads generated by **Zigbee2MQTT**. It will not work out-of-the-box with ZHA.

**Q: I have the new AAA-battery Styrbar (E2313), will it work?**
A: Yes! As of version 1.5, the device filters have been relaxed so the newer E2313 is fully supported alongside the older coin-cell versions.

---

## ⚠️ Disclaimer

**Use at your own risk.**

This blueprint is provided "as is", without warranty of any kind. 

**Created with ❤️ by Xat0X**
