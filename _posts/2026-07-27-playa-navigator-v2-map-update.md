---
layout: post
title: "Playa Navigator V2 Map Update"
author: "Zack Shivers"
tags: [projects,embedded,burningman,gps]
image: playa-navigator-map-update/title.png
hidden: true
---

# Device Version
These instructions are for the **V2** Playa Navigator. If you have a **V1** device, please see [these instructions](playa-navigator-map-update) instead.

# Map Update

Every year, Burning Man's map changes slightly. For your Playa Navigator to work for 2026, you need to update the map.

# Instructions

1. Download the <a href="assets/files/playa-navigator-map-update-2026/map_config.json" download>2026 map</a>.

1. Connect the Playa Navigator to your computer with a USB-C cable.

   1. Remove the back cover and plug in your USB-C cable.
  [![](assets/img/playa-navigator-v2-map-update/usb-connection.jpg)](assets/img/playa-navigator-v2-map-update/usb-connection.jpg)

   1. Turn on the device by pressing the power button.

1. After some time, a new USB drive named **NO NAME** will appear.
[![](assets/img/playa-navigator-map-update/no-name-usb-drive.png)](assets/img/playa-navigator-map-update/no-name-usb-drive.png)

1. Copy the `map_config.json` file you downloaded to **NO NAME**. The easiest way is to drag and drop directly. When asked about the duplicate file, click **Replace**.
[![](assets/img/playa-navigator-map-update/drag-drop.gif)](assets/img/playa-navigator-map-update/drag-drop.gif)

1. Eject the **NO NAME** drive. Once it disappears, unplug the Navigator from your computer.
[![](assets/img/playa-navigator-map-update/eject.png)](assets/img/playa-navigator-map-update/eject.png)

1. Reboot the Navigator. Press the power button to shut down. Press again to start.

1. **Important** - Confirm the Navigator has the updated map.

   1. While on the **LOCATION** screen, press and hold the menu button (button on the right side). It will bring up the **DIAGNOSTICS** screen.
  [![](assets/img/playa-navigator-v2-map-update/menu-button.jpg)](assets/img/playa-navigator-v2-map-update/menu-button.jpg)

   1. Press the same button several times until you get to the screen matching the image below. If it reads **Map:BM2026-R1**, you've upgraded successfully. If not, try these instructions again.
  [![](assets/img/playa-navigator-v2-map-update/map-id.jpg)](assets/img/playa-navigator-v2-map-update/map-id.jpg)

## Notes

- Some USB cables are cheap and only provide power (no data). These will not work for the update. Try a different USB cable if the drive isn't showing up on your computer.
