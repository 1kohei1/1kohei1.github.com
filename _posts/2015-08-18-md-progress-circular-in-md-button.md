---
layout: post
title: "md progress circular in md button"
description: "Show nice circular spinner in md-button with using md-progress-circular"
category: 
tags: [Angular Material, AngularJS]
---
{% include JB/setup %}
I wanted to show the nice spinner while waiting the response from the server. Luckily, Angular Material has nice looking spinner, `md-progress-circular`. I wanted to show this in the button when user submits the form.

The problem is the spinner takes space and expands the button. So I needed to figure out the way to keep the button size even when the spinner is spinning in the button. Anyway, here is the demo on [codepen](http://codepen.io/1kohei1/pen/XbwMLQ)!

<p data-height="268" data-theme-id="0" data-slug-hash="XbwMLQ" data-default-tab="result" data-user="1kohei1" class='codepen'>See the Pen <a href='http://codepen.io/1kohei1/pen/XbwMLQ/'>Progress Circular in md-button</a> by Kohei Arai (<a href='http://codepen.io/1kohei1'>@1kohei1</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>