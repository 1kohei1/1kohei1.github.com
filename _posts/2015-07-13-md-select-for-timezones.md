---
layout: post
title: "md-select for timezones with one variable"
description: "Let users select timezone with md-select"
category: 
tags: [AngularJS, Angular Material]
---
{% include JB/setup %}

I needed to let users select timezone for various countries. This is what I have done. 
The countries are United States, United Kingdom, Canada, and Australia.
Also I wanted to easily tell timezones for each countries.

For Canada and Australia, even states are in the same timezone district, some states adopts summer time and some don't. That was very confusing. Wikipedia for [Time in Canada - Wiki](https://en.wikipedia.org/wiki/Time_in_Canada) and [Time in Australia - Wiki](https://en.wikipedia.org/wiki/Time_in_Australia) were very helpful. Timezone names are taken from [List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

<p data-height="268" data-theme-id="0" data-slug-hash="YXvyYJ" data-default-tab="result" data-user="1kohei1" class='codepen'>See the Pen <a href='http://codepen.io/1kohei1/pen/YXvyYJ/'>Timezone md-select</a> by Kohei Arai (<a href='http://codepen.io/1kohei1'>@1kohei1</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>