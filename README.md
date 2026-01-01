   This blueprint automates the integration of an external temperature sensor with a Danfoss Ally thermostat via Zigbee2MQTT.
    It converts the temperature sensor value to the required format (multiplied by 100) and updates the thermostat's external measured room sensor.
    The automation triggers on sensor state changes, with optimizations to reduce reporting frequency (10-30 minutes) and only when temperature deviates significantly.
    It also manages a timer helper to periodically refresh the temperature data.

<a href="https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fpreamq%2FDanfossAlly_external_sensor_z2m%2Fblob%2Fmain%2FAlly_external_sensor.yaml" target="_blank" rel="noreferrer noopener"><img src="https://my.home-assistant.io/badges/blueprint_import.svg" alt="Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled." /></a>
