# Waveshare ESP32-C6-DEV-KIT-N8
These are projects that use the larger ESP32-C6 Dev Kit to make multi sensors.

I call these panopticon devices in reference to [Jeremy Bentham](https://en.wikipedia.org/wiki/Jeremy_Bentham) and [Michel Foucault](https://en.wikipedia.org/wiki/Discipline_and_Punish).
They literally watch multiple things, including you.  

Note: This will work on ZHA, but is not working on Z2M without writing your own handler.
This is also confirmed to NOT work with Hue, Sonoff, and Tuya gateways.

!! These devices may be "chatty" !! 

This means they might be sending a lot of messages via your Zigbee network causing slowness/instability/crashing.
Adjustments have been made to reduce the amount of network chatter, but you may need to change reporting times or remove zigbee attributes to maintain stability on your setup.

The PMS5003 and LD2410 modules (especially in Engineering Mode) are the worst offenders. So if your Zigbee network crashes, reports RF interference, or constantly re-initializes: 
1. Disconnect all Panopticon devices from power. 
2. Manually disable ZHA.
3. Manually restart your Zigbee network coordinator and/or Home Assistant.
4. Re-enable ZHA and monitor logs.
5. Adjust your device configuration to report less data, either by reducing reporting times or by reducing the amount of sensors/attributes pushed via Zigbee. 

# For [pms.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/pms.yaml) and [panopticon-pms-bsec2.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/panopticon-pms-bsec2.yaml):
You will need
* [ESP32-C6 Dev Kit](https://www.amazon.com/Waveshare-Microcontroller-Development-Single-Core-ESP32-C6-WROOM-1-N8/dp/B0CKR2LF83/) ~$11
* [HLK-LD2410-B 20GhZ mmWave Sensor with cable](https://www.amazon.com/JESSINIE-HLK-LD2410B-P-Presence-Bluetooth-LD2410B/dp/B0C36FRVHR) ~$11
* [PMS5003 Particulate Matter Sensor](https://www.amazon.com/BestParts-Digital-Particle-Concentration-PMS5003/dp/B0B1DQKV4N) ~$21
* [BME 680 Temp, Humdidity, Pressure, and Gas Resistance Sensor with cable](https://www.amazon.com/dp/B0BZ4W6J49?ref=nb_sb_ss_w_as-reorder_k0_1_6&amp=&crid=53Z8SLZ0MUP6&sprefix=bme680&th=1) ~$18
* [SSD1306 .96 in I2C display](https://www.amazon.com/Display-SSD1306-Self-Luminous-Compatible-Raspberry/dp/B0DY5DS8HK) ~$5/ea
* DuPont cables and wago connectors  (or some electrical tape)
* Use the PMSbox.stl and boxlid.stl to print a project box that hides everything neatly. (I recommend printing in Clear PLA)

# For [co2.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/co2.yaml) and [panopticon-co2-bsec2.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/panopticon-co2-bsec2.yaml):
You will need
* [ESP32-C6 Dev Kit](https://www.amazon.com/Waveshare-Microcontroller-Development-Single-Core-ESP32-C6-WROOM-1-N8/dp/B0CKR2LF83/) ~$11
* [HLK-LD2410-B 20GhZ mmWave Sensor with cable](https://www.amazon.com/JESSINIE-HLK-LD2410B-P-Presence-Bluetooth-LD2410B/dp/B0C36FRVHR) ~$11
* For CO2: [MHZ-19B/C](https://www.amazon.com/EC-Buying-Monitoring-Concentration-Detection/dp/B0CRKGP143) ~$25
* [BME 680 Temp, Humdidity, Pressure, and Gas Resistance Sensor with cable](https://www.amazon.com/dp/B0BZ4W6J49?ref=nb_sb_ss_w_as-reorder_k0_1_6&amp=&crid=53Z8SLZ0MUP6&sprefix=bme680&th=1) ~$18
* [SSD1306 .96 in I2C display](https://www.amazon.com/Display-SSD1306-Self-Luminous-Compatible-Raspberry/dp/B0DY5DS8HK) ~$5/ea
* DuPont cables and wago connectors  (or some electrical tape)
* Use the CO2box.stl and boxlid.stl to print a project box that hides everything neatly. (I recommend printing in Clear PLA)

# For [panopticon-lux.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/panopticon-lux.yaml):
You will need
* [ESP32-C6 Dev Kit](https://www.amazon.com/Waveshare-Microcontroller-Development-Single-Core-ESP32-C6-WROOM-1-N8/dp/B0CKR2LF83/) ~$11
* [BH1750FVI Lux Sensor](https://www.amazon.com/dp/B0CQ2KBVRM) ~ $4
* [HLK-LD2410-B 20GhZ mmWave Sensor with cable](https://www.amazon.com/JESSINIE-HLK-LD2410B-P-Presence-Bluetooth-LD2410B/dp/B0C36FRVHR) ~$11
* [BME280](https://www.amazon.com/Pre-Soldered-Atmospheric-Temperature-GY-BME280-3-3-MicroControllers/dp/B0BQFV883T) ~$12 before tax and shipping.
* DuPont cables and wago connectors  (or some electrical tape)
* Just use the CO2box.stl, everything will fit.
* I don't know if you really need to use a Lux sensor if you also have an LD2410 module, but they're cheap.
  
# BSEC2 - [panopticon-pms-bsec2.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/panopticon-pms-bsec2.yaml) and [panopticon-co2-bsec2.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/panopticon-co2-bsec2.yaml)
These files use [Bosch's proprietary BSEC2 libary](https://github.com/boschsensortec/Bosch-BSEC2-Library). These offer IAQ/Air Quality and Sensor accuracy sensors in addition to Temperature, Humidity, Motion, etc.
The IAQ and Accuracy sensors have been slightly altered from the config examples offered by ESPHome by converting these to percentages.
The display also shows shorter/more readable AQI interpretations plus sensor accuracy. Display is in a better layout for readability.

Using/compiling these files is implicit acceptance of [Bosch's license agreement](https://www.bosch-sensortec.com/media/boschsensortec/downloads/software/bme688_development_software/2024_12/20241219_clickthrough_license_terms_bsec_bme680_bme688_bme690.pdf). ... tl;dr: 
* Don't use this outside of consumer settings/contexts (no industrial/medical/safety-critical uses). 
* You may sell a device with this library enabled in firmware, but you may not modify/disassemble/reverse-engineer Bosch's library.
* Don't give/sell the config to any military or a hostle/embargoed country.
* This is not legal advice. I am not your lawyer, nor am I your dentist.
* Compile at your own risk.


# Install Instructions
1. Splice the cables for the display and the BME 680 sensor. Ground to Ground, VCC to VCC, SDA to SDA, SCL to SCL
2. Splice the VCC/Power cable to the LD2410 and the PMS or CO2 sensor
3. Connect the I2C devices with sda: GPIO12 scl: GPIO13 and VCC on 3V
4. Connect the LD2410 with tx_pin: GPIO21 rx_pin: GPIO22 and out_pin: GPIO11
5. Connect the PMS or CO2 sensor with  tx_pin: GPIO19 rx_pin: GPIO18 (and set_pin GPIO11 for the PMS)
4. Plug a USB-C cable into the ESP32-C6 module.
5. Go to github and download partitions_zb.csv then place in /config/esphome
6. Prep your device in esphome. I usually just select ESP32-C6 and skip everything.
7. Replace the new YAML file with the desired config from this repo and build your project. Note: No WiFi or OTA are available so any flashing has to be done via USB. Press and hold the button as you plug in the USB cable if you need to get into the bootloader.

Pro-Tip: You only need to keep one YAML file in ESPHome per device model/configuration that you're deploying on your network.

The YAML reports the device name as your model name and ESPhome as the manufacturer. Zigbee expects multiple devices with the manufacturer/model, so it's fine. This saves clutter and limits the offline devices in your ESPHome dashboard.

# Pairing to a Zigbee Network
The device should then pair to ZHA right away and you should see the sensors along with the LED. This may pair with Z2M, but I've been told the Analog Inputs will not appear. 

By default these YAML files configure this as a router, but you can disable that line and make this an end device, but if you're going to keep it powered all the time a repeater is a good idea, I think. These work fine as repeaters, but their range isn’t great.

To Reset/Set to Pairing (Only needed if you fiddle with the code a bunch):

1. Press the boot button for 5+ seconds
2. Release for 1+ seconds
3. Power cycle if it doesn't restart and enter pairing mode.

# Please adapt, test, and share!
If you can test, please tell me if this code does or does not work on Z2M, Hue, or any other hub you might have access to. I'll update this repo with any new information I have as I test the stability of these as routers.
