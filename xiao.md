
# XIAO MR60BHA2 60GHz mmWave Human Breathing and Heartbeat Sensor Kit
Use xiao.yaml and customize as needed.

Note: This will work on ZHA, but is not working on Z2M without writing your own handler.
This is also confirmed to NOT work with Hue, Sonoff, and Tuya gateways.

# For xiao.yaml:
You will need
* [XIAO MR60BHA2](https://www.amazon.com/dp/B0F3CCM5P6?ref=ppx_yo2ov_dt_b_fed_asin_title) ~$26 plus tax and shipping
* that's it!

# Install Instructions
1. Remove the 3d printed back cover.
2. Plug a USB-C cable into the XIAO module, not the port closest to the grove port.
3. Go to github and download partitions_zb.csv then place in /config/esphome
4. Prep your device in esphome. I usually just select ESP32-C6 and skip everything.
5. Replace the new YAML file with the desired config from this repo and build your project. Note: No WiFi or OTA are available so any flashing has to be done via USB. Press and hold the button as you plug in the USB cable if you need to get into the bootloader.

Pro-Tip: You only need to keep one YAML file in ESPHome per device model/configuration that you're deploying on your network.

The YAML reports the device name as your model name and ESPhome as the manufacturer. Zigbee expects multiple devices with the manufacturer/model, so it's fine. This saves clutter and limits the offline devices in your ESPHome dashboard.

# Pairing to a Zigbee Network
The device should then pair to ZHA right away and you should see the sensors along with the LED. This may pair with Z2M, but I've been told the Analog Inputs will not appear. 

By default these YAML files configure this as a router, but you can disable that line and make this an end device, but if you're going to keep it powered all the time a repeater is a good idea, I think. These work fine as repeaters, but their range isn’t great.

To Reset/Set to Pairing (Only needed if you fiddle with the code a bunch):

1. Press the button for 3+ seconds
2. Release for 1+ seconds
3. Power cycle if it doesn't pair right away.

# Please adapt, test, and share!
If you can test, please tell me if this code does or does not work on Z2M, Hue, or any other hub you might have access to. I'll update this repo with any new information I have as I test the stability of these as routers.

Confirmed NOT working:
* eWeLink/Sonoff ZBBridge - fails to be discovered on versions 1.4-1.7
* Hue - requires some special keys to be added
