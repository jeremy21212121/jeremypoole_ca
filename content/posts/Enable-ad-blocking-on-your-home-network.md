+++
date = "2018-03-21"
title = "Block ads on your whole home network with Pi-Hole"
math="false"
+++

## definitions
1. Raspberry Pi (RPi) - a small multi-purpose computer, capable of running Linux, with about as much power as a modern smartphone. It can be connected to a screen via HDMI or used as a server and accessed over SSH.
2. Pi-Hole - a DNS server that can block ads at the domain name level.
3. DNS - the phone book of the internet. It provides the IP address for a given domain name (for example, google.com).

## how does it work?
Generally, ads are served from a different domain name than the website or app content. Pi-hole exploits this fact by returning the wrong IP address for the ad server. This results in a 404 error and the ads not loading.

The RPi connects to your home router with an ethernet cable.

## limitations

This will not block all ads. Some apps are too clever for this approach. The YouTube app, for example, detects the ads not loading and serves them from a domain that serves content as well. This makes it impossible to block the ads this way without also blocking the content.

It will not block as many ads as a well-configured browser extension, like ublock. This is because browser-based ad blockers can use different techniques to detect ads, like inspecting the class names of HTML elements.

## where does this approach really shine?

This approach is great for providing a base layer of ad and malware domain blocking, for your whole home network. Every internet connected device gets this level of protection with no extra configuration required.

It will also block ads in some apps, which a browser-based ad-blocker cannot.

An added bonus is it can prevent novice users from accidentally infecting their device with malware, by blocking known malware domains.

## what do I need?

You'll need a raspberry pi, USB power supply of at least 2.5 amps and a case is a good idea. This can be had for about $100 CDN from amazon or wherever.

You will need a microSD memory card of at least 8gb, 16gb is better. SanDisk, Samsung and PNY are good brands. Beware fakes, amazon is riddled with them. You'll load the Raspbian OS on to this, which is a version of Debian Linux tailored for the RPi.

The installation of the Pi-Hole software itself is quite straightforward. You'll just need to follow the prompts. A bit of Linux command-line and SSH knowledge wouldn't hurt. Otherwise, this is a great way to learn!

You'll also need to set your router to use your new RPi as its DNS server. This can be done through your routers admin interface, often located at 192.168.0.1.

For full instructions, check out [the awesome official documentation](https://docs.pi-hole.net).
