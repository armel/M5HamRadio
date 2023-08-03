# M5HamRadio
![basic](https://img.shields.io/badge/M5Stack-BASIC-blue)
![grey](https://img.shields.io/badge/M5Stack-GREY-blue)
![fire](https://img.shields.io/badge/M5Stack-FIRE-orange)
![core2](https://img.shields.io/badge/M5Stack-CORE2-green)
![aws](https://img.shields.io/badge/M5Stack-AWS-orange)
![coreS3](https://img.shields.io/badge/M5Stack-CORES3-lightgrey)

**First of all, many thanks to all my [donors](#donations)🙏🏻** 

The M5HamRadio project is a compilation, in one huge firmware, of my stable HamRadio projects on M5Stack. It include 4 applications :

- ICSMeter (default application)
- ICMultiMeter
- ICKeyer
- DXTracker

All these applications work on IC-705, IC-7300 and IC-9700 and are available for FREE and for ALL !

**Big (r)evolution, you don't have to install the whole compilation chain, VSCode & Plateform.io. You don't need to be a developer or a command line expert anymore. I tried to make it as simple as possible.**


|![ICSMeter](https://github.com/armel/M5HamRadio/blob/main/img/ICSMeter.png)|
|:--:|
| ICSMeter |

|![ICMultiMeter](https://github.com/armel/M5HamRadio/blob/main/img/ICMultiMeter.png)|
|:--:|
| ICMultiMeter |

|![ICKeyer](https://github.com/armel/M5HamRadio/blob/main/img/ICKeyer.png)|
|:--:|
| ICKeyer |

|![DXTracker](https://github.com/armel/M5HamRadio/blob/main/img/DXTracker.png)|
|:--:|
| DXTracker |

# Add more firmwares

Even if you already have 4 firmwares (ICSMeter, ICMultiMeter ICKeyer and DXTracker) after flashing your M5Stack via M5Burner, you can add other firmwares to the root of the micro SD card. 

> **Important ! Important ! Important !** Because applications now use LittleFS and not SPIFFS, if you have old firmwares based on SPIFFS, consider replacing it with the latest versions using LittleFS. If you don't, after loading an old firmware using SPIFFS, it will reformat your flash memory and overwrite any firmware you already have. So, be aware.

# Installation

## Warning about M5Stack CoreS3 support

Support for the M5Stack Core S3 is still experimental. By the way, the M5Stack Core S3 only supports Bluetooth 5.0 (BLE - Bluetooth Low Energy), but not anymore Bluetooth 4.2 (Classic).
Therefore, classical Bluetooth serial connexion won't work on the M5Stack Core S3. So, you will need to use [ICUSBProxy](https://github.com/armel/ICUSBProxy). **So, if you plan to use the Bluetooth connection, get an M5Stack Core or Core2 instead !**

## Prerequisites

You need an M5Stack (with 16MB Flash Memory), a micro SD card and a PC under Windows, Linux or MacOS, with the USB drivers installed and the M5Burner application version 3.0.0 (or higher).

There is a nice [video](https://www.youtube.com/watch?v=8zPQypwEP4w&ab_channel=K6UDA), made by Bob K6UDA, about my projects. I encourage you to watch it. It may help you understand how to set up your M5Stack with my HamRadio project. Thanks a lot Bob.

|![K6UDA video](https://github.com/armel/M5HamRadio/blob/main/img/K6UDA.jpg)|
|:--:|
| [Bob's K6UDA video on his Youtube channel](https://www.youtube.com/watch?v=8zPQypwEP4w&ab_channel=K6UDA) |


## Micro SD card

Prepare and format a micro SD card in FAT32. This micro SD card will be used to put your configuration files and to place other firmwares.

## USB drivers installation

Please go to [download page](https://docs.m5stack.com/en/download) to download the USB driver that matches your operating system, and install it.

> Note: Core2 currently has two CP2104/CH9102F A USB chip version, users can install the drivers (CH9102 and CP210x) that are compatible with two ICs at the same time to ensure that the device drivers work normally.

## M5Burner installation

Please go to [download page](https://docs.m5stack.com/en/download) to download the M5Burner (version 3.0.0 or higher) that matches your operating system, and install it.

## Firmware flash

Connect your M5Stack to your PC.

Launch the M5Burner application and select the M5HamRadio firmware for your M5Stack model. Be aware, there is a version for M5Stack Core (Basic, Grey, Fire, etc.) with buttons, a version for M5Stack Core2 (Core2, AWS, etc.) with touch screen and an **experimental** version for M5Stack CoreS3. 

Click on the blue Download button. Then click on the red Burn button.

|![M5Burner](https://github.com/armel/M5HamRadio/blob/main/img/M5Burner.png)|
|:--:|
| M5Burner |

## About special TX settings

### Bluetooth usage via [CI-V to Bluetooth Adapter Converter](https://www.aliexpress.com/item/1005003015867623.html)

First of all, plug in DIN cable (for Bluetooth adapter power supply) and Jack cable (for CI-V commands). Finally, check this settings on your IC-7300 or IC-9700 :


```
Menu > Set > Connectors > CI-V > CI-V Baude Rate > 9600
Menu > Set > Connectors > CI-V > CI-V Transceive > OFF
```

> Please note that the DIN output of the IC-9700 (8-pin) is not the same as the DIN output of the IC-7300 (13-pin) ! The Bluetooth adapter I pointed on AliExpress and am using all day is **ready for use on the IC-7300**. But you'll need to adapt the pinout to use it on the IC-9700. So please, consult your manual. 

### USB usage via [ICUSBProxy](https://github.com/armel/ICUSBProxy))

Please, check this settings on your IC-7300 or IC-9700 :

```
Menu > Set > Connectors > CI-V > CI-V USB Port       Unlink from [REMOTE]
Menu > Set > Connectors > CI-V > CI-V USB Baud Rate  115200
Menu > Set > Connectors > CI-V > CI-V USB Echo Back  OFF
```

Please, check this settings on your IC-705 :

```
Menu > Set > Connectors > CI-V > CI-V USB Echo Back  OFF
```


## ICSMeter, ICMultiMeter and ICKeyer .ini file settings

Using a plain text editor, you will create a file that should have the `.ini` extension. 

> I insist, you must use a simple plain text editor. Do not save your `.ini` file in DOC or RTF format. Last, but not least, note that the `.ini` file contend is case-sensitive. 

Name it, for example `IC705BT.ini` if you plan to use an IC-705, connected by Bluetooth. 

And now, here is what you will put in this `IC705BT.ini`. Of course, **take the time to adapt the values to your use** :

```
; Icom Config
[icom]
icom_model = 705
icom_address = 0xA4
icom_connect = BT
icom_device = 30:31:7D:33:B2:58

; Wifi Config
[wifi]
wifi_ssid = YOUR_SSID
wifi_password = YOUR_PASSWORD

; Proxy Config
[proxy]
baud_rate = 115200
proxy_url = http://192.168.1.32
proxy_port = 1234

; Transverter Config
[transverter]
transverter_lo_1 = 116000000
transverter_lo_2 = 118000000
transverter_lo_3 = 404000000
transverter_lo_4 = 406000000
transverter_lo_5 = 9968000000

; Geolocation Config
[geolocation]
latitude = 48.848285
longitude = 2.2708201
```

> About Icom Config section, here are some explanations. About `icom_model` choose between 705, 7300 or 9700. About `icom_address`, this is your Icom CI-V Address. About `icom_connect` choose between BT or USB (if you choose USB, you will need [ICUSBProxy](https://github.com/armel/ICUSBProxy)). Last, about `icom_device`, 

> * If you're using an IC-705, this is the BT Address of your IC-705. From your transceiver, enter Menu and go to Set > Bluetooth Set > Bluetooth Device Information. Mine is `30:31:7D:33:B2:58`.
> 
> * If you're using an IC-7300 or a IC-9700 with a [CI-V to Bluetooth Adapter Converter](https://www.aliexpress.com/item/1005003015867623.html), this is the Adapter Bluetooth name. Use your Smartphone or your PC to find it by proximity detection. Mine is `FBT06`.


> Note that, Proxy Config section is ONLY useful if you linked your M5Stack to your Transceiver via USB using [ICUSBProxy](https://github.com/armel/ICUSBProxy). If you are using Bluetooth, you do not need to change this section of settings. So leave values as they are, by default. The same goes for the Geolocation Config section which is ONLY useful for DXTracker. But if you fill in this section (and the Wifi Config section) correctly, this `.ini` file will also work for the DXTracker too.

Please, again, **take the time to adapt the values to your use**. It's important !

Here is an another example, if you plan to use an IC-7300, connected by Bluetooth (need to use a [CI-V to Bluetooth Adapter Converter](https://www.aliexpress.com/item/1005003015867623.html)) with this `IC7300BT.ini` :

```
; Icom Config
[icom]
icom_model = 7300
icom_address = 0x94
icom_connect = BT
icom_device = FBT06

; Wifi Config
[wifi]
wifi_ssid = F1ZPX
wifi_password = petitchaton

; Proxy Config
[proxy]
baud_rate = 115200
proxy_url = http://192.168.1.32
proxy_port = 1234

; Transverter Config
[transverter]
transverter_lo_1 = 116000000
transverter_lo_2 = 118000000
transverter_lo_3 = 404000000
transverter_lo_4 = 406000000
transverter_lo_5 = 9968000000

; Geolocation Config
[geolocation]
latitude = 48.848285
longitude = 2.2708201
```

Finaly here is an another example, if you're using an IC-9700, connected by USB (need to use [ICUSBProxy](https://github.com/armel/ICUSBProxy)) with this `IC9700USB.ini` :

```
; Icom Config
[icom]
icom_model = 9700
icom_address = 0xA2
icom_connect = USB
icom_device = /dev/ttyUSB0

; Wifi Config
[wifi]
wifi_ssid = YOUR_SSID
wifi_password = YOUR_PASSWORD

; Proxy Config
[proxy]
baud_rate = 115200
proxy_url = http://192.168.1.32
proxy_port = 1234

; Transverter Config
[transverter]
transverter_lo_1 = 116000000
transverter_lo_2 = 118000000
transverter_lo_3 = 404000000
transverter_lo_4 = 406000000
transverter_lo_5 = 9968000000

; Geolocation Config
[geolocation]
latitude = 48.848285
longitude = 2.2708201
```

Last, you will need to copy these files at the root of the micro SD card. That's all.

> You are able to put multiple .ini settings files for all your transceivers. I have got 4 of them for my IC-705 and my IC-7300 in BT mode or USB mode. I put them in this repository in the `ini` folder. 

## DXTracker .ini file settings

Using a plain text editor, you will create a file that should have the `.ini` extension. For example `DXTracker.ini`. 

And now, here is what you will put in this `DXTracker.ini` :

```
; Wifi Config
[wifi]
wifi_ssid = YOUR_SSID
wifi_password = YOUR_PASSWORD

; Geolocation Config
[geolocation]
latitude = 48.848285
longitude = 2.2708201

```

> About Geolocation Config, you need to use decimal coordinates (with a dot as decimal separator). Here are some examples :
>
> Paris (France)\
> latitude = 48.866667\
> longitude = 2.333333
>
> Syndney (Australia)\
> latitude = -33.865143\
> longitude = 151.209900
>
> Los Angeles (USA)\
> latitude = 34.003342\
> longitude = -118.485832

> If these two sections Wifi Config and Geolocation Config are correctly settings in one of your others `.ini` files for ICSMeter, ICMultiMeter or ICKeyer, this will work too.

# Usage

Ready to go? Your M5Stack has been flashed with M5Burner? Your micro SD card has been formatted and you have saved your modified `.ini` files with your settings? Good. So let's go.

> Important. On M5Stack Core2, the 3 small red circles on the front bottom of the screen are capacitive buttons. Each of these buttons correspond to the left, middle and right physical buttons of the M5Stack Core.

|![Buttons](https://github.com/armel/M5HamRadio/blob/main/img/ButtonsCore2.png)|
|:--:|
| Capacitive buttons on M5Stack Core2 |

> Important. On M5Stack CoreS3, the front bottom of the screen is **not anymore** capacitive. So you need to touch the bottom left, bottom center and bottom right of the M5Stack CoreS3 screen (directly on the display area) to emulate the left, middle and right physical buttons of the M5Stack Core.

|![Buttons](https://github.com/armel/M5HamRadio/blob/main/img/ButtonsCoreS3.png)|
|:--:|
| Capacitive buttons on M5Stack CoreS3 |

## Bin Loader

By default, M5Stack will start on ICSMeter firmware. At startup, you'll see the Bin Loader with a green gauge. You have 3 seconds to use the bottom middle button to select another firmware. Pressing the left or right button will bypass this step. 

## Ini Loader

If the micro SD card is correctly inserted in your M5Stack, you'll now see the Ini Loader with a blue gauge. You have 3 seconds to use the bottom middle button to select an `.ini` file that you put on it. Select the `.ini` file you would like to load and... enjoy.

> When you select an .ini file with the Ini Loader (and if it is valid), a copy is made on the Flash memory of the M5Stack. And if at the next reboot you do not make any action / selection of .ini file with the Ini Loader, it is this last valid `.ini` file, in Flash memory, that will be read automatically. This way, you can remove the SD card from your M5Stack, if you wish.

> So, if you change something in your .ini file (for example, the Wifi password, etc.), **you must restart your M5Stack and select it again from the Ini Loader to force reload this new version**. A new copy will then be made in the M5Stack Flash memory. And it will be this new version that will be read at the next reboot (if no action / selection with the Ini Loader).

# About micro SD card issues

Regarding the micro SD card, if you are experiencing issues, please ensure that it is properly inserted into your M5Stack. Remember to format it as FAT32. If necessary, clean the contacts on the micro SD card with the purest possible alcohol (in order of purity: 99.9% isopropyl alcohol, 90% alcohol, 70% alcohol). Be sure to wait until the micro SD card is completely dry before reinserting it into your M5Stack. Last but not least try another one micro SD Card, if necessary. From experience, the quality of micro SD cards can vary from one brand to another.

# Improvements

Remember that all applications in the M5HamRadio project are full compatible with the [M5Stack Display module 13.2](https://shop.m5stack.com/collections/m5-modules/products/display-module-13-2?ref=LUxetaH4) ! So it's possible to display the screen output, via an HDMI cable, on a large PC screen or TV.

# Help me to debug your problem

Do you have a problem? Okay, don't panic. 

Connect your M5Stack to your PC.

Launch the M5Burner application and select the Serial Monitor menu option.

|![Step 1](https://github.com/armel/M5HamRadio/blob/main/img/Debug_01.png)|
|:--:|
| Step 1 |

Select the COM port to which your M5Stack is connected and click on Connect.

|![Step 2](https://github.com/armel/M5HamRadio/blob/main/img/Debug_02.png)|
|:--:|
| Step 2 |

Restart your M5Stack, copy the log trace that appears in the console and send it to me. It may be useful to understand your problem.

|![Step 3](https://github.com/armel/M5HamRadio/blob/main/img/Debug_03.png)|
|:--:|
| Step 3 |

# Power users only (esptool and CLI)

## Backup full image : *read_flash*

Using ``esptool``, enter this command:

``esptool.py --port /dev/tty.usbserial-02041F5C --baud 230400 read_flash 0x00000 0x1000000 flash_16M.bin``

Replace port and baud rate by yours.

## Restore full image : *write_flash*

Using ``esptool``, enter this command:

``esptool.py --port /dev/tty.usbserial-02041F5C --baud 921600 write_flash --flash_freq keep 0x000000 flash_16M.bin``

Replace port and baud rate by yours.

## GZipped a firmware

Using ``gzip``, enter this command:

``gzip -c firmware.bin > firmware.gz``

That's all. The size is reduced by about 30%.

# Disclaimers 

Because of the systematic plundering of my open source projects by a minority of unscrupulous people, taking advantage of my work to make money, I decided not to open the source code of these projects, for the moment.

I was insulted, threatened and blacklisted by these same people (resellers, youtubers, etc.). Some of them think they are little judges. And even if I know that the majority is behind me, that's enough 😔 

I believe in Open Source. But I believe too that a small part of the HamRadio community and some resellers are not yet mature enough to understand Open Source.

This being the case, I will make theses firmwares available for FREE and for ALL, but... 

These firmware is copyright (c) 2022 Armel FAUVEAU, that is to say me F4HWN and covered by the Berne Convention.

THESE FIRMWARES ARE NOT ALLOWED TO BE SOLD, IN ANY WAY. 

THESE FIRMWARES ARE PROVIDED "AS THEY ARE", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. 

IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THESE FIRMWARES OR THE USE OR OTHER DEALINGS IN THESE FIRMWARES.

# Credits
 
Many thanks to...

| Project             | Author                                                |  Link                                        |
|:------------------- | :---------------------------------------------------- | :------------------------------------------- |
| M5Stack             | [M5Stack](https://twitter.com/M5Stack)                | https://github.com/m5stack/M5Stack           |
| M5Stack-SD-Updater  | [Tobozo](https://twitter.com/TobozoTagada)            | https://github.com/tobozo/M5Stack-SD-Updater |
| FastLED             | FastLED                                               | https://github.com/FastLED/FastLED           |
| HamQSL              | Paul L Herrman N0NBH				                  | https://www.hamqsl.com/solar.html 			 |

Icom and the Icom logo are registered trademarks of Icom Incorporated (Japan) in Japan, the United States, the United Kingdom, Germany, France, Spain, Russia, Australia, New Zealand, and/or other countries.


# Donations

Special thanks to Rolf Schroeder DL8BAG, Brian Garber WB8AM, Matt B-Wilkinson M6VWM, Robert Agnew KD0TVP, Meinhard Frank Günther DL0CN, Johan Hansson SM0TSC, Tadeusz Pater VA7CPM, Frederic Ulmer F4ESO, Joshua Murray M0JMO, Mark Hammond N8MH, Angel Mateu Muzzio EA4GIG (2 times 🍷🍷), Hiroshi Sasaki JL7KGW, Robert John Williams VK3IE, Mark Bumstead M0IAX, Félix Symann F1VEO, Patrick Ruhl DG2YRP, Michael Beck DH5DAX, Philippe Nicolas F4IQP, Timothy Nustad KD9KHZ, Martin Blanz DL9SAD, Edmund Thompson AE4TQ, Gregory Kiyoi KN6RUQ, Patrick Samson F6GWE, George Kokolakis SV3QUP, Ambrose "Bo" Barry W4GHV, Roger Bouche F1HCN, Christopher Platt, Pascal Paquet F4ICR, Gregory Kiyoi, Ning Yang BH7JAG, Mitsuhiko Nagasawa JL1LYT, Mike Mann G4GOC, David Cappello, Matt Brinkhoff KB0RXC, Franklin Beider WD9GZ, Robrecht Laurens ON4ROB, Florian Wolters DF2ET, James Gatwood WA9JG and Christoph Gässler DL6SEZ for their donations. That’s so kind of them. Thanks so much 🙏🏻

If you find this project fun and useful then [buy me a glass of wine](https://www.paypal.me/F4HWN) 🍷 🤗 

~~You could use the code F4HWN in order to get 5% discount on the [M5Stack shop](https://shop.m5stack.com/?ref=LUxetaH4) 🎁~~

By the way, you can follow me on [Twitter](https://twitter.com/F4HWN) and post pictures of your installation with your M5Stack. It always makes me happy ;) 
