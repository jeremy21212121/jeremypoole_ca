+++
date = "2021-01-07"
title = "Announcing EvoFinder.ca"
tags = ["security","webdev","mitmproxy"]
math="false"
published="true"
+++

<figure class="blog-figure">
  <img src="/images/ef.jpg" alt="Evo Finder- Find nearby Evo car share vehicles"/>
  <figcaption>
    <a href="https://evofinder.ca" target="_blank" rel="noopener">Evo Finder-</a> Find nearby Evo car share vehicles
  </figcaption>
</figure>

## An unofficial web client for Evo Car Share

I'm a happy user of the Evo Car Share service here in Vancouver. Unfortunately, about a year ago they discontinued their web interface. This was a problem for me, as I used a web browser to interact with their service.

I don't know why they got rid of it. It looks to me like their platform vendor, Vulog, doesn't offer the option anymore. Even if I wanted to run their Android app, I couldn't. It crashes if it can't find Google Play services. Decompiling the app, one can see it is full of tracking and retargeting libraries from the likes of Baidu and Facebook.

### What now?

So, I have a problem. I want to use the service, but it has become very difficult for me to do so. The only reasonable course of action I could find was to reverse engineer the Android app and re-implement a subset of its features as a web app.

Now that the MVP is up at [EvoFinder.ca](https://evofinder.ca), I'm going to be writing a detailed blog post on the process in the near future.

### From Android app to web app

An upcoming post will cover the reverse-engineering process. In a nutshell, I ran the Android app on my workstation using an emulator and I intercepted all communications using [mitmproxy](https://mitmproxy.org/). Setting up the environment was surprisingly tedious. Using the captured traffic as documentation, I made a [prototype](https://github.com/jeremy21212121/evo-re) first in Bash, then in JavaScript and finally the [finished version in TypeScript](https://github.com/jeremy21212121/evo-client-nuxt/blob/master/plugins/AnonApi/index.ts).



### Summary

The whole thing has been a ton of fun. I still have a few bits and pieces to add to the web app, but it is already useful. I am not going to make use of the authenticated portion of the API, which would allow users to reserve cars. It would be cool, but I don't want to upset anybody. As it is now, I have to hope nobody reserves the car before I can get to it. But at least I can use the service!

I just want to make it clear that this was a labour of love. I enjoy the service and I wanted to be able to continue to use it, so I spent over 100 hours of my time making that possible. If this project offends anybody, please don't hesitate to contact me.

