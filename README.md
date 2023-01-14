# ESPHome based Circulation Pump Controller

This project describes how to build a Circulation Pump Controller using ESPHome and thats controlled from Home Assistant.  For me, I use it to control a hot water circulation pump and valve that I installed near my water heater in the garage.

## What is a Hot Water Circulation Pump:

A hot water circulation pump is a device used in plumbing systems to circulate hot water from a water heater to the various fixtures and appliances in a building. This can include things like sinks, showers, and bathtubs. The pump is typically installed in the hot water line, and its purpose is to ensure that hot water is readily available to all fixtures and appliances, without the need to wait for the water to be heated. This can save energy and reduce the wait time for hot water. This system uses a ESP32 with ESPHome and Home Assistant to control when the pump is active, further increasing energy efficiency.


## Plumbing
![This is an image](https://github.com/dresslerc/esphome-circulation-pump-controller/blob/main/circpump.png)

The yellow line is an extra return loop that I installed.  I ran it from the farthest bathroom, through the attic back to the water heater.  Without this return loop, it would take my shower about 5 minutes to get hot.  Now with pump, when I turn my shower on, it takes about 10 seconds.

## Control
Obviously, in this case, it doesnt make since to run the pump 24/7.  It really only benfits when I needed hot water in the masterbath room.  Too compensate for this I wanted to control/schedule this system through Home Assistant:

![This is an image](https://github.com/dresslerc/esphome-circulation-pump-controller/blob/main/ha_pump.png)

Currently when the system is on, it runs for 3 minutes, every 18 minutes.  This logic is done in ESPHome on a ESP32.  

## Features
- Turn on/off from Home Assistant (this also includes scheduling it)
- Run once - ability to run the pump once.
- Motion Controlled - I placed a motion sensor (z-wave) in my bathroom, when motion is triggered and the pump hasnt run in 15 minutes, it'll run again (but only if motion triggered)
- Motion Controlled Once - When the motion sensor detects motion, run the pump once, and turn off Motion Controlled Once.
- Freeze Protection - Since the return line runs through the attic.  I wanted to ensure if its cold outside, it runs the pump every 15 minutes.

