# M5HamRadio
![basic](https://img.shields.io/badge/M5Stack-BASIC-blue)
![grey](https://img.shields.io/badge/M5Stack-GREY-blue)
![fire](https://img.shields.io/badge/M5Stack-FIRE-orange)
![core2](https://img.shields.io/badge/M5Stack-CORE2-green)
![aws](https://img.shields.io/badge/M5Stack-AWS-orange)

**First of all, many thanks to all my [donors](#donations)🙏🏻** 

The M5HamRadio project is a compilation, in one huge firmware, of my stable HamRadio projects on M5Stack. It include 3 applications :

- ICSMeter (default application)
- ICMultiMeter
- DXTracker

All these applications are available for free and for all !

**Big (r)evolution, you don't have to install the whole compilation chain, VSCode & Plateform.io. You don't need to be a developer or a command line expert anymore. I tried to make it as simple as possible.**


|![ICSMeter](https://github.com/armel/M5HamRadio/blob/main/img/ICSMeter.png)|
|:--:|
| ICSMeter |

|![ICMultiMeter](https://github.com/armel/M5HamRadio/blob/main/img/ICMultiMeter.png)|
|:--:|
| ICMultiMeter |

|![DXTracker](https://github.com/armel/M5HamRadio/blob/main/img/DXTracker.png)|
|:--:|
| DXTracker |


# Installation

## Prerequisites

You need an M5Stack (with 16MB Flash Memory), a micro SD card and a PC under Windows, Linux or MacOS, with the USB drivers installed and the M5Burner application version 3.0.0 (or higher).

## Micro SD card

Prepare and format a micro SD card in FAT32. This micro SD card will be used to put your configuration files and to place other firmwares.

## USB drivers installation

Please go to [download page](https://docs.m5stack.com/en/download) to download the USB driver that matches your operating system, and install it.

> Note: Core2 currently has two CP2104/CH9102F A USB chip version, users can install the drivers (CH9102 and CP210x) that are compatible with two ICs at the same time to ensure that the device drivers work normally.

## M5Burner installation

Please go to [download page](https://docs.m5stack.com/en/download) to download the M5Burner (version 3.0.0 or higher) that matches your operating system, and install it.

## Firmware flash

Connect your M5Stack to your PC.

Launch the M5Burner application and select the M5HamRadio firmware for your M5Stack model. Be aware, there is a version for M5Core (Basic, Grey, Fire, etc.) with buttons and a version for M5Core2 (Core2, AWS, etc.) with touch screen. 

Click on the blue Download button. Then click on the red Burn button.

|![M5Burner](https://github.com/armel/M5HamRadio/blob/main/img/M5Burner.png)|
|:--:|
| M5Burner |

## About TX settings (for USB usage via ICUSBProxy)

Here is a part of my transceiver settings, on IC-7300 :

```
Set > Connectors > CI-V > CI-V USB Port       Unlink from [REMOTE]
Set > Connectors > CI-V > CI-V USB Baud Rate  115200
Set > Connectors > CI-V > CI-V USB Echo Back  OFF
```

## ICSMeter, ICMultiMeter and ICKeyer .ini file settings

Using a plain text editor, you will create a file that should have the `.ini` extension. For example `IC705BT.ini` if you plain to use an IC-705, connected by Bluetooth. 

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

> About Icom Config section, here are some explanations. About `icom_model` choose between 705, 7300 or 9700. About `icom_address`, this is your Icom CI-V Address. About `icom_connect` choose between BT or USB (if you choose USB, you will need ICUSBProxy). Last, about `icom_device`, this is the BT Address of your 705 (from your transceiver, enter Menu and go to Set > Bluetooth Set > Bluetooth Device Information).


> Note that, Proxy Config section is ONLY useful if you linked your M5Stack to your Transceiver via USB using ICUSBProxy. If you are using Bluetooth, you do not need to change this section of settings. So leave values as they are, by default. The same goes for the Geolocation Config section which is ONLY useful for DXTracker. But if you fill in this section (and the Wifi Config section) correctly, this `.ini` file will also work for the DXTracker too.
 
Please, again, **take the time to adapt the values to your use**. It's important !

Here is an another example, if you're using an IC-7300, with this `IC7300USB.ini` :

```
; Icom Config
[icom]
icom_model = 7300
icom_address = 0x94
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

> You are able to put multiple .ini settings files for all your transceivers. I have got 3 of them for my IC-705 in BT mode, my IC-705 in USB mode and my IC-7300 in USB mode. I put them in this repository in the `ini` folder. 

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

> If these two sections Wifi Config and Geolocation Config are correctly settings in one of your others `.ini` files for ICSMeter, ICMultiMeter or ICKeyer, this will work too.

# Usage

Ready to go? Your M5Stack has been flashed with M5Burner? Your micro SD card has been formatted and you have saved your modified `.ini` files with your settings? Good. So let's go.

## Bin Loader

By default, M5Stack will start on ICSMeter firmware. At startup, you'll see the Bin Loader with a green gauge. You have 3 seconds to use the bottom middle button to select another firmware. Pressing the left or right button will bypass this step. 

## Ini Loader

If the micro SD card is correctly inserted in your M5Stack, you'll now see the Ini Loader with a blue gauge. You have 3 seconds to use the bottom middle button to select an `.ini` file that you put on it. Select the `.ini` file you would like to load and... enjoy.

> When you select an .ini file with the Ini Loader (and if it is valid), a copy is made on the Flash memory of the M5Stack. And if at the next reboot you do not make any action / selection of .ini file with the Ini Loader, it is this last valid `.ini` file, in Flash memory, that will be read automatically. This way, you can remove the SD card from your M5Stack, if you wish.

> So, if you change something in your .ini file (for example, the Wifi password, etc.), **you must restart your M5Stack and select it again from the Ini Loader to force reload this new version**. A new copy will then be made in the M5Stack Flash memory. And it will be this new version that will be read at the next reboot (if no action / selection with the Ini Loader).

# Add more firmwares

Even if you already have 3 firmwares (ICSMeter, ICMultiMeter and DXTracker) after flashing your M5Stack via M5Burner, you can add other firmwares to the root of the micro SD card. 

Maybe it's time to test my last project : ICKeyer !

> **Important ! Important ! Important !** If you want to try ICKeyer in USB mode, you need to use the [ICUSBProxy](https://github.com/armel/ICUSBProxy) version 0.0.6 or upper. Note that ICKeyer works now on M5Stack Core and Core2 ! 

> **Important ! Important ! Important !** Because applications now use LittleFS and not SPIFFS, if you have old firmwares based on SPIFFS, consider replacing it with the latest versions using LittleFS. If you don't, after loading an old firmware using SPIFFS, it will reformat your flash memory and overwrite any firmware you already have. So, be aware.

|![ICKeyer](https://github.com/armel/M5HamRadio/blob/main/img/ICKeyer.png)|
|:--:|
| ICKeyer |

You find the firmwares of all these projects in this repository, in the `firmwares` folder, of course for free ! 

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
| HF Propagation Tools and Solar Data | Paul L Herrman N0NBH				  | https://www.hamqsl.com/solar.html 			 |

Icom and the Icom logo are registered trademarks of Icom Incorporated (Japan) in Japan, the United States, the United Kingdom, Germany, France, Spain, Russia, Australia, New Zealand, and/or other countries.


# Donations

Special thanks to Rolf Schroeder DL8BAG, Brian Garber WB8AM, Matt B-Wilkinson M6VWM, Robert Agnew KD0TVP, Meinhard Frank Günther DL0CN, Johan Hansson SM0TSC, Tadeusz Pater VA7CPM, Frederic Ulmer F4ESO, Joshua Murray M0JMO, Mark Hammond N8MH, Angel Mateu Muzzio EA4GIG, Hiroshi Sasaki JL7KGW, Robert John Williams VK3IE, Mark Bumstead M0IAX, Félix Symann F1VEO, Patrick Ruhl DG2YRP, Michael Beck DH5DAX, Philippe Nicolas F4IQP, Timothy Nustad KD9KHZ, Martin Blanz DL9SAD, Edmund Thompson AE4TQ, Gregory Kiyoi KN6RUQ, Patrick Samson F6GWE, George Kokolakis SV3QUP, Ambrose "Bo" Barry W4GHV, Roger Bouche F1HCN, Christopher Platt, Pascal Paquet F4ICR, Gregory Kiyoi, Ning Yang BH7JAG and Mitsuhiko Nagasawa JL1LYT for their donations. That’s so kind of them. Thanks so much 🙏🏻

If you find this project fun and useful then [buy me a glass of wine](https://www.paypal.me/F4HWN) 🍷 🤗 

You could use the code F4HWN in order to get 5% discount on the [M5Stack shop](https://shop.m5stack.com/?ref=LUxetaH4) 🎁

By the way, you can follow me on [Twitter](https://twitter.com/F4HWN) and post pictures of your installation with your M5Stack. It always makes me happy ;) 