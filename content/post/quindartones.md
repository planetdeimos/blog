+++
date = '2025-07-20'
title = 'Quindar Tones - The Famous NASA Beep'
description = ""
aliases = []
author = "Admin"
+++

Eagle, Houston. Comm Check.

### Origins

![Apollo 11 On the Moon](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fblog.sciencemuseum.org.uk%2Fwp-content%2Fuploads%2F2019%2F07%2FApollo-11-astronaut-Buzz-Aldrin-stands-next-to-a-flag-on-the-moon-on-July-20-1969.-NASA-960x600.jpg&f=1&nofb=1&ipt=1ec5e6eb4c51dd717d5a49cb8902c99a1e689c7b6b93e27793190bb2df62fab8)

Today is July 20th, 2025. 56 years ago today, humanity took its first baby steps on an incredible journey to another world. Reaching the moon was no small task. Set out following President John F. Kennedy's challenge to the nation, NASA accomplished what no other nation to date has done. In my spare time, I participate in an Amateur Radio program called [NASA On The Air](https://nasaontheair.wordpress.com/). This organization participates in radio activations to commemorate milestones in American and Human spaceflight. Including all of the Apollo Missions.

If you're interested in spaceflight in any capacity, you might be familiar with the "Quindar Tones". But what are quindar tones, you may ask? Even as someone who is thoroughly entrenched in spaceflight history and obscure mission and vehicle facts and data, I personally had no clue what their official name was. Only that [CAPCOM](https://en.wikipedia.org/wiki/Flight_controller#Spacecraft_communicator_(CAPCOM)) used them as part of the communications between Mission Control Houston and the spacecraft during the mission. The day before Apollo 11's 56th landing anniversary, I overheard the Marshall Spaceflight Center (MSFC) club NN4SA operating with a variant of Quindar Tones. As a space nerd, I was instantly mesmerized and decided to work on an implementation for our own activation the following day.

### What Are Quindar Tones?
I wont bore you with the details, here's the [Wikipedia Page](https://en.wikipedia.org/wiki/Quindar_tones) if you want to really dig into the subject, but at a high level:
"the Quindar system, named after its manufacturer, Quindar Electronics, Inc., used two tones, both being pure sine waves that were 250ms long. The "intro tone" was generated at 2,525 Hz and signaled the "key down" key-press of the PTT button and unmuted the audio. The "outro tone" was slightly lower at 2,475 Hz and signalled the release of the PTT button and muted the audio."


### Short Timelines, No Standards

Anyone's who worked in the Audio world will tell you, there are very few standards. Most things are proprietary - or at the very least don't play well together. Of course there are exceptions such as the XLR, 1/4", 1/8" audio interfaces, but in general it's messy. The same is true for the radio world. In order to implement this properly, I needed to hack into the microphone circuity. To artificially add in a delay between when the two tones are transmitted and when the voice traffic is passed. Unfortunately due to the nature of having to implement this in under 24 hours and have no time to procure a sacrificial microphone capable of working with the Elecraft K3 we would use the following day, much more crude implementation would have to occur. 

Interestingly others including the Apollo Hardware restoration legend CuriousMarc has done this in the past, worth a watch! 

{{<youtube rAAFkjYxWj4>}}


### Implementation
This project has 4 major objectives:
> 1. Transmit a 2525Hz tone for 250ms
> 2. Wait a period of time while voice traffic is passed
> 3. Transmit a 2475Hz tone for 250ms
> 4. Be repeatable and reliable

Given all the timeline and hardware constraints, I opted to use an external solution that would not directly interface with the radio's PTT (push to talk) capabilities.
This project is crude in nature, after all it was implemented in about 2 hours from what I had laying around in my parts bin :)


![Fritzing Diagram](https://i.imgur.com/G7QYIRl.png)

After some brainstorming on how to make this work with any radio, regardless of vendor it became quickly clear the simplest method to be able to deploy rapidly was to use a common Arduino Uno, button, and speaker.

When the button is pressed down and held, the first 2545 Hz tone is played. The circuit sits silent until the button is released, when the second 2475 Hz tone for 250ms is played by the speaker.

All I had to do from a hardware perspective is to wire up a button and a speaker to two pins on the Arduino. That's it - that the whole circuit.

The Arduino was programmed with the normal IDE, full code used can be found at my [Github Repo](https://github.com/planetdeimos/QuindarTones)

After some quick bench testing and troubleshooting and adding of debounce code, we were ready to deploy our system to celebrate Apollo 11!


### Operations

After getting setup at the N1KSC shack, the final setup for operations looked like the following:

![Shack Setup Diagram](https://i.imgur.com/gB4YZ6V.jpeg)

I ended up using two microphones. One for actual voice communications and the other exclusively to trigger the Arduino. In a quick lookabout my parts bin, I had a Kenwood style microphone branded TYT that I found abandoned at a hamfest. Researching Kenwood pinout diagrams, I was able to connect to the PTT pins to allow for a simple and ergonomic solution to triggering the arduino. Crude as hell, but ultimately more ergonomic then anything else I had laying around.

The mess of red/orange wires is to the speaker, which was temporarily taped near the top of the transmitting microphone connected to the Elecraft K3.

![Speaker Mic Photo](https://i.imgur.com/AJoSOHx.jpeg)


This ended up with a unique operating condition. Having to hold two microphones simultaneously to talk. I followed the following workflow:
>1. Hold Down Radio PTT
>2. Press and Hold Tone Button
>3. Speak Into Transmit Microphone
>4. Conclude Transmission by Releasing Tone Button
>5. Release Radio PTT

It took a couple tries to get things going smoothly, but in the end, there were some very solid results!


Below is audio captured by family several states away, I'm the operator and really sets an interesting precedence of how this simple setup can provide an incredible layer of immersion into the event and get people interested in space history!
{{<youtube kstWFDS7sEQ>}}


### Conclusion

Anytime I can learn something new or grow it's a win for me both professionally and personally. This project, was implemented extremely fast and not with the highest workmanship standards. All things considered it was an excellent introduction into a sect of space history I was not very familiar previously; with and reminded me once again the value of being able to rapidly prototype and test electronics - a very useful skill to maintain as an engineer.

Ad Astra.
