---
title: "spark!2350"
author: "Hudson / pythonatsea"
description: "Describe your project in a short sentence!"
created_at: "2024-07-18"
---

# spark!2350

## 7/18/25, 3 hours

### Basic idea

Basically I'm making a rp2350 based MCU designed fo keyboards, with a intergrated LiPo charger and a RPI RM2 for BLE. I'm also planning to have a intergrated rgb led, and maybe a OLED screen.

### Charger circuit.

I'm using the [MCP73871](https://www.microchip.com/en-us/product/MCP73871) to both charge the battery and switch between USB nd battery power. It uses a resistor pulldown to the PROG1 pin to set the charge current, which allows for some cool stuff. Using a little bit of math, I was able to calculate resistor values such that if you connect a solder jumper, the charge current changes from 100mA to 400mA. (this was inspired by the nice!nano v2's thing, which does the exact same thing!)
