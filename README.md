# ESP32-C6 Supermini with ST7789 TFT display Starter
Getting started with an **ESP32-C6 Supermini** device and a TFT display with driver chip **ST7789**.

This is the accompanying repository for my article "**[Getting Started with an ESP32-C6 Supermini device connected to an ST7789 TFT display](https://medium.com/@androidcrypto/getting-started-with-an-esp32-c6-supermini-device-connected-to-an-st7789-tft-display-76b0809e292f)**": https://medium.com/@androidcrypto/getting-started-with-an-esp32-c6-supermini-device-connected-to-an-st7789-tft-display-76b0809e292f.

My display is a 2.0 inch large TFT display with 240 x 320 pixels.

## Settings for the display specific setup file

I'm using a display specific setup file for the combination ESP32-C6 Supermini with TFT display driver ST7789.This file contains e.g. the display driver, size and pins for the ESP32-device. If your display has a different size please change the height and width accordingly. 

### Copy a file to the User_Setups folder

Please copy the file

    Setup703_C6_SM_ST7789_240x320.h

to the **User_Setups** folder.

### Edit the User_Setup_Select.h file

You need to place the following line in the root folder's "**User_Setup_Select.h**" file

    #include <User_Setups/Setup703_C6_SM_ST7789_240x320.h> // ESP32-C6 Supermini, 80 MHz

Second: please comment all other "#include..." entries like this, especially the "//#include <User_Setup.h>" entry.

````
// Example User_Setup files are stored in the "User_Setups" folder. These can be used
// unmodified or adapted for a particular hardware configuration.
#ifndef USER_SETUP_LOADED //  Lets PlatformIO users define settings in
                          //  platformio.ini, see notes in "Tools" folder.
///////////////////////////////////////////////////////
//   User configuration selection lines are below    //
///////////////////////////////////////////////////////
// Only ONE line below should be uncommented to define your setup.  Add extra lines and files as needed.
//#include <User_Setup.h>                       // Default setup is root library folder
// Setup file in folder Arduino/libraries (updates will not overwrite your setups)
#include <User_Setups/Setup703_C6_SM_ST7789_240x320.h> // ESP32-C6 Super Mini, 80 MHz
````

## GPIO pins setup in the display specific setup file

The **regular setup file** has these pin settings:

```` plaintext
// file Setup703_C6_SM_ST7789_240x320.h
//#define TFT_BL  18  // LED back-light
#define TFT_MISO   3  // not used/connected
#define TFT_MOSI   4  // = SDA
#define TFT_SCLK   2  
#define TFT_CS     5 
#define TFT_DC     1
#define TFT_RST    0  // Set TFT_RST to -1 if display RESET is connected to ESP32 board EN
````
As mentioned in the tutorial, the display pins are now using most of the **Analog Digital Converter (ADC) pins** (0..6). If you need them e.g. for Battery Management or other measurements you can use an **alternative pin** set that does not use any of the 7 ADC channels:

```` plaintext
// file Setup703_C6_SM_ST7789_240x320_Alternative.h
//#define TFT_BL  18  // LED back-light
#define TFT_MISO  23  // not used/connected. Pin 23 is on solder pads only
#define TFT_MOSI  16  // = SDA
#define TFT_SCLK   7  
#define TFT_CS    14 
#define TFT_DC    19
#define TFT_RST   20  // Set TFT_RST to -1 if display RESET is connected to ESP32 board EN
````

    #include <User_Setups/Setup703_C6_SM_ST7789_240x320_Alternative.h> // ESP32-C6 Supermini, 27 MHz

Please note: when using the alternative Pin settings you have to **reduce the SPI speed from 80 MHz to 27 MHz**:

    #define SPI_FREQUENCY        27000000

## Important note

You need to modify the display library TFT_eSPI to get the code to work. Please find instructions on how to do this in my forked TFT_eSPI repository here on GitHub: [https://github.com/AndroidCrypto/TFT_eSPI](https://github.com/AndroidCrypto/TFT_eSPI).
