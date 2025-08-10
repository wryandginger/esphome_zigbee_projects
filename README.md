# esphome_zigbee
Zigbee ESPHome Projects

This Repo Contains ESPHome YAML configurations and other files that might be useful in building Zigbee devices using ESPHome 2025.7.5 (and newer, probably?)
This is made possible by the hard work of @luar123  for the zigbee_esphome external component. (github://luar123/zigbee_esphome)

A lot of the code is based on examples in the github repo, but I was having some issues getting started. I thought I would share my configuration to save some folks time and effort. (This is so heckin' cool!)

Parts used in this repo:

For m5stackc6-sk6812-zb.yaml:

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.

* [(Mouser) M5Stack A035 - 15 LED 10CM RGBIC Strip](https://www.mouser.com/ProductDetail/M5Stack/A035?qs=81r%252BiQLm7BR9%252BrYGJ%2Fehhw%3D%3D) ~$5 before tax, shipping, and tariffs of about 50 cents.

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents.

Note: Prices as of Aug 2025 and may vary. I recommend buying a bunch of modules from Mouser to make the shipping costs worth it. You can buy the C6 module from Amazon, but you'll pay triple. 


For m5stackc6-ws2812-zb.yaml

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.
  
* [(Amazon) BTF-LIGHTING RGB IC WS2812B USB Lights (https://www.amazon.com/dp/B0CCVPLZ1R) ~$12 before tax and shipping. Currently not on sale, but any WS2812B string will work. This config is for a 66 LED 16ft string. 

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents.
  

For m5stackc6-bme280-zb.yaml:

* [(Mouser) M5NanoC6](https://www.mouser.com/ProductDetail/M5Stack/C125?qs=jRuttqqUwMQ%2FdHvdW%2FFIaw%3D%3D) ~$6 before tax, shipping, and tariffs of about 50 cents.
  
* [(Amazon) BME280](https://www.amazon.com/Pre-Soldered-Atmospheric-Temperature-GY-BME280-3-3-MicroControllers/dp/B0BQFV883T) ~$12 before tax and shipping. (Don't buy this. I'm just using leftover parts from an older project. You should Get a M5stack BME688 module at Mouser.)

* [(Mouser) M5Stack Grove Cable](https://www.mouser.com/ProductDetail/M5Stack/A034-D?qs=81r%252BiQLm7BQIX3ZPS9TpAA%3D%3D)  ~$2 before tax, shipping, and tariffs of about 25 cents.
  

1. Once you have your materials, connect your LED strip to the Grove cable, and the cable to the module. (For WS2182 and BME280, cut the grove cable in half and connect your 5V, GND, and data pins to the red, black, and yellow grove cables.
2. Go to github and download [partitions_zb.csv](https://github.com/luar123/zigbee_esphome/blob/8ee9eaaabacd722b3689690a91485f35514518ec/partitions_zb.csv)
then place in /config/esphome
3. Prep your device in esphome. I usually just select ESP32-C6 and skip everything.
4. Replace the new YAML file with the desired config from this repo and build your project.
