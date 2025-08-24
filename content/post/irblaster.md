+++
date = '2025-05-01'
title = 'Hacking a Holmes Tower Fan to Work with HomeAssistant'
description = ""
aliases = []
author = "Admin"
+++
### Background
Some time ago I bought a cheap vertical tower fan for my project room from a big box store. No thrils, no built-in IOT connectivity, just a cheap and simple fan that redirects air from a hallway into a room bustling with electronics! 

Most of the time, when I purchase some appliance, there's some long term strategy and thought it put into place regarding if it'll be integrated into my smart home - usually a google search seeing there is some form of HomeAssistant integration. In this case however no such planning was made.
As part of my quest to develop both a secure and automated smart home, I wanted to integrate this into my HomeAssistant ecosystem without having to purchase a new product. 

It's a 40" stand fan, Item: 12863, Model: 32510453

It quickly became very obvious that modifing the fan to do what I wanted to do was going to be a challege. The controls on the fan itself are not physical buttons, but rather utilize capacitive touch, making a servo or similar COTS product impractical.
Next I looked at mounting an IR LED to the fan body itself, writing a simple arduino script to control didnt see to big of a deal, but I wanted to use ESPHome with HomeAssistant, and determined that to be both buggy and impractical. Digging through my parts bin, I found a long abandonded universal remote control. I extracted the IR LED and attempted to use that as a priminate remote control of sorts.

There was also the concern of powering the microcontroller that would have to be mounted onto the fan body itself, cable managed, and a seperate dc power supply run to interface with the controls. 

I then noticed the largely forgotten remote control stashed away in the back of the injected molded fan housing. I quickly zeroed in on using this for my project. The remote control wasnt used by me at this point, so modifying it caused no heartbreak or loss in capabilities.
![Picture of OEM Remote](https://i.imgur.com/Y1FlCxr.jpeg)

Next, I took apart the remote housing to quickly identify how the circuit was put together, and to see if there was any possibility of hyjacking it to control the fan.
![OEM Remote Expanded View](https://i.imgur.com/zH0sJvq.jpeg)

The device is powered off of the common CR2032 Lithium battery, which operates at 3v nominally, this was excellent news, as it meant I could easily tap into the 3.3V rail on the ESP32 and would not require and non-native voltage regulation or voltage dividers! Thankfully, the designers of the PCB had some forethought, and left an availible pad on the design (C1) that could easily be tapped into the power the device. One quick set of bodge wires later and a quick hookup to a regulated powersupply, and we're in buisness to get to the main event - hacking the controller!
![External Power Supply](https://i.imgur.com/hfkfBWK.jpeg)


Next, it was time to understand the logic of how the device operates. At its core, when the buttons on the remote are pressed, the remote IC sends a series of IR pulses out to command the stand fan. In our case of project requirements, minimum viable product was to simply power on the fan to start circulating air in its default state. Because this is a very simple and low cost product, the entire PCB was a handful of surface mount components and buttons, with a singular IC and a handful of resistors on the opposite side.

