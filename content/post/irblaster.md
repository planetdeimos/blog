+++
date = '2025-05-01'
title = 'Hacking a Holmes Tower Fan to Work with HomeAssistant'
description = ""
aliases = []
author = "Admin"
+++
### Background
Some time ago I bought a cheap vertical tower fan for my project room from a big box store. No thrils, no built in IOT connectivity, just a cheap and simple fan that redirects air from a hallway into a room bustling with electronics! 

Most of the time, when I purchase some appliance, there's some long term strategy and thought it put into place regarding if it'll be integrated into my smart home - usually a google search seeing there is an integration. In this case however no such planning was made.
As part of my quest to develop both a secure and automated smart home, I wanted to integrate this into my HomeAssistant ecosystem without having to purchase a new product. 

It's a 40" stand fan, Item: 12863, Model: 32510453

It quickly became very obvious that modifing the fan to do what I wanted to do was going to be a challege. The controls on the fan itself are not physical buttons, but utilize capacitive touch, making a servo impractical.
Next I looked at mounting an IR LED to the fan body itself, writing a simple arduino script to control didnt see to big of a deal, but I wanted to use ESPHome with HomeAssistant, and determined that to be both buggy and impractical.
There was also the concern of powering the microcontroller that would have to be mounted onto the fan body itself, cable managed, and a seperate dc power supply run to interface with the controls. 

I then noticed a forgotten remote control stashed away in the back of the injected molded fan housing. I quickly zeroed in on using this for my project. The remote control wasnt used by me at this point, so modifying it caused no heartbreak
