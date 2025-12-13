# Tips for Large Networks using Zigbee Home Automation (ZHA)
If you have a large network (75+ devices), you may experience ZHA performance issues like random crashing, unresponsive devices, or devices that become unavailable. This document covers some tips I've learned to improve the stability of my ZHA network.

For reference, I am using an SMLight SLZB-06 MR1. My network is running off the EFR32MG21 (Radio 1). Radio 2 is configured as a repeater for Radio 1.

# Check your Zigbee Channel
Most forums recommend using a Zigbee Light Link Channel (11, 15, 20, and 25), but I haven't experienced issues using others. ZHA will default to channel 20, but that might not be good for you.
Personally, I always choose Zigbee Channel 25. If you are unsure, you can get a readout of your network health by Downloading Diagnostics. (Refer to the "Reporting Issues" section of the [ZHA documentation](https://www.home-assistant.io/integrations/zha/))

After downloading, you should have a JSON file listing a ton of information about your network. Scroll about half-way through the file and look for "energy_scan": You should see something that looks like this:

```
    },
    "energy_scan": {
      "11": 55.9836862725909,
      "12": 82.35373987514762,
      "13": 82.35373987514762,
      "14": 39.90320178295578,
      "15": 25.74050169409602,
      "16": 5.317630506738386,
      "17": 25.74050169409602,
      "18": 1.0256846852618655,
      "19": 21.09014924761344,
      "20": 4.15070068297423,
      "21": 1.3262022905796567,
      "22": 10.914542804728702,
      "23": 1.1664179210724432,
      "24": 0.6123372955913717,
      "25": 75.96022321405563,
      "26": 28.30261646762903
    },

```
I am using channel 25, so that explains why it's at 75. If I were to change to a different channel, I would likely choose channel 20 or if I was still having issues, I'd try 24 or 18 next.

# Check your configuration.yaml file 
I recommend setting your network to source routing. This should work with all coordinators (except Conbee II, which crash with source routing).  
Here's my ZHA section with annotations:

```
zha:
  custom_quirks_path: /config/custom_zha_quirks/  # This is needed for a Tuya device that isn't yet supported by ZHA
  zigpy_config:
    source_routing: true                  # This is needed for speed/stability on larger zha networks
    handle_unknown_devices: true          # This provides better device compatibility.
    ota:
      extra_providers:
        - type: z2m                       # This enables the Zigbee2MQTT firmware update library. 
    ezsp_config:
      CONFIG_MAX_HOPS: 4                  # 5+ hops cause 3074 errors and increase network interference. 4 is ideal.
    ezsp_policies:
      TRUST_CENTER_POLICY: 0x0002         # Allows insecure rejoins for older Philips Hue sensors/switches.
  device_config:                          # This fixes a device I have which reports as a bulb but is really a switch.
    a4:c1:38:ad:b5:33:1b:ab-1:    
      type: "switch"
```

# Keep your coordinator free from interference

* If you are using a network coordinator like the SMLight or TubesZB models, keep your coordinator away from your WiFi router.
* Make sure your 2.4 GhZ WiFi isn't interfering with your Zigbee Network.  (WiFi Channel 1 is great with Zigbee Channel 25)
* If you are using USB serial or power, make sure you are using a USB 2.0 Port with a Shielded USB Cable and keep your coordinator away from the plug. (USB 3.0 Ports and USB power adapters can cause 2.4 GhZ interference.)

# Remove/disable unnecessary sensors and use repeaters on your network

* Several Tuya Devices have power consumption sensors that never report a value. These cause ZHA to do additional polls, increasing unnecesary traffic. Disable any of these junk sensors.
* I have read there is a bug in ZHA that causes power reporting devices to flood the network with updates. Disable any of those you don't need/use.
* Any sensor you are not using is just extra traffic that bogs down your network.
* Most smart plugs and light bulbs (except Sengled) will work as a repeater, make sure you have a few in each room to strengthen your mesh.
* Too many dedicated repeaters or the wrong kind of repeater can cause issues (Personally, I avoid using Tuya or Ikea repeater devices.) The ESP32-H2 seems to work fine as a repeater, but its range isn't great.

# Use Zigbee Groups for unresponsive lighting

* If you have a bunch of bulbs close to each other (like a light fixture), one or more devices might not respond to an ON/OFF command.
* Try creating a Zigbee group for any light fixtures or other groups of lights.
* Even if a devices shows as unavailable on your network, it usually will still repond to a group command.

# Set your Global Options with care

* I don't have enhanced light color enhanced brightness features enabled. They cause stability issues when enabled.
* I keep the mains and battery power timeouts high. Both of mine are set at 29000 seconds or about 8 hours. Some devices don't do network check-ins frequently.
* Having a high timeout keeps those devices available on your network.
