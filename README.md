# Herring54 Split Keyboard Firmware

FreeRTOS-based firmware for the [Silakka54 keyboard.](https://squalius-cephalus.github.io/silakka54/)

Would probably work on other RP2040 split keyboards if anyone cared.

Very much in development and quite opinionated, just a hobby project.

## Features
- Multi-layer (I should hope so...)
- WS2818 state LEDs (one on either MCU*)
- SSD1306 OLED display
- USB-connected side agnostic**

\* - On the official Silakka54, the right-hand keyboard has the RP2040-Zero mounted upside-down,
so you can't see the WS2818. However, the Aliexpress SMD variants mount both controllers the right way up. Herring54 just runs the LEDs on both for now.

\** - I.e., you can plug the USB cable into either board and it'll configure the peer board.

## Setup
