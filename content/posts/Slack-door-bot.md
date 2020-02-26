+++
date = "2019-08-09"
title = "Slack door bot"
tags = ["slack","IOT","bot","electronics","esp8266","arduino"]
math="false"
published="true"
+++

<figure class="blog-figure">
<img src="/images/slack_doorbot.jpg" alt="Finished slack door bot in project case"/>
<figcaption>
The finished slack bot in all its glory. The cable on the left goes to a USB power supply and the wires on the bottom go to the door buzzer button.
</figcaption>
</figure>

I love tinkering with electronics and embedded devices. As a software person, I find hardware fascinating. Apparently I have a thing for [unlocking doors](https://github.com/jeremy21212121/doorman-building-arduino).

So when I was on a contract recently where they had a legacy human operated door buzzer, I immediately saw the need for innovation.

> You can find the code for this project [here](https://github.com/jeremy21212121/slack-doorbot-esp8266)

## First steps

My dev board of choice for making simple IoT devices is definitely ESP8266-based. They offer [easy integration with the arduino IDE](https://github.com/esp8266/Arduino), they are very cheap and I have a bunch of them already.

## Overview

This bot listens for the magic words (open sesame) by slack direct message, then unlocks the door. Actually, it engages a relay, which can turn on/off whatever you connect it to. Lighting? Airhorn? High-voltage arc generator? The sky and your good judgement are the limit.

The intended use case is, however, connecting it to the button that buzzes people into your building.

I started with [urish/arduino-slack-bot](https://github.com/urish/arduino-slack-bot), got it working again, and made significant changes to suit my use case.

## Slack integration

This sketch uses the [Slack real-time messaging API](https://api.slack.com/rtm). First, it authenticates with the `rtm.connect` method via HTTP API. If successful, the HTTP API returns a websocket URL to connect to. Once established, the websocket connection is maintained with "ping" messages every 5 seconds.

This slackbot only responds to direct messages. Don't invite this bot into public Channels; it will receive every event from that channel and it may become overwhelmed. It is programmed to ignore messages from public channels, but it still needs to parse the JSON. For every message sent, there are usually 3 events that the slackbot must parse: a "user is typing" event, a "message" event, and a "desktop notification" event. We only have 80MHz of CPU!

## Software dependencies

- Arduino IDE

- [ESP8266 core for arduino](https://github.com/esp8266/Arduino)

- A modified version of the [arduinoWebSockets](https://github.com/Links2004/arduinoWebSockets) library[0](#Security) included in this repo

- [ArduinoJson](https://arduinojson.org/) library (V6)

## Hardware notes

- any dev board based on the ESP8266 SoC should be fine. I used a clone of the [Wemos D1 mini](https://wiki.wemos.cc/products:d1:d1_mini) because it is small.

- 5v relay module

The relay modules I have are "low-level trigger", which means they are activated by LOW rather than HIGH (0V rather than 5V). That is not what I want. I used an NPN transistor connected in such a manner that when pin D2 is HIGH, the relay input is brought LOW. This means the relay is activated when pin D2 is brought HIGH.

Pin D2 is pulled down using a 5k resistor.

A diode and capacitor are used in an attempt to decouple the SoC from the relay module, since the are both powered by the same source. The relatively-large-ish inductive load spike from the relay being enabled can cause instability for the SoC. Electrically, I'm making it up as I go, so I don't know if what I did actually helps. But it has been stable and reliable so I'll take it.

## Before flashing

Before flashing this sketch, make sure to `#define` the following constants in a file called `Secrets.h`:

* `SLACK_BOT_TOKEN` - The API token of your slack bot
* `WIFI_SSID` - Your WiFi signal name (SSID)
* `WIFI_PASSWORD` - Your WiFi password


## Security [0]

This sketch makes use of SSL for both HTTPS:// and WSS:// requests. Due to hardware limitations, the certificate fingerprint for HTTPS requests must be provided in the sketch. The current certificate at time of writing expires on Feb 12, 2021. If you are in the future, or slack changes their cert before then, you will need to update the SSL fingerprint.

Previously, SSL for websockets with the `arduinoWebSockets` library on the ESP8266 didn't have this limitation. Due to a change in the SSL library used by ESP8266 core, this is no longer the case. I don't think it is the same cert as for HTTPS, but I really don't know because I didn't try. So, in order to enable WSS:// connections, I have altered the websockets library to disable fingerprint verfication. Data in transit is still encrypted, but it is theoretically possible for a priveleged adversary to perform a man-in-the-middle attack. This is, in my opinion, a perfectly acceptable risk for a trivial slackbot. Doing SSL at all, on an 80mHz processor, is a small miracle.


# Hire me

I'm available for hire! Ideally I'm looking for a full-time employment in Vancouver, BC, Canada. But I also love remote work and contracts, as long as there are challenging problems to solve.

Feel free to <a id="email" href="#" title="Contact Jeremy">contact me</a> with any opportunities.

