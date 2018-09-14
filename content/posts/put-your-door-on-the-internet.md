+++
date = "2018-06-12"
title = "Put your door on the internet with an esp8266"
math="false"
published="false"
+++

I live in an apartment building that has a very old buzzer/intercom system. I wanted be able to buzz myself in with only my smartphone, but there was a catch. I'm a tenant, so it has to be removable and not damage anything. I was mostly successful.


At it's most basic, the system consists of the following:


## An ESP8266 microcontroller

This is the brains of the operation. It is connected to the door release button in my apartment and wifi. It is programmed using the Arduino IDE, and exposes an API to be consumed by...


## A web app

This is a very basic web app that features only a button to open the door.



## __Security Warning__

Actually putting your front door on the open internet would be a bad idea. I have set it up so I must be on my local (wifi) network in order to unlock the door. Some sort of basic auth like a password would be a good idea, too.
