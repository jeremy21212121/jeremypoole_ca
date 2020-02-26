+++
date = "2019-11-28"
title = "Non-printable characters in HTML"
tags = ["html","webdev","bug"]
math="false"
published="true"
+++

<figure class="blog-figure">
<img src="/images/ascii.png" alt="ASCII code chart"/>
<figcaption>
ASCII code chart
</figcaption>
</figure>

This is an interesting bug that I have stumbled across a few times. Sometimes it is invisible, but it varies by browser and OS.

For those who aren't aware, there exist characters which cannot be printed. By characters I mean letters, glyphs, etc. I'm writing a bunch of them right now!

## How letters work on computers

First, a quick recap. Most developers probably know that characters are represented by numbers on computers. Computers really prefer numbers. There are different character encoding schemes (ways of mapping numbers to characters), such as ASCII (which dates way back to the TeleType days of the 60's) and Unicode. Unicode is what we use now, and the first 128 character codes are the same as ASCII. So for our purposes, we will ignore encoding scheme.

## What are these unprinted characters of which you speak?

Letters are represented by character codes. For example, "a" is 97. We can confirm this by running this in the browser console: `'a'.charCodeAt(0) === 97` or by looking up a chart of ASCII or Unicode character codes.

The first 32 character codes (0-31) are not printable. They do not represent letters. They are called control characters. These harken back to the days of TeleTypes. They would instruct the TeleType to do things, for example peform a carriage return (basically a new line on a type writer). These control codes live on today, in terminals to do things like text color, and in text to start on a new line.

Fun fact, windows and linux line endings are different. Pressing "enter" in a text editor on linux creates char code 10 (line feed) whereas on windows it also includes a carriage return (code 13). In fact, systems vary widely in how they handle these control characters.

## And so begins the End-of-text (ETX)

Character code 3 is known as the end-of-text character. It is used the signify the end of text on some systems, presumably. Some text editors like to include this character for some reason that I'm sure made sense at the time. Windows tends to not display this character, but it still gets included when text is copy-and-pasted. But unfortunately, all systems do not handle this character the same way.

## How to print the unprintable?

There is no "correct" way of displaying unprintable characters. Some systems ignore them (IE11, safari, android), chromium/linux show the tofu character (࿿), others still seem to display them as a space (Edge). They are most obvious on chrom{e,ium} on linux, because they are rendered as empty boxes.

## So what?

If you copy-and-pasted text content for your website, it could well have unprintable characters in it. A subset of your users could be seeing ugly boxes in their text.

## The horror! Please save me from this fate

The good news is there are plenty of tools to help you. [This one](https://www.soscisurvey.de/tools/view-chars.php) let's you paste text into a form and it will show you any invalid characters it contains.

You could also make a test or build step for dealing with them. Once you know they exist, there is nowhere they can hide!
