---
name: IoT security vulnerabilities and predictive signal jamming attack analysis in LoRaWAN
tools: [University, IoT, Networks]
image: "/assets/img/projects/iot-lorawan-dissertation-card.png"
description: A look at IoT security limitations and signal jamming in the low power wide area network technology LoRaWAN
---

# IoT security vulnerabilities and predictive signal jamming attack analysis in LoRaWAN

![lorawan paper preview](/assets/img/projects/iot-lorawan-dissertation-title.png)

This paper was based off of the research I did for my final year project dissertation while at university. Initially, I hadn't planned to do anything related to IoT as I was prototyping an idea for a learning website which dynamically changed aspects of itself as the user progressed further in the online course. Unfortunately, it was deemed as being far too much work in the space of time we had so I moved on, instead browsing the internal list of dissertation supervisors and their preferred areas of interest and/or expertise. On a whim, and with the deadline for choosing a supervisor looming, I opted to investigate everything IoT, low power wide area networks, and LoRaWAN.

## Research

Research for this project consisted mainly of exploring the current limitations and overall functions of LPWAN technology, and then identifying gaps where additional research could take place after heavily trawling through many academic papers and studies. Due to the nature of these devices, they needed to draw very little power and only transmit when they absolutely had to, in order to conserve resources. Due to this, security was a topic that came up frequently when researching these papers, if a device is low powered, then the encryption options available to it may also be limited.

I was fortunate in that the University had very recently installed an antenna on the roof of the main building which was configured to be used exclusively for IoT projects, with myself being among the first people to utilise and test it. Having this available meant that I could send test messages without issue or much delay from my equipment at my flat to the university, over an impressive distance of 2 miles.

With the foundational exploration done, various initial ideas were exchanged between myself and my dissertation supervisor, Dr. Deepayan Bhowmik, including exploring machine learning in Python to analyse messages sent by devices to see if content patterns could be identified. As I researched further and built upon my literature survey and methodology, I decided to take a close look at the networking around the LoRaWAN. Specifically, how messages are transmitted, the format in which they are transmitted, and whether any information could be easily gleaned from this which could potentially aid in identifying possible attack vectors.


## Equipment
{% include elements/figure.html image="/assets/img/projects/iot-lorawan-dissertation-01.png" caption="Sodaq ExpLoRer" %}

The equipment used for this project included two "Sodaq ExpLoRer" boards, and a home base station which could pick up messages from the Sodaq boards (as well as from any other LoRaWAN capable device in the area). The boards were about the same size as a credit card and were operated by a single coin cell each, the base station was powered by mains and had an ethernet backend for transmitting any received messages to a central portal over the internet.

Boasting a range of up to 3 miles in built up urban areas, and potentially up to 10 miles in more rural settings, as well as an operating time on a single battery potentially being measured in multiple years depending on device configuration, LoRaWAN devices are fantastically adapted to various agricultural and industrial applications.


## Testing and Methodologies

After deciding on the direction I was going to take my research, and properly assessing my proposed methodologies, I got to work on gathering data for my project with the hope that repeatable results would be found to draw interesting conclusions from. After some preliminary testing, I'd decided on exactly what I was trying to achieve and how I was planning on achieving it.

The plan was to attempt to disrupt the connection of the first of the two Sodaq boards I had (the legitimate user in this scenario) by flooding the base station with messages from the second Sodaq board (the attacker in this scenario) to see if I could devise a system where the attacker board could reliably cause the messages from the legitimate board to be lost. The base station I had was only half-duplex, meaning that it can't transmit and receive at the same time, it has to choose one or the other.

If the base station is currently being occupied by responding to the garbage messages of the attacker board at the same time the legitimate board wishes to send a message, then its message would be dropped. I was able to test this using different message sizes and other tweaked parameters in order to nail down a working system, for example, each device is hardcoded to adhere to the maximum duty cycle as defined by local laws and device regulations. This duty cycle however is reset when the device loses power, meaning that if you've reached the maximum duty cycle but wish to continue flooding messages to a base station, a simple timed reset of the sending device can alleviate this to great effect.

To make sure I was resetting my attacker device at the correct time, I measured and averaged out the intervals between messages of the legitimate device, as well as the reset time of the attacker board, this information put into an excel calculator I had built enabled me to reset the attacker board at just the right time so that it sends a flood of connection messages to the base station as the legitimate device is attempting to send its message.

After running multiple tests and scenarios I finally had my data set which I could then draw conclusions from and analyse for my dissertation.


## Conclusion

I was shocked that my testing had gone as well as it did, naturally, there were many optimisations that could have been done during testing, especially as I was manually resetting my attacker device as opposed to writing a script or such in order to read the data from calculator and automatically power cycle the device, but time was unfortunately limited.

In the end, with the proper settings in my specific controlled testing environment, I was able to block most or all of the legitimate messages destined for the base station with my attacker device. But there's still much more work that could be done with this, especially as the technology continues to evolve and security and protocols get better. When I handed my work in, the only thing I was concerned about was passing the module so I could earn my degree. I would never have guessed that the feedback I received from my supervisors was so positive that they ended up submitting it for publication. While I was absolutely glad to get the degree classification I did, I'd probably consider this to be my greatest achievement during my time at university. If you're at all interested in the full paper, I've included a link to it below.

If you have any questions regarding the content of this article, or anything else you may find on this site, please contact me at maxingham@duck.com.

<p class="text-center">
{% include elements/button.html link="https://ietresearch.onlinelibrary.wiley.com/doi/full/10.1049/iet-ifs.2019.0447" text="View The Paper" %}
</p>
