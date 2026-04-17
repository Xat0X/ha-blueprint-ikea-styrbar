# 🎛️ IKEA Styrbar - Control Multiple Entities (Zigbee2MQTT)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FXat0X%2Fha-blueprint-ikea-styrbar%2Fblob%2Fmain%2Fikea_styrbar_multiple_entities.yaml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A highly advanced and flexible **Home Assistant Blueprint** for the IKEA Styrbar remote control. 
This blueprint allows you to control **multiple lights or switches** using a single Styrbar remote via **Zigbee2MQTT**. It supports all hardware revisions, including the newer **E2313** model!

---

## ✨ Key Features

* **📱 Universal Compatibility:** Works seamlessly with all Styrbar models (`E2001`, `E2002`, and the new AAA-battery `E2313`).
* **🔄 Multi-Device Control:** Cycle through multiple selected lights or switches using the Left/Right arrow buttons.
* **👁️ Visual Feedback:** When switching to a new target, the light/switch will briefly blink to let you know which device is currently selected.
* **🌊 Smooth Dimming:** Optional transition-based smooth dimming. Configure step size and transition time (up to 2 seconds).
* **🛡️ Prevent Turn-Off When Dimming:** Never accidentally turn your lights off when dimming down! You can set a minimum brightness threshold (e.g., 1%).
* **💡 Force Brightness:** Option to always turn a light on at a specific brightness level.
* **🛠️ Custom Long-Press Actions:** Assign your own custom Home Assistant actions when holding or releasing the Left or Right arrow buttons.

---

## ⚙️ How it works (Target Switching)

The core magic of this blueprint is how it handles multiple lights. Instead of turning all lights on or off at the same time, you use the **Left** and **Right** buttons to cycle through your devices. 

To remember which light you are currently controlling, the blueprint uses an `input_number` helper.
1. Press `Left` or `Right` to select a different light.
2. The newly selected light will blink.
3. Use `On/Off` or `Dim Up/Down` to control *only* that specific light!

---

## 🛠️ Prerequisites & Setup

Before you import and use this blueprint, you need to create a simple helper in Home Assistant.

### Step 1: Create an Input Number Helper
This helper acts as the memory for the remote so it knows which light is currently selected.
1. Go to **Settings** -> **Devices & Services** -> **Helpers**.
2. Click **+ CREATE HELPER** and select **Number**.
3. Fill in the details:
   * **Name:** `Styrbar Active Target` *(or whatever you prefer)*
   * **Minimum value:** `0`
   * **Maximum value:** `10` *(Make sure this is higher than the total amount of lights you want to control)*
   * **Step size:** `1`
4. Click **Create**.

### Step 2: Import the Blueprint
Click the blue **Import Blueprint** button at the top of this page, or import the `ikea_styrbar_multiple_entities.yaml` URL directly into Home Assistant.

### Step 3: Create the Automation
1. Go to **Settings** -> **Automations & Blueprints** -> **Blueprints**.
2. Find this blueprint and click **Create Automation**.
3. **Select your remote:** Choose your Styrbar remote from the dropdown.
4. **Select your Targets:** Add all the lights and switches you want to control.
5. **Select your Helper:** Choose the `input_number` helper you created in Step 1.
6. Configure any extra settings (like Smooth Dimming or Minimum Brightness) to your liking!

---

## 📝 Changelog

**Version 1.5**
- 🐛 Fixed device selection for newer Styrbar models (E2313) by relaxing the device manufacturer/model selector in Zigbee2MQTT.

**Version 1.4**
- ✨ Added "Prevent turning off when dimming" feature with a configurable threshold slider.
- 🌊 Improved smooth dimming (max 2s transition) and added per-entity smooth dimming selection.
- 🎯 Fixed group expansion: Raw targets are kept intact so group entities are treated as single targets.

---
*Happy Automating! 🚀*
