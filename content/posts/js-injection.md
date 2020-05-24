+++
date = "2020-04-03"
title = "JavaScript injection"
tags = ["javascript","security"]
math="false"
published="true"
+++

# is it exploitable?

I recently found a failure to sanitize user input on Canada Post's website.

I stumbled across it by accident. When trying to log in to my account, I was greeted by a never-ending spinner and a console error: Unexpected character.

Following the error, I see some javascript code that contains the username and password I entered. The latter contained and improperly-formatted string. Because my password had an apostrophe in it and it was being reflected back into a script tag unsanitized, it was triggering a syntax error.

After further testing, I determine the console error is only triggered when the username/password are incorrect. In other words, finding it was a total fluke.

The next question any budding security enthusiast would ask is what can I do with this? Let's look at the code.

```JS
require(["app", "jquery", "./resources/js/login" ], function (AppManager,$) {
                $(function() {
                	var captchaWidgetId;
                    var username = 'me@email.ca';
                    var loginUser = {username: 'me@email.ca', remember: false, password: 'pass'word', captchaWidgetId: ''};
...
```

This is the relevant snippet that is causing the console error. As you can see, the value of loginUser.password is neither escaped nor sanitized. This means we can inject JavaScript in the context of the above function.

The goal now is to craft an input that is both valid syntax and, ideally, does something nefarious. The injection is in the middle of an object, so let's try and add a key/value to the object.

Let's take a crack at crafting an input:
```JS
', key: alert("meow")
```

This results in the following: 
```JS
var loginUser = {username: 'me@email.ca', remember: false, password: '', key: alert("meow")', captchaWidgetId: ''};
```

Close, but we are still getting a syntax error, preventing alert from being executed. This is because of the single apostrophe being appended after our crafted input. We forgot to capture the syntax that follows our payload.

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

Typically, we would hope to add the payload as a query parameter to the end of the URL. This would allow the attacker to send the URL to the target, thereby exposing them to the payload. Unfortunately, in our case it is not so simple. The vulnerable login form is a modal. On submit, it redirects to a page with our payload reflected in the contents of a script tag. Query parameters do not pre-fill the login form, so we have no way of sending a malicious link to our target.

I just can't find any way to weaponize this. There is another login form, but it works differently so our payload is not effective.

It is entirely possible that I'm missing an obvious method of weaponizing this payload. Unfortunately, I don't believe that to be the case. That means we are at a dead end.
