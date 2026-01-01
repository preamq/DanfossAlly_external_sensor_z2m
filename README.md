# Danfoss Ally External Temperature Sensor Integration

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fpreamq%2FDanfossAlly_external_sensor_z2m%2Fblob%2Fmain%2FAlly_external_sensor.yaml)

This Home Assistant blueprint automates the integration of an external temperature sensor with a Danfoss Ally thermostat using Zigbee2MQTT. It ensures accurate room temperature reporting by converting sensor values to the thermostat's required format and managing periodic updates.

## Features

- Automatic temperature scaling (multiplied by 100 for thermostat compatibility)
- Real-time updates on sensor state changes
- Periodic refresh via configurable timer (recommended 10-30 minutes)
- Battery optimization by reducing unnecessary updates
- Automatic detection of thermostat's external measured room sensor

## Requirements

- **Home Assistant**: Version 2024.12.0 or later
- **Zigbee2MQTT**: Properly configured and running
- **Danfoss Ally Thermostat**: Integrated via Zigbee2MQTT (not Deconz or ZHA)
- **External Temperature Sensor**: Any temperature sensor reporting in Celsius (°C)
- **Helpers**:
  - Input Number helper (for storing scaled temperature)
  - Timer helper (for periodic updates)

## Installation

1. Click the "Import Blueprint" button above or manually download `Ally_external_sensor.yaml`
2. In Home Assistant, go to **Settings > Automations & Scenes > Blueprints**
3. Import the blueprint from URL or file
4. Create the required helpers as described below

## Setup Guide

### 1. Create Required Helpers

Go to **Settings > Devices & Services > Helpers > Create Helper**

#### Number Helper (Temperature Scaling)
- **Name**: `Temperature Scaling Helper` (or similar)
- **Display mode**: Input
- **Step**: 1
- **Min value**: -8000
- **Max value**: 3500
- **Unit**: (leave blank)

#### Timer Helper (Periodic Updates)
- **Name**: `Temperature Update Timer` (or similar)
- **Restore on restart**: Enabled (recommended)

### 2. Configure the Blueprint

When creating an automation from this blueprint, configure these inputs:

- **Temperature sensor**: Select your external temperature sensor (must report in °C)
- **Integer helper**: Select the Number helper you created
- **Timer helper**: Select the Timer helper you created
- **Timer duration**: Set between 10-30 minutes (see notes below)
- **Danfoss Ally thermostat**: Select your thermostat device (must be Zigbee2MQTT integrated)

## Usage

Once configured, the automation will:

1. Monitor your temperature sensor for changes
2. Scale the temperature value by 100 (e.g., 21.5°C → 2150)
3. Update both the helper and thermostat's external sensor
4. Restart the timer for the next periodic check

The thermostat will use this external temperature for more accurate climate control.

## Notes

- **Timer Duration**: Must be at most 30 minutes to comply with Zigbee2MQTT and battery-powered sensor limitations
- **Temperature Units**: Sensor must report in Celsius (°C). Fahrenheit sensors are not supported
- **Thermostat Compatibility**: Only works with Danfoss Ally thermostats via Zigbee2MQTT integration
- **Battery Life**: Longer timer durations (20-30 minutes) help preserve sensor battery life
- **Accuracy**: The blueprint rounds temperatures to the nearest 0.01°C for precision

## Troubleshooting

### Automation Not Triggering
- Verify the temperature sensor is updating and reporting valid numeric values
- Check that the sensor's device_class is set to "temperature"
- Ensure the thermostat device is properly integrated via Zigbee2MQTT

### Thermostat Shows Wrong Temperature
- Confirm the external measured room sensor entity was found correctly (check automation trace)
- Verify the temperature scaling (value should be temperature × 100)
- Check Zigbee2MQTT logs for any communication issues

### Timer Not Working
- Ensure the timer helper is not paused or finished
- Check that the timer duration is within 10-30 minutes
- Verify the timer entity is correctly selected in the blueprint

### Blueprint Import Errors
- Ensure you're using Home Assistant 2024.12.0 or later
- Check for YAML syntax errors in the blueprint file
- Remove any unsupported keys if present (like `author`, `version`, `min_version`)

## Contributing

Feel free to submit issues or pull requests for improvements. Please include:
- Home Assistant version
- Zigbee2MQTT version
- Blueprint configuration details
- Automation trace logs when reporting bugs

## License

This blueprint is provided as-is for the Home Assistant community. Use at your own risk.
