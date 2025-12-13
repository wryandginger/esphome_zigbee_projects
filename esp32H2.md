# Generic ESP32- H2-DEV-KIT-N4S router and light
These are projects that use the low power ESP32-H2 Dev Kit to make a generic router and RGB light with a few light effects that can be used for notification.

Note: This will work on ZHA, but is not working on Z2M without writing your own handler.
This is also confirmed to NOT work with Hue, Sonoff, and Tuya gateways.

# Troubleshooting Zigbee Network Crashing
If your Zigbee network crashes, reports RF interference, or constantly re-initializes be sure to reflash a clean configuration. (Clean build files and erase flash using esptool before reflashing using EPHome.)
This will fix the majority of issues you might have with custom devices. In-depth troubleshooting can be found with the ESP32C6 instructions.

# Build Notes
You will need
* [ESP32-H2-N4 Dev Kit](https://www.[amazon.com/Waveshare-Microcontroller-Development-Single-Core-ESP32-C6-WROOM-1-N8/dp/B0CKR2LF83/](https://www.amazon.com/Teyleten-Robot-ESP32-H2-DevKitM-1-N4-ESP32-H2-Development/dp/B0CHP8TS1S)) ~$10 for 3
* (Optional) A 3D printed enclosure or project box. There are plenty of designs that you can find on thingiverse, printables, etc. 

# Installation Instructions
1. Create a new configuration file in ESPHOME
2. Cut and paste this basic yaml configuration:

```
esphome:
  name: esp32-h2-router
  friendly_name: esp32-h2-router

esp32:
  board: esp32-h2-devkitm-1
  flash_size: 4MB
  partitions: partitions_zb.csv
  framework:
    type: esp-idf
    sdkconfig_options:
      CONFIG_ESPTOOLPY_FLASHSIZE_4MB: y
  variant: esp32h2

external_components:
  - source: github://luar123/zigbee_esphome
    components: [zigbee]

globals:
  - id: color_x
    type: float
    restore_value: no
    initial_value: '0'
  - id: color_y
    type: float
    restore_value: no
    initial_value: '0'


zigbee:
  id: "zb"
  router: true
  endpoints:
    - num: 1
      device_type: COLOR_DIMMABLE_LIGHT
      clusters:
        - id: ON_OFF
          attributes:
            - attribute_id: 0
              id: led_1
              type: bool
              on_value:
                then:                
                  - light.control:
                      id: led1
                      state: !lambda "return x;"
        - id: LEVEL_CONTROL
          attributes:
            - attribute_id: 0
              type: U8
              value: 255
              on_value:
                then:
                  - light.control:
                      id: led1
                      brightness: !lambda "return ((float)x)/255;"
        - id: COLOR_CONTROL
          attributes:
            - attribute_id: 3
              type: U16
              on_value:
                then:
                  - lambda: id(color_x) = (float)x/65536;
                  - light.control:
                      id: led1
                      red: !lambda "return zigbee::get_r_from_xy(id(color_x), id(color_y));"
                      green: !lambda "return zigbee::get_g_from_xy(id(color_x), id(color_y));"
                      blue: !lambda "return zigbee::get_b_from_xy(id(color_x), id(color_y));"
            - attribute_id: 4
              type: U16
              on_value:
                then:
                  - lambda: id(color_y) = (float)x/65536;
                  - light.control:
                      id: led1
                      red: !lambda "return zigbee::get_r_from_xy(id(color_x), id(color_y));"
                      green: !lambda "return zigbee::get_g_from_xy(id(color_x), id(color_y));"
                      blue: !lambda "return zigbee::get_b_from_xy(id(color_x), id(color_y));"
    - num: 2
      device_type: ON_OFF_OUTPUT
      clusters:
        - id: ON_OFF
          attributes:
            - attribute_id: 0
              type: bool
              on_value:
                then:   
                  - if:
                      condition: 
                        - light.is_off: led1
                      then: 
                        - light.turn_on:
                            id: led1
                            effect: random
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"
                      else:
                        - light.turn_off:
                            id: led1          
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"         
    - num: 3
      device_type: ON_OFF_OUTPUT
      clusters:
        - id: ON_OFF
          attributes:
            - attribute_id: 0
              type: bool
              on_value:
                then:   
                  - if:
                      condition: 
                        - light.is_off: led1
                      then: 
                        - light.turn_on:
                            id: led1
                            effect: quarter
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"
                      else:
                        - light.turn_off:
                            id: led1          
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"    
    - num: 4
      device_type: ON_OFF_OUTPUT
      clusters:
        - id: ON_OFF
          attributes:
            - attribute_id: 0
              type: bool
              on_value:
                then:   
                  - if:
                      condition: 
                        - light.is_off: led1
                      then: 
                        - light.turn_on:
                            id: led1
                            effect: full
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"
                      else:
                        - light.turn_off:
                            id: led1         
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"    
    - num: 5
      device_type: ON_OFF_OUTPUT
      clusters:
        - id: ON_OFF
          attributes:
            - attribute_id: 0
              type: bool
              on_value:
                then:   
                  - if:
                      condition: 
                        - light.is_off: led1
                      then: 
                        - light.turn_on:
                            id: led1
                            effect: pulse
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"
                      else:
                        - light.turn_off:
                            id: led1         
                        - zigbee.setAttr:
                            id: led_1
                            value: !lambda "return x;"    
light:
  - platform: esp32_rmt_led_strip
    rgb_order: GRB
    pin: GPIO08
    num_leds: 1
    chipset: WS2812
    rmt_symbols: 48
    id: "led1"
    name: "Board LED"
    icon: "mdi:led-outline"
    effects:
      - random:
      - pulse:
      - addressable_rainbow:
          name: full
          speed: 10
          width: 100
      - addressable_rainbow:
          name: quarter
          speed: 1
          width: 100

```
3. Save the config and install via USB.
4. After install the device should immediately enter pairing mode. 
