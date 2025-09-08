# Zigbee ESPHome Projects

This Repo Contains ESPHome YAML configurations and other files that might be useful in building Zigbee devices using ESPHome 2025.7.5

Note: ESPHome 2025.8.1+ breaks [I2C](https://github.com/esphome/esphome/issues/10498) and [UART using esp-idf](https://github.com/esphome/esphome/issues/10515) -- Be warned, ESPHome will ALWAYS break non-standard/custom integrations on a new version.

As a rule, you should NEVER trust software updates will work as intended. Always make several backups (including yaml files, encryption keys, etc.).

To save yourself a lot of frustration and anger, you should ALWAYS freeze any working version of ESPHome by using [khendrick's ESPHome legacy addons](https://github.com/khenderick/esphome-legacy-addons)
(i.e. Before a new monthly release, install the current month's legacy add-on. Doing things this way will allow you beta test future versions until everything can correctly complile on your specialized hardware.)

These instructions work with the ESPHome 2025.7 legacy addon as of 9/1/2025:

Troubleshoot by clearing build files and erasing flash memory by using the [ESP Tool](https://espressif.github.io/esptool-js/)


-----------------------------

This is made possible by the hard work of @luar123  for the [zigbee_esphome external component.](https://github.com/luar123/zigbee_esphome)

A lot of the code is based on examples in the github repo above, but I was having some issues getting started and a lot was discovered by trial and error. I'd like to save you some time and frustration.

# [m5stack.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/m5stack.md)
Contains instructions for making lights and sensors for the M5Stack NanoC6

# [xiao.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/xiao.md)
Contains instructions for using the XIAO MR60BHA2 60GHz mmWave Human Breathing and Heartbeat Sensor Kit 

# [waveshare.md](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/waveshare.md) 
Contains instructions for using the Waveshare ESP32-C6-DEV-KIT-N8 (and likely other makers too) to make multi sensors
