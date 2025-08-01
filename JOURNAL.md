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

<img alt="image" src="https://github.com/user-attachments/assets/67eb3e5c-05c3-4da0-8c00-04d9ef1ee7d1" />

### NeoPixel

I put a neopixel on `GPIO0`, with a jumper that can be cut so the pin can be used for other things.

<img width="1358" height="760" alt="image" src="https://github.com/user-attachments/assets/0826a53f-ee6f-497b-93b6-9420d694aa43" />

### Schematic (mostly) done!

The schematic is done, now I need to find footprints and make the actual PCB!!

## 7/29/25, 4 hours

### Footprints (sigh)

I had to find a bunch of different footprints, including the RP2350, the inductor, and the crystal. I also had to make a castellated hole footprint, which worked quite well. 

<img width="1790" height="953" alt="image" src="https://github.com/user-attachments/assets/6110abac-9215-4801-af4d-8fc4d6e1d8e1" />

### General layout

The two castellated headers are positioned so they have 25mm between them. The antenna of the RM2 hangs of the bottom of the PCB so that there's no copper in the RF keepout.

<img width="556" height="1098" alt="image" src="https://github.com/user-attachments/assets/ebe636ee-f3ce-488f-9e06-cabe02c56cec" />

## 7/31/25, 8 hours (oh boy i locked in)

### Parts

I'm trying to use as many basic/preferred extended parts as possible to keep costs low. For example, I'm using relativly large 0805 LEDs for the charging indicators because they're basic parts.

### Routing

Imma be honest, there was a lot of wacky nonsense that took a while to fix but I don't really remeber specifics. Actually I did switch USBC posrt because routing would've been close to immpossible with the other one because of the two d+ and d- pins being on opposite sides. 

<img width="848" height="704" alt="image" src="https://github.com/user-attachments/assets/a4f771e6-26e1-4c2f-8777-f0e03df9167b" />

### Finished!

It's finally done! I'm pretty happy with hor it turned out, if I had to make a v2 I'd probably try to make it smaller.

<img width="658" height="914" alt="image" src="https://github.com/user-attachments/assets/5f0b79fb-1c53-4021-a019-7d78e75d1043" />
