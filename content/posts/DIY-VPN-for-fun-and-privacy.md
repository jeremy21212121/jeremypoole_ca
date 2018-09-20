+++
date = "2018-07-15"
title = "DIY VPN for fun and security"
tags = ["technical","VPN","security"]
math="false"
+++

## what exactly is a VPN?

A VPN is basically an encrypted tunnel for your internet traffic. They can be used for accessing a corporate or home network remotely, or for privacy/security purposes. This post will focus on the latter.

The tunnels ends at a VPN server. This VPN server may be run by you, or by a VPN service provider like "Private Internet Access". The end of the tunnel is a privileged location that you must trust completely. 

Unless you are operating the VPN server yourself, you can't know for sure if it is logging the sites you visit and selling that data, or something more nefarious. There are many ways that a negligent or malicious VPN provider can degrade your privacy or security. For example, a poorly isolated, shared VPN server can open you up to attacks from other users of the VPN service.

## what are the limitations?

The following will not protect you if you plan on breaking the law. So if that is your plan, you might as well give up now because you are woefully unprepared.

It also won't facilitate piracy. Digital Ocean, the service provider we will be using for our server, will shut down your account in a heartbeat.

## well what IS it good for, then?

In a word, privacy. Mostly from unscrupulous Internet Service Providers that want to "monetize" your internet activity. Thankfully, that seems to be less of an issue in Canada than it is to the south. I use a VPN mostly when I am on untrusted or public WiFi, because I feel I can trust my home ISP. 

It can also be used to get around some "geo-fencing" (content blocking based on region). You will need a VPN server in each country you want to appear to be in.

 *A caveat if that content happens to be video:

1. Video streaming uses a lot of bandwidth. If you stream video heavily over your own VPN server, you will get additional bandwidth charges, which can really add up. For this use case, you may be better-off with a commercial VPN service with unlimited data.
2. Some video streaming services, like Netflix, are really quite good at blocking VPN users. They seem to have blocked all the IP addresses of the major VPS providers (Digital Ocean, Amazon Web Services, Google Cloud, MS Azure). If this is your use case, you will have to do some research to find a provider that isn't blocked.

## enough disclaimers, let's get to it!

OK, this can go one of two ways: The easy way or the hard way.

Both ways will give you effectively the same end result, a private VPN server running on a virtual Linux server with Digital Ocean for $5 a month.

### the hard way

The hard, and educational, way is to setup your own Ubuntu server on Digital Ocean and configure OpenVPN. 

Digital Ocean publishes the best guides, in my opinion, for configuring popular open source software on Linux servers. And their [guide for configuring OpenVPN](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-ubuntu-16-04) is no exception. A bit of experience with command-line Linux and SSH is definitely an asset, but you can also figure that out as you go.

It took me a couple hours to get it all set up. Manually configuring OpenVPN gave me much better insight into how it works.

To connect to your newly-created VPN server, you will need client software on each device you wish to connect from. On Android, I recommend the open-source app, aptly-named OpenVPN for Android, available from f-droid. I have found it to function very well, automatically reconnecting as I change between WiFi and LTE.

On my laptop running Linux Mint 18.3, a VPN client is integrated into the network manager. So, no additional software needed to be installed.

### that's not my idea of fun, give me the easy way

The easy way is to use software called [Outline](https://getoutline.org). It is [open source,](https://github.com/Jigsaw-Code/?q=outline) made by Google, and available for computers and mobile devices. It is intended for journalists, but it works equally well for non-journalists.

This software creates and configures a Linux server with OpenVPN automagically. You can even create an account with Digital Ocean, if you don't have one yet.

It also handles connecting to the VPN from your client devices, supporting nearly every platform. This is as easy as it gets!
