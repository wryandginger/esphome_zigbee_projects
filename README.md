# esphome_zigbee - Zigbee ESPHome Projects

This Repo Contains ESPHome YAML configurations and other files that might be useful in building Zigbee devices using ESPHome 2025.7.5 (and newer, probably?)

This is made possible by the hard work of @luar123  for the zigbee_esphome external component. (github://luar123/zigbee_esphome)

A lot of the code is based on examples in the github repo, but I was having some issues getting started and a lot was discovered by trial and error. I'd like to save you some time and frustration.

Note: Prices as of Aug 2025 and may vary. I recommend buying a bunch of modules from Mouser to make the shipping costs worth it. You can buy the C6 module from Amazon, but you'll pay triple. 


# For m5stackc6-sk6812-zb.yaml:

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.

* [(Mouser) M5Stack A035 - 15 LED 10CM RGBIC Strip](https://www.mouser.com/ProductDetail/M5Stack/A035?qs=81r%252BiQLm7BR9%252BrYGJ%2Fehhw%3D%3D) ~$5 before tax, shipping, and tariffs of about 50 cents.

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents.

I also created a 3D printable cylander lamp that snugly fits the NanoC6 module and the LED 



# For m5stackc6-ws2812-zb.yaml

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.
  
* [(Amazon) BTF-LIGHTING RGB IC WS2812B USB Lights](https://www.amazon.com/dp/B0CCVPLZ1R) ~$12 before tax and shipping. Currently not on sale, but any WS2812B string will work. This config is for a 66 LED 30ft string. 

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents.


# For m5stackc6-bme280-zb.yaml:

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.
  
* [(Amazon) BME280](https://www.amazon.com/Pre-Soldered-Atmospheric-Temperature-GY-BME280-3-3-MicroControllers/dp/B0BQFV883T) ~$12 before tax and shipping. (Don't buy this. I'm just using leftover parts from an older project. You should just buy a M5stack BME688 module at Mouser.)

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents.
  
# Install Instructions

1. Once you have your materials, connect your LED strip to the Grove cable, and the cable to the module. (For WS2182 and BME280, cut the grove cable in half and connect your 5V, GND, and data pins to the red, black, and yellow grove cables.
2. Go to github and download [partitions_zb.csv](https://github.com/luar123/zigbee_esphome/blob/8ee9eaaabacd722b3689690a91485f35514518ec/partitions_zb.csv)  then place in /config/esphome
3. Prep your device in esphome. I usually just select ESP32-C6 and skip everything.
4. Replace the new YAML file with the desired config from this repo and build your project.
   Note: No WiFi or OTA are available so any flashing has to be done via USB. Press and hold the button as you plug in the USB cable if you need to get into the bootloader.

# Pairing to a Zigbee Network
The device should then pair to ZHA right away. I don’t have Z2M, so you’ll have to test this, but I believe this would work just fine. 

By default these YAML files configure your C6 module as a router, but you can disable that line and make this an end device, but if you're going to keep it powered all the time as a lamp making this a repeater is a good idea, I think. These work fine as repeaters, but their range isn’t great.

For the LED yaml files the code exposes:

* The LED strip as an RGB bulb,
* NanoC6 button as an RGB Bulb
* The blue LED as a standard ON/OFF bulb.
* 6 on/off switches that activate RGBIC lighting effects.
* The internal module temperature as a sensor
* These can all be controlled via ZHA as any other LED devices.

The Nano C6 Button does the following:

* One click: Hue-style color loop
* Double-click: RGBIC rainbow effect on the strip and button
* Triple-click: RGBIC chase effect on the strip and rainbow for the button

To Reset/Set to Pairing (Only needed if you fiddle with the code a bunch):

1. Press the button for 3+ seconds
2. Release for 1+ seconds
3. Press for 3+ seconds
4. Release for 1+ seconds
   
The lights should then turn off. Unplug/Plug in the NanoC6 and you’re back in pairing mode.

# Please adapt, test, and share!
If you can test, please tell me if this code does or does not work on Z2M, Hue, or any other hub you might have access to. I'll update this repo with any new information I have as I test the stability of these as routers.
