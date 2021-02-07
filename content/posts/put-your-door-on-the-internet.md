+++
date = "2019-01-12"
lastmod="2020-02-03"
title = "IoOT - Internet of Old Things"
description = "Connecting a vintage intercom system to the internet with the ESP8266 SoC"
image = "images/va-k_esp8266.jpg"
tags = ["IOT","esp8266","aiphone VA-K"]
math="false"
published="true"
+++

<figure class="blog-figure">
  <img src="/images/va-k_esp8266.jpg" alt="ESP8266 system-on-chip over the internals of a vintage Aiphone VA-K intercom"/>
  <figcaption>
    An ESP8266 System-on-Chip overlayed on top of the guts of a vintage Aiphone VA-K
  </figcaption>
</figure>

I live in an apartment building that has a very old buzzer/intercom system. I wanted be able to buzz myself in with only my phone, but there was a catch. I'm a tenant, so it has to be removable and not damage anything. I was mostly successful.


## The old hardware
The unit in my apartment is an ancient aiphone model va-k. It is basically a phone handset and a button for opening the main building door.

The following image shows where the button contacts are:

<figure class="blog-figure">
<img src="/images/aiphone_va-k.jpg" alt="Aiphone VA-K handset internals"/>
<figcaption>
The guts of an Aiphone VA-K handset with button contacts circled
</figcaption>
</figure>

I connected leads to the switch contacts, connected those to a NPN transistor, connected an IO pin on the ESP8266 to the gate (middle pin) of the transistor and tied the grounds together. A large-value resistor (2k-10k or so) is used to pull down the IO pin.

You could use a relay instead of a transistor, and you wouldn't have to tie the grounds together.

If that wasn't clear, the following diagram (not to scale) probably won't help. But I had fun making it.

<figure class="blog-figure">
<img src="/images/dm_diagram.png" alt="Aiphone VA-K handset internals"/>
<figcaption>
A super technical diagram
</figcaption>
</figure>


## An ESP8266 microcontroller

This is the brains of the operation. It is connected to the door release button in my apartment and wifi. The code can be [found here](https://github.com/jeremy21212121/doorman-building-arduino). It is programmed using the Arduino IDE w/ [esp8266 library](https://github.com/esp8266/Arduino), and exposes a simple API to be consumed by...


## A web app

This is a very [basic web app](https://github.com/jeremy21212121/doorman-webapp) that features only a button to open the door. It works with a hard-coded IP address that is only accessible on my local network. Adding mDNS would allow me to remove the hard coded IP, but unfortunately my phone doesnt support mDNS :(

It is hosted at old.jeremypoole.ca and intentionally served over plain HTTP to avoid a mixed content error in the browser.


## __Security Warning__

Actually putting your front door on the open internet would be a bad idea. I have set it up so I must be on my local (wifi) network in order to unlock the door. Some sort of basic auth like a password would be a good idea, too, as it is currently pretty insecure.

It is also an XSS nightmare, as any website I browse could potentially unlock the door if it knew the URL. That would be a great targeted attack vector, if only I was more interesting and/or that door wasn't left open half the time anyway.

## But how reliable is it?

I have been absolutely shocked by the stability of this contraption. The only outages have been caused by my accidental disconnection of the power supply. The credit for this stability should go to the [devlopers of that lovely esp8266 arduino library](https://github.com/esp8266/Arduino/graphs/contributors).

### Update: January 2020

Still going strong a year later. It has been unreasonably reliable, considering it is run on a discount dev board. The LED burned out because they were too cheap to put a resistor inline and yet this monster marches on. When the board finally dies, I will use a smaller one and embed it inside the handset so it is invisible! I only installed it externally to make for easy servicing which miraculously hasn't been necessary.
