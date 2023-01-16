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

## Hardware - Control System

- LILYGO TTGO T-Relay - https://www.amazon.com/LILYGO-T-Relay-Wireless-Development-Control/dp/B09XWWYK4V/ref=sr_1_2?crid=1UW20B1XXXDN1&keywords=lilygo%2Brelay&qid=1673831677&sprefix=lilygo%2Brelay%2Caps%2C117&sr=8-2&th=1

- Enclosure - https://www.amazon.com/gp/product/B07S75TV3V/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1

- Breaker - https://www.amazon.com/gp/product/B09F5Z2ZX3/ref=ppx_yo_dt_b_asin_title_o00_s01?ie=UTF8&th=1

- Power Supply (110vac to 12vdc) - https://www.amazon.com/gp/product/B074DV7ZKS/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1

What it looks like:

![This is an image](https://github.com/dresslerc/esphome-circulation-pump-controller/blob/main/controlbox.png)

![This is an image](https://github.com/dresslerc/esphome-circulation-pump-controller/blob/main/controlboxcover.png)

## Hardware - Pump Valve

- Pump - KOLERFLO 115V Water Recirculating Pump - https://www.amazon.com/gp/product/B07F25CH5R/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1

- Digital Valve - Motorized Ball Valve - https://www.amazon.com/gp/product/B06X99PHJJ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1

## Control Logic

### Pump
The pump runs with 110v.  Simply give it voltage and the pump runs.  We simply use 1 relay of the relay board to turn the pump on/off.

### Valve
The Valve opens with 12v.  If you flip the polarity of the wires, then the valve closes.  It takes about 5 seconds to open/close at 12v.  We use 2 relays of the relay board to control the valve.
