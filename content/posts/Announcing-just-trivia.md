+++
date = "2020-02-15"
title = "Soft launch of open-source trivia web app Just Trivia"
description = "An open-source trivia game with no ads or tracking"
image = "images/trivia.png"
tags = ["PWA","JS","Vue.js","Nuxt.js","web app"]
math="false"
published="true"
+++

<figure class="blog-figure">
<a href="https://justtrivia.fun">
<img src="/images/trivia.png" alt="Just Trivia logo"/>
</a>
<figcaption>
Logo for <a href="https://justtrivia.fun">Just Trivia</a>
</figcaption>
</figure>

## Announcing JustTrivia.fun, a lean mobile trivia game for phones and tablets

The MVP of my passion project has just been released! [Just Trivia](https://justtrivia.fun) is a mobile-focused trivia game with no ads, tracking, or monetization of any kind. I built this because I wanted a simple, light-weight trivia game to play on my phone, but couldn't find one.

It is a progressive web app, which means it can be installed to the home screen on mobile devices and behaves like a native app on subsequent launches. It is lean, with the whole app bundle, before splitting, weighing in at about 700kb. Each round of 10 questions only uses about 7kb of data.

## Early reception

I soft-launched the MVP of this game 3 days ago and I have been delighted with the usage so far. Before yesterday, I had only sent the link to a few friends and family. The peak load had been about 3 concurrent users.

Then, while browsing [HN](https://news.ycombinator.com) before bed, I saw a post about the [demise of Trivia HQ](https://news.ycombinator.com/item?id=22331339). Seeing an opportunity to shamelessly plug my creation, I [posted a comment](https://news.ycombinator.com/item?id=22334090) briefly outlining Just Trivia and went to sleep.

When I woke up, it only had 2 replies. One was a potential bug report, the other was not related. I was pumped one person had tried it and shared their issue.

Since, as promised, there is no tracking, my debugging options are limited to basically `grep`-ing through the nginx logs. I haven't even setup [GoAccess](https://goaccess.io/) yet. The log file was much bigger than I expected. Lots of hackernews in the referrer field.

I wonder how many unique IPs came from HN?

```bash
$ cat access.log | grep https://news.ycombinator.com/ | sed -r 's/(^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}) .*/\1/' | uniq | wc -l

> 550
```

Wow! That is amazing. 550 unique IPs came from HN! And more still probably didn't set the referrer header. How many actually played the game, though?

```bash
$ cat access.log | grep /start | sed -r 's/(^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}) .*/\1/' |  uniq | sort | wc -l

> 1113
```

Woah! Over a thousand unique IPs started a game in the relevant 12 hours! That is phenomenal! Almost nothing makes me happier than when people use the software I make.

Only a few tens of those IPs are from people I know. Almost all came from that one HN comment. I wonder if anyone played multiple games?

```bash
$ cat access.log | grep /start | sed -r 's/(^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}) .*/\1/' |  uniq -c | sort | tail

>
>      3 *serbian IP address*
>      3 *UK IP*
>      4 *washington state*
>      4 *atlanta*
>      4 *new jersey*
>      4 *new jersey*
>      4 *new jersey*
>      4 *washington state*
>      5 *washington state*
>      8 *minnesota*
```

> IP addresses have been replaced with the region returned by `whois`

I am truly amazed. To the person in Minnesota that played 8 rounds, thank you so much!

## Next steps

These results have me blown away. I was planning to do a "Show: HN" post in the near future, but I might have to move that timeline up! I have so many great ideas for the future and this has been really encouraging.

### Offline play

> [Github issue](https://github.com/jeremy21212121/trivia-frontend/issues/6)

The whole trivia DB is only about 1 MB. By including the DB and server logic in a service worker, we can enable offline play with minimal modification to the client. This is a high priority for me.

### Score tracking and visualizations

> [Github issue](https://github.com/jeremy21212121/trivia-frontend/issues/9)

I have some good ideas for storing score-related data and visualizing it for the user. This will enable showing streaks of correct answers, results of previous attempts at a question, etc.

### Improve and add questions

I'm working on an interface to allow people to easily propose updates and new questions. I'm also manually curating the DB, updating questions with typos or out of data answers.

### In-game feedback
A low-friction way to provide feedback on the game or a particular question. Currently the best option is to [open an issue](https://github.com/jeremy21212121/trivia-frontend/issues) on github.

Stay tuned, because there are many refinements and improvements to come!

## Github repos

[This](https://github.com/jeremy21212121/trivia-frontend) is the repo for the Vue.js/Nuxt.js front-end.

[This](https://github.com/jeremy21212121/express-trivia-server) is the repo for the Node/Express back-end. It is in pretty rough shape at the moment, don't judge me 😉.

## Hire me

I'm available for hire! Ideally I'm looking for full-time employment in Vancouver, BC, Canada. But I also love remote work and contracts, as long as there are challenging problems to solve.

Feel free to <a id="email" href="#" title="Contact Jeremy">contact me</a> with any opportunities.


