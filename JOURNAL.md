---
title: "spark!2350"
author: "Hudson / pythonatsea"
description: "nice!nano but RP2350"
created_at: "2024-07-18"
---

# spark!2350

## 7/18/25, 3 hours

### Basic idea

Basically I'm making a rp2350 based MCU designed fo keyboards, with a intergrated LiPo charger and a RPI RM2 for BLE. I'm also planning to have a intergrated rgb led, and maybe a OLED screen.

### Charger circuit.

I'm using the [MCP73871](https://www.microchip.com/en-us/product/MCP73871) to both charge the battery and switch between USB nd battery power. It uses a resistor pulldown to the PROG1 pin to set the charge current, which allows for some cool stuff. Using a little bit of math, I was able to calculate resistor values such that if you connect a solder jumper, the charge current changes from 100mA to 400mA. (this was inspired by the nice!nano v2's thing, which does the exact same thing!)

<img width="1573" height="1054" alt="image" src="https://github.com/user-attachments/assets/d897e4da-35e3-43e2-871e-34118503cecb" />

## 7/21/25, 5 hours

### Power supply

Since I'm using a battery charger, the voltage regulator can receive 3.7-4.2v (from the battery) or it can get the 5v passed through from the usb port. This means it has to have >300mA of dropoff, which means the one recommended by the rp2350 design guide won't actually work, since it has ~1v of dropoff. I was able to find the MCP1700, which has ~250mA of dropoff, which works perfectly!

<img width="1447" height="626" alt="image" src="https://github.com/user-attachments/assets/53f3b8e5-b647-4b91-9a00-168e849e7c3b" />

### Flash

I'm using the W25Q128JVS flash, which is the recommended module from the design guide. It has 128 mbits of storage, the max allowable, and it's also a basic part on JLC!

### Crystal

Again, I'm just going with the recommended module, but here it's more important than the flash, as the crystal has to be very precise for stuff like USB to work.

<img width="821" height="881" alt="image" src="https://github.com/user-attachments/assets/e55b1239-b6c8-4a53-a100-91d33f860e61" />

## 7/27/25, 4 hours

### Pinout

I made the pinout for the left and right pinheaders, it has the USB data pins broken out so that the user can have their own USB port if they desire.

<img width="576" height="4256" alt="image" src="https://github.com/user-attachments/assets/67eb3e5c-05c3-4da0-8c00-04d9ef1ee7d1" />

### NeoPixel

I put a neopixel on `GPIO0`, with a jumper that can be cut so the pin can be used for other things.

<img width="1358" height="760" alt="image" src="https://github.com/user-attachments/assets/0826a53f-ee6f-497b-93b6-9420d694aa43" />

### Schematic (mostly) done!

The schematic is done, now I need to find footprints and make the actual PCB!!
