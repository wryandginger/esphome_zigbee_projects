# Zigbee ESPHome Projects
This Repo Contains ESPHome YAML configurations and other files that might be useful in building Zigbee devices using ESPHome 2026.7.3+

As of 8/4/2026, these **ONLY** compile on ESPHome 2026.7.3, you must use this version or newer. This is **NOT** backwards compatible with older versions of ESPHome.

## 🆕 Starting from scratch? 
If you don't have any sensors built yet, feel free to follow these guides. 

If you have some experience with ESPHome, you might want to just jump to luar123's [zigbee_esphome external component.](https://github.com/luar123/zigbee_esphome) and use the basic mode.

## ❓ Planning to update? 
<details>
<summary>Click to expand</summary>
  
If you have already compiled an older version and your devices are working: 

### ⚠️ Proceed with Caution!

First, please practice gratitude; you have working sensors. If you're **really sure** you want to risk not having working sensors, then proceed. (This is totally a note for myself 🤦‍♂️).

ESPHome 2026.7+ and updates to the Zigbee external component switches to a newer Zigbee SDK (ZBOSS -> ESP Zigbee SDK 2.0). All of the configuration files had to change to accommodate this change. Presently, routers on SDK 2.0 produce significant network issues. To improve network stability, most non-motion sensors have a hard throttle of 60 seconds. As a result sensors have been rearranged, endpoints are a little different, and the partitions file is no longer required. You will probably need to change automations or purge sensor data if you update your configs

**NOTE:** Even with these changes, SDK 2.0 creates a Zigbee black hole, causing most commercial devices to enter a panic mode. Sonoff, Gledopto, and Hue devices will rapidly disconnect and attempt to reconnect to the network. Over 3-4 hours the entire network collapses and/or ZHA stops listening to SDK 2.0 routers. You may switch between branches without much fuss.

If you plan on making an **end device** (no routing), then you are safe to use SDK 2.0:
```
external_components:
  - source: github://luar123/zigbee_esphome
    components: [zigbee]

zigbee:
  id: "zb"
  router: false 
```

If you **NEED routing**, you must use the 1.x branch as the SDK 2.0 creates a routing black hole:

```
external_components:
  - source: github://luar123/zigbee_esphome/tree/v1.x
    components: [zigbee]

zigbee:
  id: "zb"
  router: true
```

# Friendly Reminder:
Be warned, ESPHome will **ALWAYS** break non-standard/custom integrations on a new version.
As a rule, you should NEVER trust software updates will work as intended. Always make several backups (including yaml files, encryption keys, etc.).

To save yourself a lot of frustration and anger, you should ALWAYS freeze any working version of ESPHome by using [khendrick's ESPHome legacy addons](https://github.com/khenderick/esphome-legacy-addons)
(i.e. Before a new monthly release, install the current month's legacy add-on. Doing things this way will allow you beta test future versions until everything can correctly compile on your specialized hardware.)

If you are having issues with ZHA, take a look at some tips I created here: [zhatips.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/zhatips.md) 

# Firmware Updates:
Firmware cannot be sent via Zigbee OTA at this time. Updates only work via USB/UART using the procedure below. You do not need to constantly update your devices on ESPHome, unless there's a compelling reason. 

For example, ESPHome 2026.2 improves system resource usage and system event processing times, so it might make your mesh happier.

1. ALWAYS clear build files in ESPHome AND
2. Fully ERASE the device's flash memory by using the [ESP Tool](https://espressif.github.io/esptool-js/) before you
3. Update your device's firmware and
4. ALWAYS delete and re-pair any device you update.

</details>

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
* [esp32H2.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/esp32H2.md) 
Contains instructions for a basic router and LED light using a generic [ESP32-H2-DevKitM-1-N4S](https://www.amazon.com/Teyleten-Robot-ESP32-H2-DevKitM-1-N4-ESP32-H2-Development/dp/B0CHP8TS1S/).
