+++
date = "2020-11-11"
lastmod = "2021-02-05"
title = "Protecting API keys on the front-end using NGINX"
decription = "Using a reverse proxy to keep secrets out of a client web application"
image = "images/nginx_security1006x530.jpg"
tags = ["security","webdev","devops"]
math="false"
published="true"
+++

<figure class="blog-figure">
<img src="/images/nginx_security.jpg" alt="Nginx logo over the shadowy face of a hooded hacker, with streams of ones and zeroes coming out of the hood."/>
<figcaption>
Awesome haxor image by <a href="https://pixabay.com/users/geralt-9301" rel="noopener noreferrer">Gerd Altmann</a>
</figcaption>
</figure>

It is fairly straight forward, at least in theory, to keep secrets out of source control systems like git. When it comes to client-side web applications, however, it is very difficult to keep secrets, like API keys, out of the application bundle.

The reason for this is simple. The client-side application needs those secrets, usually API keys, to function. This means that, no matter how you obfuscate them in the code, all one must do is open the "Network" tab in the browser dev tools to find these keys.

Some services, such as those offered by Google, allow you to tightly restrict the usage of an API key. You can restrict a key by domain or IP address for example. The domain restriction isn't bullet-proof, however, because a bad actor could spoof the "referer" header from the server side, thereby appearing to originate from an allowed domain.

I found a nice solution to a few of these problems that I would like to share. Now, exposing anything on the internet has a ton of security implications. I will cover a few here, but there is always a chance that I missed some.

## NGINX to the rescue

Nginx, for the uninitiated, is a very versatile, battle-tested web server. It can be used for serving static files, but also as [reverse proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/), TLS termination (HTTPS) and load balancer, to name a few use cases.

This particular blog post is about using Nginx to proxy API calls, thereby hiding the API key from the front-end application.

### Example time

Let's say you have an API call to the Google Places API to get and display business hours on a webpage. This is something I have a done a bunch of times. The typical approach would be to call the API endpoint directly from the web page/app, thereby exposing the API key to the wider world. This can be partially mitigated by restricting the domains the key can be used from, but, as I mentioned earlier, that is not bullet-proof.

Instead, what I have been doing is exposing a proxied endpoint on the first-party domain. For example, lets say the desired path is `/api/v1/hours`. We can configure Nginx to proxy calls to that endpoint to the desired Google API endpoint. This has benefits in addition to hiding the API key from the client app. By only calling the Google API from the server-side, we can restrict the key to just one IP address. This means that even if the key leaks, it will be useless to anyone else.

There are some security considerations to keep in mind. You application will think this is a first-party request, so, depending on the application, it might send cookies or auth tokens from the application on to the Google API. Obviously, this would be bad. By consulting the extensive and sometimes-overwhelming Nginx docs, I believe I have mitigated these risks.

### The Nginx config

Conceptually, it is a little bit confusing because you have request/response pairs being made in different contexts. Hopefully this Windows 98 style diagram clears things up.

<figure class="blog-figure">
<img src="/images/proxy-diagram.jpg" alt="Simple reverse proxy diagram highlighting the separate requests: from browser to proxy and from proxy to server."/>
<figcaption>
Retro diagram indicating the two separate requests involved in a reverse-proxied request. We'll be setting response headers on the green (left) and request headers on the blue (right).
</figcaption>
</figure>




```
# Proxy cache settings.
# Caches the results for 10 minutes to reduce API billing and latency.
proxy_cache_path /var/lib/nginx/cache levels=1:2 keys_zone=backcache:8m max_size=50m;
proxy_cache_key "$scheme$request_method$host$request_uri$is_args$args";

# Only cache valid responses for a max of 10 minutes
proxy_cache_valid 200 10m;

#...

location /api/v1/hours {

		# Enables the cache settings from above
		proxy_cache backcache;

		# Optional. Allows bypassing the cache if the request includes the 'cache-control: no-cache' header,
		# like when pressing Shift + Reload or disabling caching in the browser dev tools.
		proxy_cache_bypass $http_cache_control;

		# Add a header to the response that tells us the cache status of that request.
		# Expected values are HIT, MISS, BYPASS or EXPIRED
		# This is optional, but can help with debugging.
		add_header X-Proxy-Cache $upstream_cache_status;

		# Don't allow the upstream server to set cookies in the browser
		proxy_hide_header 'Set-Cookie';

		# Remove some google-specific headers that we don't need
		proxy_hide_header 'alt-svc';
		proxy_hide_header 'server-timing';

		# Ignore the following headers so they don't control our caching decision.
		# We want to use our own caching strategy, not Googles.
		proxy_ignore_headers 'X-Accel-Expires' 'Expires' 'Cache-Control' 'Set-Cookie';

		# Make sure the client can't pass their cookies or bearer token to the upstream API.
		# By setting them to empty strings Nginx will omit them. The 'Proxy-Authorization'.
		proxy_set_header 'Authorization' '';
		proxy_set_header 'Cookie' '';
		proxy_set_header 'Proxy-Authorization' '';

		# Optionally don't pass the referer header upstream.
		# If your API key is also restricted by domain, you will need to comment out the next line.
		proxy_set_header 'Referer' '';

		# Proxy the request
		proxy_pass https://maps.googleapis.com/maps/api/place/details/json?key=K3Y&place_id=1D&fields=opening_hours;
	}
```

### Conclusion

Using this strategy, you can create first-party endpoints for each external API endpoint your application needs to contact. In addition to helping secure your API keys, it can also be used with caching to reduce call volume to metered API endpoints. This strategy helps me keep lower-volume sites in the Google API free tier! Even with a 10 minute cache duration, that reduces calls to the upstream metered API to approximately one every 10 minutes[0], or 432 requests per month, which is well within the free tier.

There will be some additional latency introduced here. In my case, a cache miss takes about 180ms[1], which is about 50ms longer than a direct request from browser to google API. But a cache hit, on the other hand, takes only ~20ms[1]. That is a reduction of 110ms or 85%. It can take some fine tuning to find the ideal cache size and duration for your use-case. In this case, the business hours change infrequently and even a 20 minute cache limit would be perfectly acceptable.

For further reading, check out [Googles API key best practices](https://developers.google.com/maps/api-key-best-practices) and [Nginxs reverse proxy guide](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/).

### Footnotes

[0] There is no guarantee that requests will only hit the upstream server once every cache duration period, there are a bunch of edge cases.

[1] If a fresh TLS handshake is required, it will add up to 50ms to this duration.


