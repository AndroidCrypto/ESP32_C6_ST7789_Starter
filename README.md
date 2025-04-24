# ESP32 C6 ST7789 Starter
Getting started with an ESP32-C6 Supermini device and a TFT display ST7789.

This is the accompanying repository for my article "**Getting Started with an ESP32-C6 Supermini device connected to an ST7789 TFT display**".

My display is a 2.0 inch large TFT display with 240 x 320 pixels.

## Settings for the display specific setup file

I'm using a display specific setup file for the combination ESP32-C6 Supermini with TFT display driver ST7789. If your display has a different size please change the height and width accordingly:

**Setup703_C6_SM_ST7789_240x320.h**

You need to place the following line in the root folder's "**User_Setup_Select.h**" file

    #include <User_Setups/Setup703_C6_SM_ST7789_240x320.h> // ESP32-C6 Supermini, 80 MHz

## Important note

You need to modify the display library TFT_eSPI to get the code to work. Please find instructions on how to do this in my forked TFT_eSPI repository here on GitHub: [https://github.com/AndroidCrypto/TFT_eSPI](https://github.com/AndroidCrypto/TFT_eSPI).

