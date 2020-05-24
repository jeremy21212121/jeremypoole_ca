+++
date = "2020-04-21"
title = "Comparing new Canadian COVID-19 stats between the provinces"
tags = ["nuxt.js","vue.js","covid-19"]
math="false"
published="true"
+++

<a href="https://jeremypoole.ca/covid" target="_blank" rel="noopener">
<b>
> See the chart in action here
</b>
</a>

<figure class="blog-figure">
<img src="/images/sars2.png" alt="Coronavirus emoji"/>
<figcaption>
SARS-CoV-2 emoji by <a href="https://pixabay.com/users/iximus-2352783/" target="_blank" rel="noopener">iXimus</a>
</figcaption>
</figure>


The <a href="https://www.cbc.ca" target="_blank" rel="noopener">CBC</a> publishes a bunch of great COVID-19 charts that allow you compare various rates between provinces. While they really are well-done in general, I found them lacking in one way: They all use absolute numbers rather than normalized for population (per capita). This makes it really hard to compare between provinces with vastly different populations (two orders of magnitude).

## Data science as a hobby

I'm no data scientist, but I do enjoy munching numbers. Poking around the browser developer tools I found that the CBC has an API for COVID-19 data. As a bonus, they set the CORS header to allow use on any domain, which I take as implicit approval to make gentle use of it myself.

Looking specifically at daily new cases of COVID-19, I thought that it would be more informative to compare the province's rates per capita. I settled on cases per one million people.

## Pick a stack, any stack

I've been using Nuxt.js a lot lately, so it was a natural choice.

There isn't a ton of benefit to server-side rendering this project. It uses Chart.js under the hood, which renders into a `<canvas>` element. SSR-ing the contents of a `<canvas>` element isn't really possible, as there in no DOM to render.

But Nuxt has more to offer than just SSR. The additional lifecycle hooks it provides, like `fetch`, are ideal for making API requests. This means the API call doesn't need to be made from the browser, hopefully resulting in a faster load time.

You can check out <a href="https://github.com/jeremy21212121/covid-new-canada" target="_blank" rel="noopener">the github repo here</a>.

## Normalizing the data

In addition to the "new cases" API endpoint 
<a href="https://canopy.cbc.ca/live/covid_data/api/canada/daily/new_cases" target="_blank" rel="noopener">here</a>
, I also got a CSV from Statistics Canada containing the latest population data and munged it into 
<a href="https://github.com/jeremy21212121/covid-new-canada/blob/master/static/population.js" target="_blank" rel="noopener">pretty JSON</a> with `csvjson` from csvkit and `jq`.

There is one other thing that irked me about the data. My home province, British Columbia, does not release data on Sundays. This shows as a zero datapoint for that day, which I feel is misleading. To address this, I wrote <a href="https://github.com/jeremy21212121/covid-new-canada/blob/master/pages/index.vue#L92" target="_blank" rel="noopener">some code</a> to map those values to `null`. Combined with the Chart.js options `spanGaps`, there is no datapoint shown on the chart for that day.

I saw the CBC take a different approach to deal with the BC's lack of Sunday data points on one of their charts. They average the values for Saturday - Monday. I had already implemented my "span the gaps" strategy, but I'm really not sure if one is "more accurate" than the other. Drop me a line if you know.

# Show me the chart, already

OK, <a href="https://jeremypoole.ca/covid" target="_blank" rel="noopener">here it is</a>. You can compare various provinces and the nation as a whole. Just click on the regions you want to enable in the legend at the bottom. Hover/clicking on individual points on the chart will show you the absolute value.

It is just a quick prototype and it is not very mobile-friendly. The legend does not work great on mobile and we could probably exclude the data points from before about March to make it better fit the screen.

# Limitations

Unfortunately, the numbers never tell the whole story. These are just the confirmed cases and each province tests differently. 

Here are a few more factors to keep in mind:

- Tests can get backed up, resulting in a backlog of cases all being reported at the same time.

- There is no distinction between a large number of cases in a single facility or community spread.

- In low-population provinces, a small absolute number of cases can result in a huge spike in cases per million people.

# Conclusion

I find numbers comforting. It helps me feel like I know what is going on and I can plan accordingly. This may just be a comforting illusion but, either way, I will take it.

Stay safe and look out for each other.




