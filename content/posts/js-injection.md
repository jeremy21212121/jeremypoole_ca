+++
date = "2020-04-03"
lastmod = "2021-02-05"
title = "JavaScript injection on CanadaPost.ca"
description = "Finding a JavaScript injection vulnerability on the Canada Post website"
image = "images/js_injection_canadapost.jpg"
tags = ["javascript","security"]
math="false"
published="true"
+++

<figure class="blog-figure">
  <img src="/images/js_injection_canadapost.jpg" alt="JavaScript injection vulnerability on Canada Post"/>
  <figcaption>
    JavaScript injection on Canada Post. Images from <a href="https://pixabay.com" target="_blank" rel="noopener">Pixabay</a>.
  </figcaption>
</figure>

> **TL;DR:** CanadaPost.ca doesn't sanitize input on *invalid* logins. This is a bug that allows for execution of user input. Impact seems quite low.

> **POC:** Canadapost.ca -> "Sign in" button on top right -> Any username, with this password: `', key: alert("meow"), otherKey: '`

## Introduction

I recently discovered a failure to sanitize user input on Canada Post's website.

I stumbled across it by accident. When trying to log in to my account, I was greeted by a never-ending spinner and a console error: Unexpected character.

Following the error, I see some javascript code that contains the username and password I entered. The latter contained an improperly-formatted string. Because my password had an apostrophe in it, and it was being reflected back into a script tag unsanitized, it was causing a syntax error.

After further testing, I determine the console error is only triggered if the password is incorrect *and* it contains an apostrophe ('). Finding it was a total fluke.

## Can we execute?

The next question any budding security enthusiast would ask is what can be done with this? Let's look at the code.

```JS
require(["app", "jquery", "./resources/js/login" ], function (AppManager,$) {
                $(function() {
                	var captchaWidgetId;
                    var username = 'me@email.ca';
                    var loginUser = {username: 'me@email.ca', remember: false, password: 'pass'word', captchaWidgetId: ''};
...
```

This is the relevant snippet that is causing the console error.

I believe that `require` function relates to Angular 1.x and was apparently <a href="https://www.codelord.net/2016/11/30/advanced-angular-1-dot-x-component-communication-with-require/" target="_blank" rel="noopener">used for communication between components</a>.  I think being forced to maintain a legacy Angular 1.x app would be an effective punishment.

As you can see, the value of `loginUser.password` is neither escaped nor sanitized. This means we can inject JavaScript in the context of the above function!

The goal now is to craft an input that is both valid syntax and, ideally, does something interesting. The injection is in the middle of an object, so let's try and add a key/value to the object.

Here's a first attempt at crafting an input:

```JS
', key: alert("meow")
```

This results in the following: 

```JS
var loginUser = {username: 'me@email.ca', remember: false, password: '', key: alert("meow")', captchaWidgetId: ''};
```

Close, but there is still a syntax error preventing `alert()` from being executed. This is because of the single apostrophe being appended after the crafted input. I forgot to capture the syntax that follows our payload.

Let's add another property to the object, just to make the syntax valid:

```JS
', key: alert("meow"), otherKey: '
```

This payload returns the following:

```JS
...
var loginUser = {username: 'me@email.ca', remember: false, password: '', key: alert("meow"), otherKey: '', captchaWidgetId: ''};
...
```

Success! We have executed code in the context of the above function. This is acheived by setting the value of the "key" property to `alert("meow")`. This causes the alert function to execute, and sets the value of the "key" property to the return value of the function, in this case `undefined`. We don't care about the return value, however, our only goal was to execute code.

## But can we do anything with it?

So what can we do in the context of this function? We can access the page cookies through `document.cookie`, but we aren't authenticated and all the good cookies are HTTP only. We have access to the `AppManager` object. Unfortunately, all we can do with it is submit login credentials for authentication. We can install a key logger to capture subsequent password entries by adding an event listener to the `keyup` or `keydown` event and send that off with an HTTP request. This could be promising, but there is one problem: How would the attacker deliver the payload to the target?

Typically, we would hope to add the payload as query parameters to the end of the URL. This would allow the attacker to send the URL to the target, thereby exposing them to the payload. Unfortunately, in our case it is not so simple. The vulnerable login form is a modal. On submit, it redirects to a page with our payload reflected in the contents of a script tag. Query parameters do not pre-fill the login form, so that is a non-starter.


There is another login form, but it works differently so our payload is not effective.

It is entirely possible that I'm missing something. But as it stands, I can find no way this could be used as a realistic XSS vector.

## Update

As of Feb 2021 this bug is still present on canadapost.ca

I tried to notify them, but I did not receive a response.

