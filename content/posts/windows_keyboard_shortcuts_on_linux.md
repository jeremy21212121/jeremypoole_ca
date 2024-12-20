+++
date = "2021-01-14"
title = "Bringing Windows keyboard shortcuts to Linux"
description = "Using the 'Alt' key and the number pad to type accented characters on Linux, just like on Windows"
image = "/images/keyboard_hotkeys.jpg"
tags = ["linux","desktop","cinnamon"]
math="false"
published="true"
+++

> Using "Alt" and the numberpad to type accented characters

<figure class="blog-figure">
  <img src="/images/keyboard_hotkeys.jpg" alt="Silly image of a gangsta linux penguin"/>
  <figcaption>
    I spent way too much time making this ridiculous image.
Credits: <a href="https://pixabay.com/users/clker-free-vector-images-3736/" target="_blank" rel="noopener">Penguin</a>,
<a href="https://pixabay.com/users/coxinhafotos-3726685/" target="_blank" rel="noopener">Monitor</a>,
<a href="https://pixabay.com/users/schmidsi-104144/" target="_blank" rel="noopener">Keyboard</a>
  </figcaption>
</figure>

## Note from 2024

I found out about the compose key at some point and switched to that, but this is still a fun silly hack.

## Preramble

I switched to Linux back in 2007. I hated XP, so I dual-booted Ubuntu. Then I corrupted my Windows partition and the rest is history.

But even before that, in school we learned to type French on English keyboards on Windows. It has a handy keyboard shortcut for typing these characters: Hold "Alt" and type the 4 digit character code. For example, to type "è" one would hold "Alt" and type 0,2,3,2 on the number pad. These numbers correspond to the unicode character value. 232 == 0xe8 == è

<figure class="blog-figure">
  <img src="/images/accents.png" alt="Table of accented characters and their codes"/>
  <figcaption>
    Accented characters and their corresponding decimal value
  </figcaption>
</figure>

I realize this sounds awkward, but it actually becomes very fast. I have most of the relevant codes committed to memory, even many years later. I don't have many opportunities to type in French these days, except for on IRC sometimes. In those cases I just omit the accents.

## The problem

All of a sudden, I have a need to type a more formal document in French. It is a cover letter for a remote job out of Montréal, working with my favourite front-end stack Nuxt.js (A framework around Vue.js that enables SSR and lots of other cool stuff). I use Nuxt for the majority of my personal projects, and I would love to be able to work with it full time.

As a challenge to myself and to get myself in a French state-of-mind (?) I decided to write the cover letter in French first. Words are flowing but I keep trying to hit "Alt" and the numberpad to type accented characters. I could just omit them for now, the edit them in later. But that is just not my process, I find it disruptive.

There are [means of typing these characters under Linux](https://wiki.linuxquestions.org/wiki/Accented_Characters), but they are not ideal for me.

## The solution

Being a master procrastinator, the only sane option is to implement these keyboard shorcuts on Linux myself. How long could that possibly take?

## Longer than I thought

I start with the simplest possibility, the custom keyboard shortcuts offered by my desktop environment, Cinnamon. Immediately I hit complications. These shortcuts allow you to run a command when a key combination is pressed. Unfortunately, what I need is slightly different. I need to grab the subsequent keystrokes *while* "Alt" is held down.

The next possibility I investigated was [Autokey](https://github.com/autokey/autokey). I hear it is more powerful. Unfortunately, it was immediately disqualified for being too slow. Advanced functionality is done using Python scripts, which take at least a full second to even begin running. I need the whole process to take less than a second.

## The hacky hybrid solution

Giving up on implementing this cleanly, I decide to get hacky. I will use the OS custom keyboard shortcuts to launch a utility that captures the subsequent keypresses and does the magic.

<figure class="blog-figure">
  <img src="/images/cinnamon_shortcuts.png" alt="Screenshot of Cinnamon custom keyboard shortcut configuration"/>
  <figcaption>
    Configuring custom keyboard shortcuts with the Cinnamon desktop environment
  </figcaption>
</figure>

When it's a hacky solution that needs to be fast, Bash is my go to. It gives me the execution speed of C with the development speed of a higher-level language. I decided on "Alt + Numpad_0" to take advantage of exisiting muscle memory.

The objective now is to capture the subsequent 3 keystrokes, convert them to the corresponding unicode character and simulate typing the character in the active window.

## Everybody knows X11 is insecure

Being an avid reader of [Hacker News](https://news.ycombinator.com), I was under the impression that X11 is totally insecure and any process can grab keystrokes from any window. I was shocked to find that I couldn't easily capture/inject keyboard characters from/to the X11 window of my choosing.

I can send the event to the window of my choosing, but X11 events generated by XSendEvent are ignored by every application I tried. I couldn't even log the keystrokes from the window of my choosing (using [xev](https://linux.die.net/man/1/xev)) as the keyboard events were not received. It is possible I was just doing it wrong, but unable to proceed I changed tactics.

`xev` can launch a small window and report all the events in that window. I could launch a small, unobtrusive window and use that to grab the keystrokes. That still leaves the problem of injecting the character at the end, but at least it is progress.

## Putting it all together

Emitting the character to the active window ended up having an easy solution; Copy & paste! 'xclip' lets us store things in the clipboard, and 'xdotool' will let us simulate "Ctrl + V" to paste. Since paste automatically goes to the active window, it is mission accomplished. As an added bonus, by firing the keyup event for the "Alt" key, we don't even have to let go of "Alt" (Alt has its own uses on Linux, such as Alt+F opens the current window's file menu).

You see, on Windows, you hold "Alt" while typing the code. My hack launches the utility with "Alt + 0". This means I should probably let go of "Alt" before typing the code, but if I forget out of habit, it will still work. The semantics are identical.

I present to you the finished Bash script (the decimal\_to\_unicode dependency source can be found [here](https://github.com/jeremy21212121/decimal-to-unicode)):


```shell
#!/bin/bash 

set -e;

# Pop a small window in the corner to grab keystrokes. We use timeout to kill the process after 800ms,
# you may need to adjust this value depending on how fast you type.
raw_value=$(timeout 0.7s xev -geometry 1x1+0+0 -event keyboard | grep -A4 --line-buffered '^KeyPress' | grep 'XLookupString' | sed -n 's/.*\"\(.\)\"/\1/p');

# fire keyup for "Alt" in case I didn't let go of it. This allows the semantics to match those of Windows exactly.
xdotool keyup "alt";

# By storing multi-line subshell output as a var, it seems to replace the newlines with spaces.
# It would be more efficient to incorporate this into the previous command but I couldn't make it work.
final_value=$(echo -n $raw_value | sed -n 's/ //gp');

# Currently only handling values between 100 and 999. This is all I need, but there is no reason it couldn't
# be extended to a wider range of decimal unicode values.
if [[ ( "$final_value" -gt 99 && "$final_value" -lt 1000 ) ]]
then
	# Convert decimal number to a unicode char and add it to clipboard
	$HOME/projects/bash_scripts/decimal_to_unicode.sh $final_value | xclip -selection "clipboard";
	# Paste accented character into active window.
	# Note this won't work in the terminal, where the command to paste is Ctrl+Shift+V
	xdotool key --clearmodifiers "ctrl+v";
	# We could add some logic to find out if the active window is a terminal and use "ctrl+shift+v" in that case.
	# I don't actually need to use accented characters in the terminal, so it is not a priority.
fi

exit 0;
```

## Shortcomings

It does not work in the terminal (where paste is "Ctrl+Shift+V"). It also doesn't work perfectly in the browser, but it depends on the site. The browser loses focus then regains focus, but the individual text input on the webpage doesn't always get the focus back.

On the bright side, there is a work-around for any instance where the character fails to paste properly. The character will remain on your clipboard, which means you can manually paste it in wherever you like!

## Summary

This hacky little keyboard shortcut arrangement works surprisingly well. It is now quite easy for me to type in French on my English keyboard layout.

<span lang="fr-CA">
*Merci beaucoup d'avoir lu mon article de blog. J'espère que vous reviendrais bientôt!*
</span>

