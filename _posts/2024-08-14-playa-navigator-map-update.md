---
layout: post
title: "Playa Navigator Map Update"
author: "Zack Shivers"
tags: [projects,embedded,burningman,gps,design,3dprinting]
image: playa-navigator-map-update/title.png
hidden: true
---

# Map Update
Every year, Burning Man's map changes slightly. For your Playa Navigator to work for 2024, you need to update the map.

# Instructions
1. Download the <a href="assets/files/playa-navigator-map-update/map_config.json" download>2024 map</a>.

1. Connect the Playa Navigator to your computer with a USB cable.

1. After some time, a new USB drive will come up called **NO NAME**.
[![](assets/img/playa-navigator-map-update/no-name-usb-drive.png)](assets/img/playa-navigator-map-update/no-name-usb-drive.png)

1. Copy the `map_config.json` file you downloaded to **NO NAME**. Easiest way is to drag and drop directly. When asked about the duplicate file, click **Replace**.
[![](assets/img/playa-navigator-map-update/drag-drop.gif)](assets/img/playa-navigator-map-update/drag-drop.gif)

1. Eject **NO NAME** drive. After you see the **NO NAME** drive disappears, unplug the Navigator from your computer.
[![](assets/img/playa-navigator-map-update/eject.png)](assets/img/playa-navigator-map-update/eject.png)
1. Reboot the Navigator. Press and hold the power button for 3 seconds to shut down. Press again to start.

1. **Important** - Confirm the Naviator has the updated map.

   1. Press and hold the first button on the left. It will bring up the **DIAGNOSTICS** screen.
  [![](assets/img/playa-navigator-map-update/left-button.jpg)](assets/img/playa-navigator-map-update/left-button.jpg)

   1. Press the same button several times until you get to the screen matching the image below. If it reads **Map:BM2024-USB**, you've upgraded successfully. If not, try these instructions again.
  [![](assets/img/playa-navigator-map-update/map-id.jpg)](assets/img/playa-navigator-map-update/map-id.jpg)

## Notes
- Some USB cables are cheap and only provide power (no data). These will not work for the update. Try a different USB cable if the drive isn't showing up on your computer. The original cable I gave you will work.
- On my Macbook, it took a while for the **NO NAME** drive to appear. Give it 1 minute before giving up.
