# Zigbee ESPHome Projects
This Repo Contains ESPHome YAML configurations and other files that might be useful in building Zigbee devices using ESPHome 2025.12.2

# Compatibility Notes: 
Minimum requirements are ESPHome 2025.7 but this code may not compile correctly on that version.
As of 2/2/2026 these configuration files will compile on ESPHome version 2026.1.6, as long as you follow the directions.

Be warned, ESPHome will ALWAYS break non-standard/custom integrations on a new version.
As a rule, you should NEVER trust software updates will work as intended. Always make several backups (including yaml files, encryption keys, etc.).

To save yourself a lot of frustration and anger, you should ALWAYS freeze any working version of ESPHome by using [khendrick's ESPHome legacy addons](https://github.com/khenderick/esphome-legacy-addons)
(i.e. Before a new monthly release, install the current month's legacy add-on. Doing things this way will allow you beta test future versions until everything can correctly compile on your specialized hardware.)

If you are having issues with ZHA, take a look at some tips I created here: [zhatips.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/zhatips.md) 

# Firmware Updates:
Firmware cannot be sent via Zigbee OTA at this time. Updates only work via USB/UART using the procedure below. You do not need to constantly update your devices on ESPHome, unless there's a compelling reason. 
For example, ESPHome 2025.11 improves system resource usage and system event processing times.

1. ALWAYS clear build files in ESPHome AND
2. Fully ERASE the device's flash memory by using the [ESP Tool](https://espressif.github.io/esptool-js/) before you
3. Update your device's firmware and
4. Be prepared to delete and re-pair any device you update.

# Acknowledgements:
This is made possible by the hard work of @luar123  for the [zigbee_esphome external component.](https://github.com/luar123/zigbee_esphome)
A lot of the code is based on examples in the github repo above, but I was having some issues getting started and a lot was discovered by trial and error. I'd like to save you some time and frustration.

# Installation Instructions:
These are sorted by devkit manufacturer and function.

* [m5stack.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/m5stack.md)
Contains instructions for making lights using the M5Stack NanoC6
* [xiao.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/xiao.md)
Contains instructions for using the XIAO MR60BHA2 60GHz mmWave Human Breathing and Heartbeat Sensor Kit 
* [waveshare.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/waveshare.md) 
Contains instructions for using the Waveshare ESP32-C6-DEV-KIT-N8 (and likely other makers too) to make multi sensors. (Uses LD2410B, BME680, and generic lux sensors)
* [esp32H2.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/esp32h2.md) 
Contains instructions for a basic router and LED light using a generic [ESP32-H2-DevKitM-1-N4S](https://www.amazon.com/Teyleten-Robot-ESP32-H2-DevKitM-1-N4-ESP32-H2-Development/dp/B0CHP8TS1S/).
