# Zigbee ESPHome Projects for the M5Stack NanoC6


# For [m5stackc6-sk6812-zb.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/m5stackc6-sk6812-zb.yaml):

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.

* [(Mouser) M5Stack A035 - 15 LED 10CM RGBIC Strip](https://www.mouser.com/ProductDetail/M5Stack/A035?qs=81r%252BiQLm7BR9%252BrYGJ%2Fehhw%3D%3D) ~$5 before tax, shipping, and tariffs of about 50 cents.

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents.

# [sk6812-lamp.stl](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/[sk6812-lamp.stl) - a 3D Model (STL) of a lamp to use with the SK6812 (15 LED): 

* This is a 3D printable cylander lamp that snugly fits the NanoC6 module and the LED.
* Print using clear/transparent PLA at 5% infill and use Archimedes screw as your infill pattern for optimal light diffusion.
* Print time: 90 minutes on a FlashForge Adventurer 5MPro and sliced with OrcaSlicer.
* You can literally place this upside down, sideways, right side up, whatever you think looks best. Use the open channel in the back to tuck your cords out of view.
* This is brighter and more visually appealing than a Philips Hue Bloom.


# For [m5stackc6-ws2812-zb.yaml](https://github.com/wryandginger/esphome_zigbee_projects/blob/main/m5stackc6-ws2812-zb.yaml):

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.
  
* [(Amazon) BTF-LIGHTING RGB IC WS2812B USB Lights](https://www.amazon.com/dp/B0CCVPLZ1R) ~$12 before tax and shipping. Currently not on sale, but any WS2812B string will work. This config is for a 66 LED 30ft string. 

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents. (Other lengths and suppliers of grove cables are available. I usually make my own.)

Because this is a waterproof LED string, you can put these in a damp location IF your module stays well protected from the elements. I'm testing this outdoors in a waterproof electrical box.

# Install Instructions

1. Once you have your materials, connect your LED strip to the Grove cable, and the cable to the module. (For WS2182 and BME280, cut the grove cable in half and connect your 5V, GND, and data pins to the red, black, and yellow grove cables.
2. Go to github and download [partitions_zb.csv](https://github.com/luar123/zigbee_esphome/blob/8ee9eaaabacd722b3689690a91485f35514518ec/partitions_zb.csv)  then place in /config/esphome
3. Prep your device in esphome. I usually just select ESP32-C6 and skip everything.
4. Replace the new YAML file with the desired config from this repo and build your project.
   Note: No WiFi or OTA are available so any flashing has to be done via USB. Press and hold the button as you plug in the USB cable if you need to get into the bootloader.


Pro-Tip: You only need to keep one YAML file in ESPHome per device model/configuration that you're deploying on your network. 

* The YAML reports the device name as your model name and ESPhome as the manufacturer. Zigbee expects multiple devices with the manufacturer/model, so it's fine. This saves clutter and limits the offline devices in your ESPHome dashboard.

* You can customize the model and manufacturer if needed desired. For example, you could try mimicking the make/model of a supported device to troubleshoot (e.g., LEDVANCE FLEX RGBW, eWeLight ZB-CL01, or Signify Netherlands B.V. LCA003). Or, if you're planning to take everything on this repo and make some Etsy side hustle selling crystal zigbee desk lamps with your own custom brand name.    (Please don't do this otherwise bad karma will come to you.)


# Pairing to a Zigbee Network
The device should then pair to ZHA right away. I don’t have Z2M, so you’ll have to test this, but I believe this would work just fine. 

By default these YAML files configure your C6 module as a router, but you can disable that line and make this an end device, but if you're going to keep it powered all the time as a lamp making this a repeater is a good idea, I think. These work fine as repeaters, but their range isn’t great.

For the LED yaml files the code exposes:

* The LED strip as an RGB bulb,
* NanoC6 button as an RGB Bulb
* The blue LED as a standard ON/OFF bulb.
* 6 on/off switches that activate RGBIC lighting effects.
* The internal module temperature as a sensor (I'm using this to monitor that they're not overheating or catching fire, etc.)
* These can all be controlled via ZHA as any other LED devices.

The Nano C6 Button does the following:

* One click: Hue-style color loop for the LED strip
* Double-click: RGBIC rainbow effect on the LED strip
* Triple-click: RGBIC chase effect on the LED strip

To Reset/Set to Pairing (Only needed if you fiddle with the code a bunch):

1. Press the button for 3+ seconds
2. Release for 1+ seconds
3. Press for 3+ seconds
4. Release for 1+ seconds
   
The lights should then turn off. Unplug/Plug in the NanoC6 and you’re back in pairing mode.


Confirmed NOT working:
* eWeLink/Sonoff ZBBridge - NanoC6 fails to be discovered on versions 1.4-1.7
  I was able to get the device to pair once, but never responded to commands.
* Hue - requires some special keys to be added
