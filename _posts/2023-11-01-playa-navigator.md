---
layout: post
title: "Playa Navigator"
author: "Zack Shivers"
tags: [projects,embedded,burningman,gps,design]
image: playa-navigator-location.jpg
---

# Navigating at Burning Man
It can be hard to get around at [Burning Man](https://burningman.org). Despite the clock-like road layout and posted [road signs](https://www.google.com/search?q=burning+man+road+signs&tbm=isch), it is easy to get confused.

- Places you may want to revisit may not be within the city blocks. For example, it is easy to get find A & 7:00 again, but how about that cool art you saw in deep playa?
- The road signs are ritually removed near the end of the week.
- Landmarks and tall objects change, especially near the end of the week.
- There are blue light markers for portos, but they can be hard to see among the huge visual noise of Burning Man.
- The nearest porto in the middle of deep playa may be far or not be easy to find.

You could just use your phone, download offline maps, and follow the little blue dot. You could even make a custom app that does everything my device does. But what's the fun in that? Let's make bespoke hardware!

You can find the complete design files (for the hardware and firmware) in my [Github repo](https://github.com/zshivers/PlayaNavigator).

# Design

## Functionality
The device should be simple, and only provide these functions:
1. Show you where you are right now.
2. Navigate to somewhere you've been before.
3. Navigate to a porto.

## Design Goals
- Simple and direct interface. No complex menu systems.
- Useful for both biking and walking.
- Week-long battery life - recharge as few times as possible during the burn.
- Low total cost for building about 20 units.

# User Interface

## Location
![Playa navigator device showing the location screen](assets/img/playa-navigator-location-front.jpg)
Display the current location in a useful format.

There are two address formats, which depend on where you are:
1. Inside city blocks: `HH:MM / Road` - e.g. `05:50 / 1.2 mi`
2. Everywhere else: `HH:MM / Distance` - e.g. `05:50 / S`

The distance units automatically adjust: 0 to 9999 feet, then in miles.

## Waypoint Naviation
[![](assets/img/playa-navigator-waypoint.jpg)](assets/img/playa-navigator-waypoint.jpg)
  - Show the distance and bearing to a waypoint stored in non-voltaile memory.
  - Single press to cycle through 5 possible waypoints.
  - Press and hold to store the current location to the waypoint.

## Bathroom Navigation
[![](assets/img/playa-navigator-bathroom.jpg)](assets/img/playa-navigator-bathroom.jpg)
Show the distance and bearing to the nearest porto.

## Brightness & Power
- Single press to cycle through 4 different brightness levels.
- Press and hold to turn on or off.

# GPS Data
The Burning Man org website started publishing [map data](https://innovate.burningman.org/dataset/2023-gis-map-data/) about the playa. It has become especially detailed starting in 2023. The published data includes KMZ and GeoJSON files defining a map of the roads, promenades, portos, city outline, etc. 

For this project, the Navigator device must know:
- City center location
- Radial distance from center to each road
- Location of each porto

Comparison image between city map and representation used by navigator.

# Hardware
TODO Links to schematic and layout.

## Display
The display's main constraints were sunlight readability and graphic capability. [Transflective](https://en.wikipedia.org/wiki/Transflective_liquid-crystal_display) graphic LCDs are very legible in sunlight, and have low power requirements.

[![](assets/img/playa-navigator-sunlight.jpg)](playa-navigator-sunlight.jpg)
_Transflective LCD showing excellent readability in full sunlight_

[Pico GFX Pack](https://shop.pimoroni.com/products/pico-gfx-pack)

## GNSS Receiver
Aliexpress has a great, no-frills, low-cost option for a [GNSS receiver](https://www.aliexpress.us/item/3256801517715702.html?gatewayAdapt=glo2usa) with a UART interface. It includes an antenna. Total per unit cost (including shipping from China) was $3.77 per unit for quantity 25. 🤯
[![](assets/img/ATGM336H.jpg)](assets/img/ATGM336H.jpg)
Surprisingly, I was able to find an working, English version of the [UI](https://github.com/zxcwhale/GnssToolKit3-binaries) used to configure the receiver. 

[![](assets/img/gnsstoolkit-screenshot.png)](assets/img/gnsstoolkit-screenshot.png)

I ended up just using the receivers without any customization. Thse controllers just work out of the box outputting plenty of info by default. I tweaked a few settings in an attempt to lower the power consumption, but I was not successful. 

## Microcontroller
I chose the [Raspberry Pi Pico](https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html), mostly because it allowed me to use the display breakout. However, RP2040s have an excellent price to performace ratio. Bought in quantity of 10s, they are only [about $4](https://shop.pimoroni.com/products/raspberry-pi-pico). The Pico has dual ARM Cortext M0 cores, 264kB of SRAM, and 2MB of on-board flash memory, and native USB.

## Battery and Charger
Battery life was important to this project, because remembering to charge a device out on the playa is definitely not top priority. I did not doing anything particularly sophisticated to select the battery - I found a lipo from Adafruit that roughly matched the dimensions of the LCD board and selected a capacity that maximized battery life.

Usage Time        | Backlight Setting   | Estimated Life      |
----------------- | ------------------- | ------------------- |
1 hour / day      | | |

I used the ubiquitious MCP73832 single-cell lipo charging IC. 

## Bike Mount


## 3D Modeling

## Cost Breakdown

# Firmware
## LVGL for Graphics
[LVGL](https://lvgl.io) is an impressive C graphics library designed for embedded applications. I chose it because I wanted to try it, and it is possible to run the same code for the host machine. The ability to emulate on the host is a huge timesaver when making small tweaks.

## Lowering the Power Consumption
I reduced the opearting power consumption using these techniques, ordered from most savings to least:
- Automatic shutdown (lowers overall power consumption in use rather than instaneous power).
- (-100mW) Reduce CPU clock frequency to 48 MHz.
- (-1mW) Disable Pico board debug LED.

I was somewhat surprised to find the largest determination of battery life is the LCD backlight.

## USB Configuration File
These devices took too long to manufacture to just toss them after one year. Since the map changes each year, I added the ability to reconfigure them with a JSON file via USB mass-storage device.



# Testing
Doing major firmware upgrades or debugging at Burning Man was _not an option_. I invested time in unit testing and interactive testing. The unit tests cover the most critical parts of the code (coordinate conversions, playa address formatting).

## Harware checkout test
I built about 20 of these devices, so a quick hardware go/no-go test was a time saver to detect issues early.

[![](assets/img/playa-navigator-charging.jpg)](assets/img/playa-navigator-charging.jpg)


With minimal user input, the a special firmware can check these hardware elements:

- Backlight: cycle through R, G, B, W every 1 sec.
- Display: Show a repeating pixel pattern that moves.
- Buttons: Print button press state.
- Battery: Print charging state.
- GPS: Print total of incoming bytes from GPS UART.

IMO, it is important to keep the firmware for this check as basic as possible. It is useful to keep this check independent of the main firmware, ensuring I have a basic check to fall back to if an unexpected bug pops up.

## Running on Host
Running firmware on the host speeds up development. LVGL works on host machines through the cross-platform [libSDL](https://www.libsdl.org/). 

## Interactive Testing in the Broswer
Interactive tests can be a reasonable replacement for integration or unit tests that would otherwise be very sophisticated. I wanted to emulate being at any location on the playa, and checking that the display was showing the right address. It was perfect to test out if the bearing algorithm was giving the right directions to waypoints.

TODO gif of interactive testing

Making this test required:
- A map of the playa (from the BM provided data) in GeoJSON.
- A web app that can show a map of the playa, and send emulated GPS coordinates at a cursor to a websocket.
- Firmware running on the host that accepts GPS coordinates over a websocket.

I re-purposed [this code](https://github.com/openlayers/ol-vite) combining OpenLayers and Vite to make the webapp. I added a bit of code to import the map data, add a cursor, and send the coordinates.

To connect the firmware to the websocket, you could use a websocket library. But it was easier to use [websocat](https://github.com/vi/websocat) and then pipe the output into `stdin`.
```bash
websocat -s 9998 | ./.pio/build/host/program
```

The host version of the GPS driver then parses the coordinates in a separate thread:
```c++
static auto io_thread = std::thread([&] {
  std::string s;
  while (!error && std::getline(std::cin, s, '\n')) {
    double lat, lon;
    int n = sscanf(s.c_str(), "%lf,%lf", &lat, &lon);
    if (n == 2) {
      auto lock = std::unique_lock<std::mutex>(m);
      gps_info_.location.lat = lat;
      gps_info_.location.lon = lon;
      gps_info_.valid = true;
      lock.unlock();
    }
  }
  auto lock = std::unique_lock<std::mutex>(m);
  error = true;
  lock.unlock();
});
```